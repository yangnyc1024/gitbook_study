# Question 7 Trapping Rain Water 1





```java
// Some code

class Solution {
    public int trap(int[] height) {

        /// initialState 外围就两个点
        int left = 0;
        int right = height.length - 1;

        // minHeap.offer(<左端点，左普高>， <右端点，右普高>)
        int leftMax = height[0];
        int rightMax = height[height.length - 1];
        
        // totalResult
        int totalWater = 0;

        while (left < right) { // while(!minHeap.isEmpty())
            // generate and update 左右端点普高
            leftMax = Math.max(leftMax, height[left]); 
            rightMax= Math.max(rightMax, height[right]);

            if (leftMax <= rightMax) { // minHeap.poll() 普高中的最小值
                totalWater  += leftMax - height[left]; // left准备进入下一轮的generate
                left++;
            }
            else {
                totalWater  += rightMax - height[right]; // right准备进入下一轮的generate
                right--;
            }
        }
        return totalWater;
    }
}

```
