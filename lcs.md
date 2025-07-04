Recursion + Memo

```


class Solution
{
    //Function to find the length of longest common subsequence in two strings.
    static int[][] dp = new int [1001][1001]; 
    static int lcs(int x, int y, String s1, String s2)
    {
        for(int i=0;i<=x;i++)
        {
            for (int j=0;j<=y;j++)
            {
                dp[i][j] = -1;
            }
        }
        
        lcsUtil (s1 , s2 , x , y);
        
        return dp[x][y];
        
    }
    
    static int lcsUtil (String s1 , String s2 , int i, int j)
    {
        // System.out.println("i "+ i + " j "+j );
        
        if (i==0 || j==0) {dp[i][j] = 0;return 0;}
        
        if (dp[i][j] != -1) return dp[i][j];
        
        if (s1.charAt(i-1) == s2.charAt(j-1))
        {
            dp[i][j] =  1 + lcsUtil(s1, s2 , i-1 , j-1);
            
        }
        else{
            dp[i][j] = Math.max(lcsUtil(s1, s2 , i-1 , j) , lcsUtil(s1, s2 , i , j-1));
        }
        
        return dp[i][j];
    }
    
    
}
```


Tabulation
```
class Solution
{
    //Function to find the length of longest common subsequence in two strings.
    static int lcs(int x, int y, String s1, String s2)
    {
       int [][] dp =  new int [x+1][y+1];
       for (int i=0;i<=x;i++)
           for (int j=0;j<=y;j++)
            if (i==0 || j==0)
                dp[i][j] = 0;
       
       for (int i=1;i<=x;i++)
       {
           for (int j=1;j<=y;j++){
               if (s1.charAt(i-1) == s2.charAt(j-1))
               dp[i][j] = dp[i-1][j-1] + 1;
               else 
                dp[i][j]  = Math.max(dp[i][j-1], dp[i-1][j]);
           }
       }
       
       
    
       return dp[x][y];
    }
    
}
```
