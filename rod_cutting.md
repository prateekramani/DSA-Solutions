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

```
