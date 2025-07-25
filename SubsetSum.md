
class Solution {

    static Boolean isSubsetSum(int arr[], int sum) {
        // code here
        
        // -- Top Down space optimized Approach -- 
        int prev[] = new int[sum+1];
        int cur[] = new int[sum+1];
        Arrays.fill(prev, 0);
        prev[0] = 1;
        for (int i=1;i<=arr.length;i++) {
            cur[0] = 1;
            for (int j=1;j<=sum;j++){
                if (arr[i-1] > j) {
                    cur[j] = prev[j];
                } else {
                    if (prev[j-arr[i-1]] == 1 || prev[j] == 1) {
                        cur[j] = 1;
                    } else {
                        cur[j] = 0;
                    }
                }
            }
            
            System.arraycopy(cur, 0, prev, 0, sum + 1);
            Arrays.fill(cur,0);
        }
        // System.out.println(Arrays.toString(prev));
        return prev[sum] == 1;
        
        
        
        // -- Top Down Approach --
        
        // int subsetSum[][] = new int[arr.length+1][sum+1];
        
        // for (int i=0;i<subsetSum[0].length;i++){
        //     subsetSum[0][i] = 0;   
        // }
        
        // for (int i=0;i<subsetSum.length;i++){
        //     subsetSum[i][0] = 1;   
        // }
        
        // for (int row=1;row<subsetSum.length;row++) {
        //     for (int col=1;col<subsetSum[0].length;col++) {
                
        //         // not taking 
        //         if (arr[row-1] > col){
        //                 subsetSum[row][col] = subsetSum[row-1][col];
        //         } else {
        //             if (subsetSum[row-1][col-arr[row-1]] == 1 || subsetSum[row-1][col] == 1)
        //               { subsetSum[row][col] = 1;}
        //             else 
        //                 {subsetSum[row][col] = 0;}
        //         }
        //     }
        // }
        
        
        // return subsetSum[arr.length][sum] == 1;
        
        
        // ---  DP + Memo Appraoch ---
        
        // int [][] dp = new int[arr.length+1][sum+1];
        
        // isSubsetSumUtil(arr, sum, arr.length, dp);
        
        // return dp[arr.length][sum] == 1;
    }
    
    static int isSubsetSumUtil(int [] arr, int sum, int len, int[][]dp){
        
        // System.out.println("Sum "+ sum + " index " + index);
        
        if (sum == 0) return 1;
        
        if (len == 0 || sum < 0) return 0;
        
        if (dp[len][sum] != -1) return dp[len][sum];
        
        int taking = isSubsetSumUtil(arr, sum-arr[len-1], len-1, dp);
        if (taking == 1){
            dp[len][sum] = 1;
            return dp[len][sum];
        }
        
        int notTaking = isSubsetSumUtil(arr, sum, len-1, dp);
        if (notTaking == 1){
            dp[len][sum] = 1;
            return dp[len][sum];
        }
        
        dp[len][sum] = 0;
        return dp[len][sum];
        
    }
}


Space Optimized Approach
```
 boolean knapsack(int W, int[] wt) {
        
        
        boolean[] dp = new boolean[W + 1];
        dp[0] = true;
        for (int i = 1; i <= wt.length; i++) {
            for (int j = W; j >= wt[i - 1]; j--) {
                dp[j] = dp[j] || dp[j - wt[i - 1]];
            }
        }
      	// System.out.println(Arrays.toString(dp));
        return dp[W];
    }
```
