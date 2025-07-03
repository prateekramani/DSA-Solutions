0-1 Knapsak Problem

```
class Solution {
    static int knapsack(int W, int val[], int wt[]) {
        
        int [][] dp = new int[W+1][val.length+1];
        for (int[] row: dp) Arrays.fill(row, -1);
        return knapsackUtil(val, wt, W, val.length, dp);
    }
    
    static int knapsackUtil (int val[], int wt[], int W, int n, int[][]dp) {
        if (n == 0 || W == 0) return 0;
        if (dp[W][n] != -1) return dp[W][n];
        if (wt[n-1] <= W){
            return dp[W][n] = Math.max(val[n-1] + knapsackUtil(val, wt, W-wt[n-1], n-1, dp) , knapsackUtil(val, wt, W, n-1, dp));
        } else {
            return dp[W][n] = knapsackUtil(val, wt, W, n-1, dp);
        }
    }
}
```

Tabulation

```
class Solution {
    static int knapsack(int W, int val[], int wt[]) {
        
       int dp[][] = new int [W+1][val.length+1];
       
       for (int i=0;i<W;i++) dp[W][0] = 0;
       for (int i=0;i<val.length;i++) dp[0][i] = 0;
       
       for (int i=1;i<dp.length;i++){
           for (int j=1;j<dp[0].length;j++){
               if (wt[j-1] <= i){
                   dp[i][j] = Math.max(val[j-1]+ dp[i-wt[j-1]][j-1] , dp[i][j-1]);
               } else {
                   dp[i][j] = dp[i][j-1];
               }
           }
       }
       
       return dp[W][val.length];
       
    }

}

```
