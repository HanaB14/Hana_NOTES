# Dynamic Programming

Keywords: "Minimum/Maximum/Optimal/most/least/shortest/cheapest"
---

[64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/)  

Remarks: 
1. Bottom-up version

2. Remember for max/min: `Math.max()` or `Math.min()`

```java
class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int[][] dp = new int[m][n];

        dp[0][0] = grid[0][0];
        //Base Case
        for(int j=1;j<n;j++){
            dp[0][j] = dp[0][j-1] + grid[0][j];
        }// first row
        for(int i=1;i<m;i++){
            dp[i][0] = dp[i-1][0] + grid[i][0];
        }// first column
        
        //Main Case
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                dp[i][j] = Math.min(dp[i-1][j], dp[i][j-1]) + grid[i][j];
            }
        }

        return dp[m-1][n-1];
    }
}
```

[53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return *its sum*.

---

### Example 1:
**Input:** `nums = [-2,1,-3,4,-1,2,1,-5,4]`  
**Output:** `6`  
**Explanation:** The subarray `[4,-1,2,1]` has the largest sum = `6`.

---

Remarks: 
    Use `maxSum` to track the global maximum.

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int n = nums.length;
        int[] dp=new int[n];
        dp[0] = nums[0];
        int maxSum = dp[0];
        for(int i=1;i<n;i++){
            dp[i] = Math.max(nums[i],dp[i-1]+nums[i]);
            maxSum = Math.max(maxSum,dp[i]);
        }
        return maxSum;
    }
}
```