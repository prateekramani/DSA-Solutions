
Recursion + Memo Approach
```
public int lengthOfLIS(int[] nums) {
        int [][]dp = new int[nums.length+1][nums.length];
        for (int [] row : dp) Arrays.fill(row, -1);
        return lengthOfLISUtil(nums, -1, 0, dp);
    }


    public int lengthOfLISUtil(int[] nums, int prevIndex, int index, int[][] dp) {
        if (index == nums.length) return 0;
        if (dp[prevIndex+1][index] != -1) return dp[prevIndex+1][index];

        if (prevIndex == -1 || nums[index] > nums[prevIndex]) {
            return dp[prevIndex+1][index] = Math.max(1 + lengthOfLISUtil(nums, index, index+1, dp) , lengthOfLISUtil(nums, prevIndex, index+1, dp));
        } else {
            return dp[prevIndex+1][index] = lengthOfLISUtil(nums, prevIndex, index+1, dp);
        }
    }
```

Tabulation Approach
```
public int lengthOfLIS(int[] nums) {
        int[]dp = new int[nums.length];
        Arrays.fill(dp, 1);
        int ans = 1;
        for (int i=1;i<nums.length;i++) {
            for (int j=0;j<i;j++) {
                if (nums[j] < nums[i]){
                    dp[i] = Math.max(dp[i], 1+dp[j]);
                    ans = Math.max(ans,dp[i]);
                }
            }
        }

        return ans;
    }
```

Binary Search Approach
```
class Solution {
    public int lengthOfLIS(int[] nums) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(nums[0]);
        for (int i=1;i<nums.length;i++) {
            if (list.get(list.size()-1) < nums[i]) {
                list.add(nums[i]);
            } else {
                int index = getUpperBound(list, nums[i]);
                list.set(index, nums[i]);
            }
        }
        return list.size();
    }

    // find greater than or equal to number index
    int getUpperBound(ArrayList<Integer> list, int k) {
        int low = 0;
        int high = list.size()-1;
        int ans = 0;
        while(low <= high) {
            int mid = low + (high - low)/2;
            if (list.get(mid) >= k){
                ans = mid;
                high = mid - 1;
            } else {
                low = mid+1;
            }
        }
        return ans;

    }
}
```

Printing LIS
```
public ArrayList<Integer> getLIS(int nums[]) {
        // Code here
        
        int[]dp = new int[nums.length];
        Arrays.fill(dp, 1);
        int ans = 1;
        int lastIndex = 0;
        int parent[] = new int[nums.length];
        
        for (int i=1;i<nums.length;i++) {
            for (int j=0;j<i;j++) {
                if (nums[j] < nums[i]){
                    if (dp[i] < 1+ dp[j]) {
                        dp[i] =  1+dp[j];
                        parent[i] = j;
                    }
                    
                    if (ans < dp[i]){
                        ans = dp[i];
                        lastIndex = i;
                    }
                }
            }
        }
        
        ArrayList<Integer> list = new ArrayList<>();
        
        while (dp[lastIndex] != 1) {
            list.add(nums[lastIndex]);
            lastIndex = parent[lastIndex];
        }
        list.add(nums[lastIndex]);
        Collections.reverse(list);
        
        return list;
        
    }
```
