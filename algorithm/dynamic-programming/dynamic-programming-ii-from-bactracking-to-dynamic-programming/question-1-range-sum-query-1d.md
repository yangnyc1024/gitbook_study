# Question 1: Range Sum query 1D

#### Method 1空间O(1)暴力



#### Method 2 PerfixSum(off by 1 VS not off by 1)

Index 0 1 2 3 4

Value  0 3 5 7 9&#x20;

注意你要先定义prefixSum

```java
/*
off by 1
prefixSum[I] represents the sum from [0,i-1] 
prefixSum[I] = prefixSum[I-1] + array[I-1]
partSum[I, j] = prefixSum[j+ 1] - prefixSum[I]

not off by 1
prefixSum[I] represents the sum from [0, I ]
prefixSum[0] = array[0]
prefixSum[I] = prefixSum[I-1] + array[I]
partSum[I, j] = prefixSum[j] - prefixSum[I- 1]
*/


class NumArray {
    int[] prefix;
    public NumArray(int[] nums) {
        this.prefix = new int[nums.length + 1];
        for (int i = 1; i < this.prefix.length; i++) {
            this.prefix[i] = this.prefix[i- 1] + nums[i- 1]; 
        }
    }
    pubic int sumRange(int left, int right) {
        return this.prefix[right + 1] - this.prefix[left];
    }
}



class NumArray {
    int[] prefix;
    public NumArray(int[] nums) {
        this.prefix = new int[nums.length];
        for (int i = 0; i < this.prefix.length; i++) {
            if (i = 0) {
                this.prefix[0] = nums[0];
            }
            this.prefix[i] = this.prefix[i- 1] + nums[i- 1]; 
        }
    }
    pubic int sumRange(int left, int right) {
        if (left == 0) {
            return this.prefix[right];
        }
        return this.prefix[right] - this.prefix[left - 1];
    }
}


```



