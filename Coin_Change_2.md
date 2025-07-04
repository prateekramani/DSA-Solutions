Coin Change (Min Ways)

Recursion
```
class Solution {

    public int minCoins(int coins[], int sum) {
        int ans = minCoinsUtil(coins, sum, coins.length);
        if (ans == Integer.MAX_VALUE-1) return -1;
        else return ans;
    }
    
    
    int minCoinsUtil(int coins[], int sum, int num) {
        if (sum == 0) return 0;
        if (num == 0) return Integer.MAX_VALUE-1;
        if (num == 1) {
            if (sum%coins[0] == 0) return sum/coins[0];
            else return Integer.MAX_VALUE-1;
        }
        
        if (coins[num-1] > sum){
            return minCoinsUtil(coins, sum, num-1);
        } else {
            return Math.min(minCoinsUtil(coins, sum, num-1) , 1+minCoinsUtil(coins, sum-coins[num-1], num));
        }
    }  
}
```


Recursion + Memo
```
class Solution {

    public int minCoins(int coins[], int sum) {
        int [][] dp = new int[sum+1][coins.length+1];
        int ans = minCoinsUtil(coins, sum, coins.length, dp);
        if (ans == Integer.MAX_VALUE-1) return -1;
        else return ans;
    }
    
    
    int minCoinsUtil(int coins[], int sum, int num, int[][]dp) {
        if (sum == 0) return dp[sum][num]=0;
        if (num == 0) return dp[sum][num]=Integer.MAX_VALUE-1;
        if (num == 1) {
            if (sum%coins[0] == 0) return dp[sum][num]=sum/coins[0];
            else return dp[sum][num]=Integer.MAX_VALUE-1;
        }
        
        if (coins[num-1] > sum){
            return dp[sum][num]=minCoinsUtil(coins, sum, num-1, dp);
        } else {
            return dp[sum][num]=Math.min(minCoinsUtil(coins, sum, num-1, dp) , 1+minCoinsUtil(coins, sum-coins[num-1], num, dp));
        }
    }
    
}
```

Tabulation
```
class Solution {

    public int minCoins(int coins[], int sum) {
        
        int [][] dp = new int[sum+1][coins.length+1];
        // sum -> row num -> col
        for (int i=0;i<=coins.length;i++) dp[0][i] = 0;
        for (int i=0;i<=sum;i++) dp[i][0] = Integer.MAX_VALUE-1;
        for (int i=0;i<=sum;i++) {
            if (i%coins[0]==0) dp[i][1] = i/coins[0];
            else dp[i][1] = Integer.MAX_VALUE-1;
        }
        
        for (int row=1;row<=sum;row++){
            for (int col=2;col <= coins.length;col++){
                if (coins[col-1] > row)
                    dp[row][col] = dp[row][col-1];
                else 
                    dp[row][col] = Math.min(dp[row][col-1], 1+dp[row-coins[col-1]][col]);
            }
        }
        
        return dp[sum][coins.length] == Integer.MAX_VALUE-1 ? -1 : dp[sum][coins.length];   

    }
}
```
