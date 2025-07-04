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
