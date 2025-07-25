DP + Memo
```
 public int perfectSum(int[] nums, int target) {
        
        int dp[][] = new int[nums.length+1][target+1];
        for (int[] row: dp) Arrays.fill(row,-1);
        
       return perfectSumUtil(nums, target , nums.length, dp);
    }
    
    int perfectSumUtil(int[] nums, int target, int n, int[][]dp){

        if (n == 0 && target == 0) return 1;
        if (target < 0 || n==0) return 0;
        if (dp[n][target] != -1) return dp[n][target];
        
        if (nums[n-1] <= target) {
            return dp[n][target] = perfectSumUtil(nums, target-nums[n-1], n-1, dp) + perfectSumUtil(nums, target, n-1, dp);    
        } else {
            return dp[n][target] = perfectSumUtil(nums, target, n-1, dp);
        }
        
    }
```

Space Optimized Tabular
```
public int perfectSum(int[] nums, int target) {
        // code here
        return knapsack(target, nums);
        
    }
int knapsack(int W, int[] wt) {
        
        int[] dp = new int[W + 1];
        dp[0] = 1;
        for (int i = 1; i <= wt.length; i++) {
            for (int j = W; j >= wt[i - 1]; j--) {
                dp[j] = dp[j] + dp[j - wt[i - 1]];
            }
        }
      	// System.out.println(Arrays.toString(dp));
        return dp[W];
    }
```
