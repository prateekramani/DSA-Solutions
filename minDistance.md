https://leetcode.com/problems/edit-distance/description/
```
public int minDistance(String word1, String word2) {
        

        // topdown approach

        int dp[][] = new int[word1.length()+1][word2.length()+1];

        // base cases 

        for (int i=0;i<=word1.length();i++){
            dp[i][0] = i;
        }

        for (int i=0;i<=word2.length();i++){
            dp[0][i] = i;
        }

        for (int i=1;i<dp.length;i++){
            for (int j=1;j<dp[0].length;j++){
                if (word1.charAt(i-1) == word2.charAt(j-1)){
                    dp[i][j] = dp[i-1][j-1];
                } else {
                    int delete = dp[i-1][j];
                    int insert = dp[i][j-1];
                    int replace = dp[i-1][j-1];
                    dp[i][j] = 1 + Math.min(Math.min(delete, insert), replace);
                }
            }
        }

        return dp[word1.length()][word2.length()];

    }
```

// Recursive + Memo approach

```
public int minDistance(String s1, String s2) {
        int m = s1.length();
        int n = s2.length();
        int dp[][] = new int[m + 1][n + 1];
        for(int row []:dp ){
            Arrays.fill(row,-1);
        }

        return path(m , n ,s1, s2,dp);
        
    }
    public int path(int i , int j,String s1,String s2,int dp[][]){

        if(i == 0) return j;
        if(j == 0) return i;

        if(dp[i][j] != -1){
            return dp[i][j];
        }

        if(s1.charAt(i-1) == s2.charAt(j-1))
        return dp[i][j] =  path(i-1, j-1 , s1, s2,dp);
         

         // Characters don't match: choose min of insert, delete, or replace
        int insert = path(i, j - 1, s1, s2, dp);
        int delete = path(i - 1, j, s1, s2, dp);
        int replace = path(i - 1, j - 1, s1, s2, dp);

        return dp[i][j] = 1 + Math.min(insert, Math.min(delete, replace));
    }
```
