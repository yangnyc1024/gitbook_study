# Anomaly Detection



Sources:

* https://docs.datadoghq.com/monitors/types/anomaly/
* https://www.datadoghq.com/blog/watchdog/

### 开场总结

**English:**\
For anomaly detection on a latency time series, I would design the solution as a pipeline with four key stages: **pre-processing, detection model, scoring, and post-processing**. This structure ensures the system is both accurate and practical in production.

**中文:**\
针对延迟类时间序列的异常检测，我会设计一个包含四个主要阶段的流水线：**预处理、检测模型、打分机制和后处理**。这种结构既保证了检测的准确性，也方便在生产环境中落地。

{% stepper %}
{% step %}
### 1. Pre-processing（预处理）

**English:**\
Latency signals usually contain missing values, noise, and seasonal patterns like daily cycles. So the first step is to clean and normalize the data. I would fill missing points with interpolation, smooth sudden spikes if they’re artifacts, and decompose the series to remove seasonality, for example using STL decomposition. This ensures the model focuses on real anomalies instead of predictable fluctuations.

**中文:**\
延迟信号通常包含缺失值、噪声，以及像日周期这样的季节性模式。所以第一步是清理和标准化数据。我会用插值法填补缺失点，对偶然的噪声尖峰进行平滑，并用 STL 分解等方法去除季节性。这样模型就能聚焦在真正的异常，而不是可预测的波动。

* 动机：原始 latency 数据可能包含噪声、缺失值、异常 spikes。
* 做法：
  * 去除 outliers 或平滑 (moving average, EWMA)。
  * 缺失值填补（linear interpolation, forward fill）。
  * 归一化/标准化 (z-score, min-max)。
  * 提取周期性特征 (hour-of-day, day-of-week)。
* 面试示例：比如 latency 通常有日周期，我们会在预处理时去除 seasonality，让后续模型更容易检测真正的异常。
{% endstep %}

{% step %}
### 2. Detection Model（检测模型）

**English:**\
The detection model is the core. For a fast and interpretable baseline, I could use forecasting models like ARIMA or Prophet. They predict expected latency, and anomalies are large residuals. For more complex scenarios, I might use machine learning like Isolation Forest, or deep learning models such as LSTM Autoencoders, which learn and highlight deviations. The choice depends on accuracy requirements and scalability.

**中文:**\
检测模型是核心。为了快速且可解释的基线，我可以用 ARIMA 或 Prophet 这样的预测模型，它们预测期望延迟，残差大的部分就是异常。在更复杂的场景下，可以用机器学习方法比如 Isolation Forest，或者深度学习模型如 LSTM 自编码器，去学习正常的时间模式并识别偏差。选择哪种方法取决于精度需求和可扩展性。

* 方法选型（取决于业务和数据特性）：
  * 统计方法：ARIMA, STL decomposition, z-score threshold。
  * 机器学习：Isolation Forest, One-Class SVM。
  * 深度学习：LSTM Autoencoder, Transformer-based models。
* 面试示例：如果我们想快速上线，可以用基于预测残差的统计方法；如果要 scale 和应对更复杂模式，可以用 LSTM autoencoder。
{% endstep %}

{% step %}
### 3. Scoring（打分机制）

**English:**\
Next, we translate model outputs into anomaly scores. For example, residual size or reconstruction error. Then we set thresholds. A static threshold like three standard deviations can work in stable environments, but for latency, a dynamic threshold such as rolling quantiles is more robust because traffic patterns vary over time.

**中文:**\
接下来，需要把模型输出转化为异常分数，比如预测残差的大小，或者自编码器的重建误差。然后设定阈值。在稳定环境里，可以用固定阈值（比如 3 个标准差）；但对于延迟这种随时间变化的信号，更合适的是动态阈值，比如滚动分位数，因为流量模式会不断变化。

* 模型输出 anomaly score（如残差、重建误差、概率）。
* 将 score 转换成 interpretable 指标。
* 方法：
  * 固定阈值（比如 > 3σ）。
  * 动态阈值（rolling window quantile）。
* 面试示例：对于 latency 这种指标，我会用 rolling quantile 方法来动态设置阈值，因为系统负载在不同时段差异很大。
{% endstep %}

{% step %}
### 4. Post-processing（后处理 / 报警策略）

**English:**\
Finally, we refine the alerts to reduce false positives. Instead of alerting on every single anomaly point, I would aggregate anomalies into windows and require multiple consecutive detections before triggering. I would also integrate business rules, such as only alerting if the p95 latency exceeds the SLA threshold. This makes alerts fewer but more actionable for engineers.

**中文:**\
最后一步是后处理，用来减少误报。不是每个点异常就立刻报警，而是把异常聚合成时间窗口，并要求连续多个点异常才触发报警。同时结合业务规则，比如只有当 p95 延迟超过 SLA 阈值时才报警。这样报警数量更少，但更有意义，工程师才会真正关注。

* 避免误报 & 提升可用性：
  * 连续多个点异常才触发告警 (debouncing)。
  * 聚合成 anomaly windows 而不是单点报警。
  * 结合业务规则（如只在 p95 > SLA 时报警）。
* 面试示例：为了避免 alert fatigue，我们会加 post-processing，比如只有当连续 3 个时间点超过阈值才发出告警。
{% endstep %}
{% endstepper %}

***

### 收尾总结

**English:**\
So in summary, my pipeline is: clean and normalize the latency series, apply forecasting or learning-based models, generate anomaly scores with adaptive thresholds, and post-process the results into meaningful alerts. This structure is both systematic and practical for production monitoring systems.

**中文:**\
总结来说，我的流水线就是：清理并标准化延迟数据，应用预测或学习模型，基于自适应阈值生成异常分数，并通过后处理把结果转化为有意义的告警。这样的设计既系统化，又能真正用于生产监控。

***

## Model

### 📌 Shared anomaly scoring / 通用异常打分

Idea / 假设

*   EN: Independent of model type (ETS, ARIMA, LSTM, HTM…), we usually evaluate residuals:

    $$
    s_t = \frac{|y_t - \hat{y}_t|}{\hat{\sigma}_t}
    $$

    where $\hat{\sigma}\_t$ is model-estimated or empirically estimated uncertainty.
*   CN: 不论使用 ETS、ARIMA、LSTM、HTM，核心思路都是基于残差标准化：

    $$
    s_t = \frac{|y_t - \hat{y}_t|}{\hat{\sigma}_t}
    $$

    其中 $\hat{\sigma}\_t$ 来自模型预测区间，或滚动残差方差。

How to use / 如何用于异常检测

* EN:
  * Prefer model-based PI (prediction interval) if available (ETS, ARIMA, quantile-LSTM).
  * If no PI, use rolling residual variance (EWM std over recent window).
  * Flag when $s\_t$ exceeds threshold (e.g., 99.5% quantile).
  * Add persistence rule (e.g., require 2 out of 3 recent points above threshold) to reduce false alarms.
* CN:
  * 有预测区间的模型（ETS/ARIMA/LSTM-Quantile）→ 用模型不确定度。
  * 无预测区间的模型 → 用滚动残差方差近似。
  * 异常判定：$s\_t$ 超过校准阈值（如 99.5% 分位数）。
  * 引入持续性规则（如最近 3 点中至少 2 点异常）降低噪声。

Variants / 扩展方法

* EN:
  * Dynamic thresholds: exponentially weighted moving average (EWMA) of residual distribution.
  * Robust scores: Median Absolute Deviation (MAD) instead of std.
  * One-sided scoring: For latency SLOs, only flag upward deviations (long-tail).
* CN:
  * 动态阈值：基于残差分布的指数加权移动更新。
  * 稳健统计：用 MAD（中位数绝对偏差）代替方差。
  * 单侧判定：延迟类指标只关注 **向上异常**（长尾风险）。

Pros / Cons

* ✅ Universal: works with any forecaster.
* ✅ Interpretable: standardized score directly shows how abnormal the point is.
* ❌ Needs good variance estimate; otherwise false alarms.
* ❌ May lag in regime shifts (variance baseline needs time to adjust).

***

### Forecasting-based Methods (selected)

#### Exponential Smoothing (ETS / Holt-Winters)

* Idea: Time series decomposed into level (ℓ), trend (b), and seasonality (s). Seasonality can be additive or multiplicative. Multiplicative is useful for latency (variance grows with mean).
* Use for anomalies: ETS state-space formulation provides forecasts and prediction intervals. If y\_t ∉ \[L\_t, U\_t], mark anomaly.
* Key knobs: smoothing params α, β, γ; season length m; additive vs multiplicative; Box-Cox λ transform.
* Pros: Fast & interpretable; handles single strong seasonality.
* Cons: Limited with multi-seasonality; no natural support for covariates unless extended.

Prod tips: use multiplicative seasonality for latency, log-transform latency, auto-tune via AIC/BIC, re-fit nightly and warm-start online updates.

#### ARIMA / SARIMA / ARIMAX

* Idea: After differencing, model as AR + MA; SARIMA adds seasonal terms; ARIMAX adds exogenous regressors.
* Use for anomalies: produce forecasts with variance estimates; flag based on standardized residuals or prediction intervals.
* Key knobs: orders (p,d,q), seasonal (P,D,Q,m), stationarity tests, exogenous regressors, transforms (log/Box-Cox).
* Pros: Good for linear seasonal signals; principled forecast intervals; supports regressors.
* Cons: Weak for nonlinear dynamics; model selection costly at scale.

Prod tips: use auto-ARIMA for initial search, maintain small per-service models, re-diagnose weekly.

#### LSTM / GRU

* Idea: LSTM uses gates to model long-term dependencies; GRU is a lighter alternative.
* Use for anomalies: train as forecaster (point or quantile); anomalies when actual beyond PI; estimate uncertainty with MC Dropout or ensembles.
* Key knobs: window length, hidden units, dropout, loss (MSE or quantile/pinball), teacher forcing for multi-step.
* Pros: capture nonlinearities and covariates; Cons: data hungry, expensive to train, black-box.

Prod tips: scale latency (log+robust scaler), add exogenous features, quantile regression head for p95/p99, early stopping + drift detection.

#### Echo State Networks (ESN)

* Idea: Reservoir computing — fix random recurrent network; only train linear readout.
* Use for anomalies: fast forecaster; anomalies via residuals.
* Pros: Extremely fast training; online adaptation feasible.
* Cons: Sensitive to hyperparams; fewer libraries.

Prod tips: small reservoirs per endpoint, ridge-regularize readout, random re-initialization + validation.

#### Hierarchical Temporal Memory (HTM)

* Idea: Sparse Distributed Representations, online sequence learning; outputs anomaly likelihood directly.
* Use for anomalies: strong for sudden changes/new regimes; outputs anomaly likelihood without explicit forecasting.
* Pros: online learning, adapts to drift automatically.
* Cons: encoder tuning hard; smaller ecosystem.

Prod tips: encode latency in log-scale, add time-of-day/week encoding, use persistence/cooldown to filter transients; pair with ARIMA/LSTM for hybrid.

#### Quantile Forecasting for p95/p99

* Train forecasters to directly predict quantiles (ETS+bootstrapping, Gradient Boosted Quantile, LSTM/GRU with pinball loss). Anomaly if actual exceeds predicted quantile + δ.

#### Multi-scale & ensembling

* Train at multiple granularities (1-min / 5-min / 1-hour) and combine scores (max standardized residuals or calibrated probability average). Or ensemble multiple model types (ETS/SARIMA/GRU) for robustness.

***

#### Minimal anomaly pipeline (pseudo)

```python
# y_t: log-latency metric (per minute); X_t: covariates (traffic, deploy flags, hour, dow)
model.fit(train_y, X_train)        # ETS/SARIMA/GRU/ESN/HTM (HTM “fit” is online)
yhat, sigma = model.predict(y_val, X_val, return_std=True)  # or quantiles

res = np.abs(y_val - yhat)
s = res / (sigma + 1e-6)           # standardized residual
thr = np.quantile(s_calib, 0.995)  # calibrated on clean window
flags = ewma(s > thr, alpha=0.3).astype(int)                # persistence smoothing
alerts = require_n_of_m(flags, n=2, m=3)                    # reduce flaps
```

Production notes:

* Transform: latency → log / Box-Cox; handle zeros with ε.
* Calendar: hour-of-day, day-of-week, holidays, deploy flags as regressors.
* Drift: nightly re-fit + weekly hyper-scan; retrain quickly after major releases.
* Cold start: begin with ETS/ESN; backfill training as data accrues.
* Uncertainty: prefer model PI/quantiles over raw residual std.
* Alert hygiene: persistence, cooldown, dedup, severity tiers (mild/warn/critical).
* Evaluation: PR-AUC, F1@K, false-alert-minutes, MAPE/MASE for forecast sanity; replay past incidents as offline backtests.

***

## Datadog Toto 模型介绍

**Datadog 自研的时序基础模型（Time Series Foundation Model）**

### 1. 什么是 Toto？

* 中文：
  * Toto（Time Series Optimized Transformer for Observability）是 Datadog 开发的时序基础模型，专门为可观测性指标设计。
  * 它是一个零样本预测（zero-shot forecasting）模型，不需要为每个新指标重新训练。
  * 与通用 LLM 不同，Toto 针对高频、多维、非平稳、有异常点的监控指标优化。
* English:
  * Toto (Time Series Optimized Transformer for Observability) is a time series foundation model developed by Datadog.
  * Designed for observability metrics (latency, CPU, traffic, etc.).
  * Enables zero-shot forecasting on new metrics without per-metric retraining.

### 2. 训练数据规模

* 中文：在超过 1–2 万亿个时序数据点上训练。数据来源：约 75% 来自 Datadog 平台的匿名监控指标，其余来自公开数据集和合成数据。
* English: Trained on 1–2 trillion time series data points. Sources: \~75% anonymized Datadog metrics, plus public datasets and synthetic data.

### 3. 技术架构亮点

* Decoder-only Transformer.
* Proportional Factorized Space-Time Attention for efficient multivariate modeling.
* Student-T mixture prediction head to handle heavy-tailed distributions.
* Patch-based normalization & robust composite loss for non-stationary stability.

### 4. 性能表现

* 在 Datadog 发布的 BOOM 基准（Benchmark of Observability Metrics）上表现领先。
* 在 GIFT-Eval、LSF 等公开时序基准测试中零样本性能优异。
* 在真实监控数据上的 sMAPE / sMdAPE 指标优于其他模型。

***
