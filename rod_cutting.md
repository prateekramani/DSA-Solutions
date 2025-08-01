DP + Memo

```
    public int cutRod(int[] price) {
        // code here
      
        int dp[] = new int[price.length+1];
        Arrays.fill(dp, -1);
        return cutRodUtil(price, price.length, dp);
    }
    
    int cutRodUtil(int[] price, int n, int[]dp){
        // System.out.println(n);
        if (n == 0) return 0;
        if (dp[n] != -1) return dp[n];
        int tempAns = Integer.MIN_VALUE;
        for (int cut=1; cut <= n; cut ++){
            tempAns = Math.max(tempAns, price[cut-1] + cutRodUtil(price, n-cut, dp));
        }
        
        return dp[n] = tempAns;
        
    }
```

Top Down Approach (Best)
```
public int cutRod(int[] price) {
        // code here
        
        int []dp = new int[price.length+1];
        
        dp[0] = 0;
        
        for (int i=1;i<dp.length;i++){
            int tempAns = Integer.MIN_VALUE;
            for (int cut=1;cut<=i;cut++){
                tempAns = Math.max(tempAns , price[cut-1] + dp[i-cut]);
            }
            
            dp[i] = tempAns;
        }
        
        return dp[price.length];
    }
```

Knapsack (Understanc it like, we have to collect rod parts with their corresponding prices such that total length is Rod)
```
   public int cutRod(int[] price) {
        // code here
        
        int dp[][] = new int[price.length+1][price.length+1];
        
        for (int i=0;i<dp.length;i++){
            dp[0][i] = 0;
            dp[i][0] = 0;
        }
        
        // row = i = N = cut
        // col = j = Weight 
        
        for (int i=1;i<dp.length;i++) {
            for (int j=1;j<dp.length;j++){
                if (i <= j) {
                    dp[i][j] = Math.max(price[i-1] + dp[i][j-i],dp[i-1][j]);
                } else {
                    dp[i][j] = dp[i-1][j];
                }
            }
        }
        return dp[price.length][price.length];
    }
```
