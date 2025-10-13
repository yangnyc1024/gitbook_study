# 6 Video Recommendation System

* Clarifying requirements
  * suggest post from content creator
  * improve dau or session or engagement for the viewer
  * ml objective is aligned with the business motive: DAU/ session
  * viewing content: engaging, liking, commenting so on
  * ML model that improves individual engagement: view/ post/ liking/ commenting
  * non-funtional
    * scalable
    * available
    * tooling
      * debuggability, monitoring, MLoperations, alerts and warnings
    * analytics
  * estimation
    * DAU 500 million
* Framing as ML
  * Defining the ML objective
    * Maximize # of user clicks
    * Maximize # of completed videos
    * Maximize watch time
    * Maximize # of relevant videos
  * Specifying input and output
    * input: user
    * output: a ranked list of videos sorted by their relevanace scores
  * ML category
    * Non-personalized —— Rule- based filtering
    * Personalized
      * Content-based filtering
        * user A liked video X& Y, user A liked similar video Z
      * Collaborative filtering
        * user-based
          * find similar user and his related items
        * item-based
        * Hybrid filtering
          * cf+ content, or cf---> content
  * Pipepline
    * Candidate generating-----> Ranking-----> Post Processing& Reranking(fairness & diversity)
* Data preparation
  * User Feature
    * Demographics
    * Behavior history
      * Search history
      * Liked videos
      * Watched videos
      * Impressions
    * Interests
      * 主题/标签分布（user-topic embedding via clustering） 长期兴趣 vs 短期兴趣（Long-term embedding / short-term sequence embedding, e.g. GRU/Transformer）
    * Engagement level / 活跃度：日均观看时长、日均登录频率、近7日/30日活跃度
  * Video features
    * Basic
      * Video ID (embedding), Duration, Language(embedding)
      * titles (pre-train BERT)
      * tags, dance& music(CBOW)
      * likes, views, length
    * Popularity / 流行度：
      * 播放量、点赞数、评论数、分享数
      * 热门趋势特征（time series smoothing: 近1小时、近1天的点击量增速）
    * Content embedding / 内容表示：
      * 文本（标题/字幕 → BERT embedding）
      * 图像（封面图像 → CNN embedding）
      * 视频帧序列（CLIP/Video Transformer embedding）
      * 音频特征（音乐/讲话 embedding）
  * User-video interactions
    * user id, video id
    * interaction type (like, impression ,watch, click, search, comment)
    * iteraction value (8 second, 46 minutes)
    * location(lat, long)
    * timestamp
    * serach history
    * liked videos
    * watched videos and impression
  * Even feature
    * 类目、主办方、文本 embedding（描述/标题）
    * 时间：活动开始时间、剩余时间
    * 地点：经纬度、场馆类型
    * 有 时间窗口（start/end time），过期即失效。
    * 有 空间位置（venue, city, GPS），用户可达性强约束。
    * 有 容量限制（门票数、报名名额），供给不是无限。
    * 消费成本高：需要出行、时间投入、甚至金钱。
    * 内容特征多是文本（标题、描述）、类目、主办方 → 语义特征有限，更多依赖 时间、地理、社交 因子。
  * event user features
    * Demographics / 人口属性：性别、年龄、职业、地域
    * Interests / 兴趣画像：
      * 历史报名/参加过的活动类别（concert, sports, tech talk, meetup）
      * 兴趣 embedding（基于活动标签聚类）
    * Behavior history / 历史行为：
      * 报名/出席/缺席历史
      * 活动停留时长（event dwell time）
      * 活动反馈（rating, review, like, share）
    * Engagement / 活跃度：
      * 报名频率（每周/月几次）
      * 是否活跃在特定类别（比如：音乐会/讲座/户外）
  * event
    * Basic metadata / 基础信息：标题、描述、组织者、类型（concert、seminar、sports）
    * Time / 时间特征：开始时间、结束时间、是否周末/节假日
    * Location / 地点特征：城市、场馆、地理坐标（lat/long）
    * Capacity / 容量特征：总席位数、剩余席位、是否sold out
    * Price / 价格：票价、折扣、是否免费
    * Popularity / 热度：报名人数、浏览次数、收藏次数、社交媒体提及度
    * Organizer reputation / 主办方信誉：评分、历史活动反馈
  * Context Features | 上下文特征
    * User’s current time / 当前时间：离活动开始还有多久
    * User’s location / 当前位置：和活动地点的距离、交通便利性
    * Device / 设备环境：App / Web / Mobile
    * Session context / 会话上下文：
      * 用户正在浏览的活动类别
      * 是否在搜索特定关键字（“rock concert near me”）
  * User-Event Interaction Features | 用户-活动交互特征
    * Geographic distance / 地理匹配：
      * 用户当前位置 vs 活动地点的距离
      * 预计交通时间（driving / public transport）
    * Temporal availability / 时间冲突：
      * 活动时间是否与用户已报名活动冲突
      * 用户的空闲时间与活动时间匹配度
    * Interest match / 兴趣匹配：
      * 用户历史参与的活动类别 vs 候选活动类别相似度
      * 用户 embedding 与活动 embedding 的余弦相似度
    * Price sensitivity / 价格偏好：
      * 用户历史报名的价格区间 vs 候选活动价格
    * Social influence / 社交关系：
      * 好友是否也报名了该活动
      * 共同社交圈对该活动的参与度
    * Freshness & Novelty / 新颖性：
      * 候选活动是否为用户从未参加过的类型
      * 主办方/场馆是否是用户第一次接触
* Model development
  * Pipepline
    * Candidate generating(Recall)------> Ranking-----> Post Processing& Reranking(fairness & diversity)
  * Method 1:Matrix factorization----> collaborated based filter
    * Feedback matrix
      * 全部都是原来user的反应，都是由0，1组成的matrix
      * A = UV factor as two lower-dim matrix,
      * get predict score matrix by times these two lower matrix---> get the score
    * Training loss
      * Squared distance over observed pairs
      * Squared distance over all pairs
      * Weighted combination of observed and unobserved pairs
      * loss = sum (A\_ij - Ui Vj)^2 + w sum (A\_ij - Ui Vj)^2
    * Optimization algorithm
      * SGD
      * WALS
    * Pros & Cons
      * Pros: training & serving speed fast
      * Cons: ony relies on user-video interactions
  * **Method 2: Two tower model (binary classification problem)**
    * user tower + video tower
    * user feature--> user encoder(DNN) --> user embedding
    * video feature--> videoencoder(DNN) --> video embedding
    * find similarity ---> dot product (0.7) ---> cross-entropy loss& sigmoid ---> label
      * 要么在建索引时就只存可用活动（pre-filter），要么在召回结果上再过滤（post-filter）。
      * SGD
      * AUC, ROC curve 80%
    * pro& con
      * pros: utlizes user feautre & handless new user
      * cons: slower serving, training is more expnesive
    * 输入 (Input)
      * Two-Tower = User Tower + Item Tower
      * User Tower 输入
        * 用户特征 (User features)：人口统计、兴趣标签、历史序列 embedding 等
        * 输出：用户向量 u∈Rd
      * Item Tower 输入
        * 物品/活动特征 (Item features)：类目、文本 embedding、地理位置、价格等
        * 输出：物品向量 v∈Rd
      * 👉 最后把 u,vu, vu,v 做 相似度计算：
        * s(u,v)=u⊤v或cos⁡(u,v)s(u,v)
    * 输出 (Output)
      * 任务：二分类 → 判断用户 uuu 是否会对物品 vvv 产生正反馈 (点击/报名/购买)。
      * 输出概率：
      * y^=σ(s(u,v))∈(0,1)
      * 其中 σ\sigmaσ 是 sigmoid 函数。
    * Loss Function (训练损失函数)
      * ![](https://api2.mubu.com/v3/document_image/12267179_8fce97d3-efde-4118-f8a1-149b775981f5.png?)
  * ANN
    * Two-Tower 模型把用户和物品嵌入到同一空间，ANN 是在这个空间里 高效检索最近邻物品 的加速器。没有 ANN，Two-Tower 在大规模推荐里就落不了地。
    * ANN (Approximate Nearest Neighbor)：不用精确比较所有向量，而是用 索引结构 快速缩小搜索范围，只在一小部分候选里做精确比较。
      * k means cluster, bucket,
      * 先找到用户 embedding 属于哪个桶，再只在该桶里查
  * Reranking
    * 方案 A：GBDT（XGBoost / LightGBM）
      * 输入：所有特征拼接成 tabular
        * 用户特征 (User features)
        * 年龄 = 25
          * 平均消费 = 30
        * 活动特征 (Event features)
          * 票价 = 20
          * 活动类目 = 音乐会 交
        * 互特征 (User–Event interaction)
          * 距离 = 5 km
          * 出行时间 = 15 min
          * 是否时间冲突 = 0
          * 好友参加人数 = 3
        * 把它们拼接成一行，就得到
      * 输出：预测一个概率 P(y=1 | user, event)。
      * 优点：解释性强、工程落地快。
      * 缺点：对序列行为建模能力弱。
    * 方案 B：深度 CTR 模型（常见于工业界）
      * Embedding 层：对用户、活动、类目、时间、地点等离散特征 embedding。
      * 行为序列建模：DIN/DIEN/Transformer，把用户历史行为和当前候选活动做 attention。
      * 交互层：Wide\&Deep、DeepFM、DCN，建模高阶交互（用户兴趣 × 活动属性 × 上下文）。
      * 多目标输出：
        * 点击概率 (CTR)
        * 报名概率 (Signup)
        * 到场概率 (Attendance)
    * 方案 C：多任务学习 (Multi-task Learning)
      * 用 shared bottom + task-specific tower。
      * 主任务：到场预测 (Attendance)
      * 辅助任务：点击、报名（帮助缓解稀疏问题）。
    * 训练目标 (Objective)
      * 如果是单任务：
        * L=−∑(ylog⁡y^+(1−y)log⁡(1−y^)
        * 其中 y=1y=1y=1 表示用户真实报名/到场。
      * 如果是多任务：
        * L=w1⋅CTR Loss+w2⋅Signup Loss+w3⋅Attendance Loss
      * 训练样本：
        * 正样本 = 用户真实参加/报名的活动
        * 负样本 = 用户曝光但未报名/未到场的活动
    * 在线服务流程：
      * 输入用户特征 + 候选活动特征。
      * 精排模型输出打分
        * （CTR / CVR / Attendance Probability）。
      * 结合业务目标打分，例如：
        * Final Score=α⋅CTR+β⋅Signup+γ⋅Attendance
        * 按分数排序，返回前 N 个活动。
* Evaluation
  * Offline metrics
    * Precision@k
      * 前k个中符合要求的
      * meausre the proportion of relevant videos among the top k recommended videos.
      * Multiple k valus (1,5, 10) can be used
    * Recall@k
      * Fraction of all relevant items retrieved in the top-k.
    * mAP
      * ranking quality of recommend video
    * Diversity
  * Online metrics
    * CTR
      * number of cliekd videos / total number of recoomenned video
    * \# of completed videos
    * Total watch time
    * Explicit user feedback
    * CVR (Conversion rate, 转化率)
      * Definition: Ratio of conversions to clicks.
    * Retention (留存率)
      * Definition: Fraction of users who return after d days.
    * DAU/MAU (粘性)
      * Definition: Daily active users over monthly active users.
    * Revenue Lift (收入提升)
      * Definition: Percentage increase in revenue compared to control.
    * Latency (延迟)
      * Definition: Time taken to serve a request, usually measured at P95/P99.请求处理所需时间，通常取 P95/P99。
    * Throughput (吞吐量)
      * Definition: Number of requests processed per second.
* Serving
  * Candidate generation
    * two tower neural network
    * retreived the most similar videos from the approximate nearest neighbor service(ANN)
      * these vidoes are ranked based on similarity in the embedding space and are returned as the output
    * prefer efficiency over accuracy , not concerned about flase positives
    * can apply k candidate generation to diversify recommended videos (relevant & popular& trending)
  * Scoring
    * prioritize accuracy over efficiency
    * query user. + thoursands of candidate videos ----> scoring (two tower neural network model) ---> dozens of videos
    * could choose content base filters and pick a model which relies on video features.
  * Re-ranking
    * adding additional criteria or constraint
    * may use standalone ML models to determine if a video is clickbait
    * important thing to consider
      * region -restrict vidoes
      * video freshness
      * video spreading misinformatin
      * duplicate or near-duplicate videos
      * fairness and bias
  * Challenges in recommendation system
    * Serving speed
    * Precision
    * Diversity
    * Cold-start problem
    * Training scalability
* Other talking points
* &#x20;
