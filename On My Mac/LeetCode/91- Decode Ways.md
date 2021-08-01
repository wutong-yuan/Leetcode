# 91. Decode Ways

**# 91. Decode Ways**

https://www.youtube.com/watch?v=6aEyTjOwlJU 
Recursive approach - top down with memo
class Solution {
    Map<Integer, Integer> memo = new HashMap<>();
    
    public int numDecodings(String s) {
        if (s.length() == 0 || s == null) return 0;
        return dp(s, 0);
    }
    
    private int dp(String s, int index) {
        
**        // when index == s.length() we reach the end, need to return 1 - valid**
**        // when index == s.length() -1 we only have one possibility - has to return 1 as well**

        if (index == s.length()) return 1;
        if (s.charAt(index) == '0') return 0;
        if (index == s.length() - 1) return 1;
        if (memo.containsKey(index)) return memo.get(index);
        
        int result = dp(s, index + 1);
        if (Integer.parseInt(s.substring(index, index + 2)) <= 26) {
            result += dp(s, index + 2);
        }
        
        memo.put(index, result);
        
        return result;
    }
}

![91- Decode Ways](images/91- Decode%20Ways.png)

Approach 2 : DP with constant space

class Solution {
    public int numDecodings(String s) {
        // example {3,2,6,1,2,3}
        int n = s.length();
        int dp1 = 1; 
        int dp2 = 0;
        
        for (int i = n - 1; i >= 0; i--) {
            char curr = s.charAt(i);
            int dp = (curr == '0' ? 0 : dp1);
            if (i < n - 1 && (curr == '1' || 
                               curr == '2'  && s.charAt(i + 1) < '7')) {
                dp += dp2;
            }
            // assign dp1 t dp2 because for the next characer, dp1 becomes dp2 when adding the next character to the current string
            dp2 = dp1;
            dp1 = dp;            
        }
        
        return dp1;
    }
}
