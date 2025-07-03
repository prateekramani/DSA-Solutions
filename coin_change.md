Coin Change (infinite Suppy)

Recursive Approach
```
class Solution {
    public int count(int coins[], int sum) {
        return countUtil(coins, sum, coins.length);
    }
    
    
    int countUtil(int coins[], int sum, int n) {
        if (sum == 0) return 1;
        
        if (n == 0) return 0;
        
        if (sum >= coins[n-1]){
            return countUtil(coins, sum-coins[n-1], n) + countUtil(coins, sum, n-1);
        } else {
            return countUtil(coins, sum, n-1);
        }
    }
}
```

Recursion + Memo
```
class Solution {
    public int count(int coins[], int sum) {
        int dp [][] = new int[sum+1][coins.length+1];
        return countUtil(coins, sum, coins.length, dp);
    }
    
    
    int countUtil(int coins[], int sum, int n, int[][] dp) {
        if (sum == 0) return dp[sum][n] = 1;
        
        if (n == 0) return dp[sum][n] = 0;
        
        if (sum >= coins[n-1]){
            return dp[sum][n] = countUtil(coins, sum-coins[n-1], n, dp) + countUtil(coins, sum, n-1, dp);
        } else {
            return dp[sum][n] = countUtil(coins, sum, n-1, dp);
        }
    }
}
```

Tabulation
```
class Solution {
    public int count(int coins[], int sum) {
        int dp [][] = new int[sum+1][coins.length+1];
        
        for (int i=0;i<=sum;i++) dp[i][0] = 0;
        for (int i=0;i<=coins.length;i++) dp[0][i] = 1;
        
        
        // sum = row , n = col
        for (int row=1;row<=sum;row++){
            for (int col=1;col<=coins.length;col++){
                if (row >= coins[col-1]){
                    dp[row][col] = dp[row-coins[col-1]][col] + dp[row][col-1];
                } else {
                    dp[row][col] = dp[row][col-1];
                }
            }
        }

        
        return dp[sum][coins.length];

    }
}
```
