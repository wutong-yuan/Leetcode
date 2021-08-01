# 32. Longest Valid Parentheses

**# 32. Longest Valid Parentheses**
# 

https://www.youtube.com/watch?v=VdQuwtEd10M

**_Approach 1: use stack_**
class Solution {
    public int longestValidParentheses(String s) {
        if(s.isEmpty()) return 0;
        Stack<Integer> stack = new Stack<>();
        // the bottom element in the stack is the boundary
        // the next element after that would be our possible target
        
        stack.push(-1);    
        int maxLen = 0;
        
        for (int i = 0; i < s.length(); i++) {
            // if we see '(', we push
            // if we see ')' we pop to make it a pair 
            // unless the stack is empty, meaning the ) is the recounting start 
            // like we are at the last index of the string, "(())(", we need to 
            // recount
            if (s.charAt(i) == '(') {
                stack.push(i);
            } else {
                stack.pop();
                if (!stack.isEmpty()) {
                    int len = i - stack.peek();
                    maxLen = Math.max(maxLen, len);
                } else {
                    // to make the new starting point
                    stack.push(i);
                }
            }
        }
        
        return maxLen;
    }
}

**_Approach 2 : Left scan + right scan_**

class Solution {
    public int longestValidParentheses(String s) {
        if (s.isEmpty()) return 0;
        int openCount = 0;
        int closeCount = 0;
        
        int maxLen = 0;
        // scan from the left to right
        for (int i = 0; i < s.length(); i++) {
            char current = s.charAt(i);
            if (current == '(') {
                openCount++;
            } else {
                closeCount++;
            }
            
            if (closeCount == openCount) {
                int len = 2 * closeCount;
                maxLen = Math.max(maxLen, len);
            }
            // Because we do the following, if we have ")()", after we count the
            // closeCount, it would reset both of them two 0 before we move forward
            // this make sure the open comes before the close
            // correspondingly, when we scan from the right to the left, we would set 
            // both of the to 0 if the openCount > closeCount to make sure the close
            // comes before the open
            if (closeCount > openCount) {
                openCount = 0;
                closeCount = 0;
            }             
        }
        
        openCount = 0;
        closeCount = 0;
        for (int i = s.length() - 1; i >= 0; i--) {
            char current = s.charAt(i);
            if(current == '(') {
                openCount++;
            } else {
                closeCount++;
            }
            
            if (openCount == closeCount) {
                int len = 2 * openCount;
                maxLen = Math.max(len, maxLen);
            }
            
            if (openCount > closeCount) {
                openCount = 0;
                closeCount = 0;
            }
        }        
        return maxLen;        
    }
}

**_Approach 3 : DP_**
**_
_**
class Solution {
    public int longestValidParentheses(String s) {
        int maxLen = 0;
        
        int[] dp = new int[s.length()];
        for (int i = 1; i < s.length(); i++) {
            // we only update our dp once we see a ')'
            if (s.charAt(i) == '(') continue;
            if (s.charAt (i - 1) == '(') {
                // if i > 1 means we are at the second element
                if (i > 1) {
                    // only when we at the second and the first is (, we update 
                    dp[i] = dp[i - 2] + 2;
                } else {
                    // below means the first element is ), then we just put 0
                    dp[i] = 2;
                }
                //below we need to check when we encounter )) do we have enough ( 
                // before )) this is the case (()), 
                // i - dp[i -1] < 0 means, ()), if this is the case, we cannot go deep
                // only we have enough elements before )) to make the formula valid
                // like (())
            } else if (i - dp[i - 1] > 0 && s.charAt(i - dp[i - 1] - 1) == '(') {
                // to make sure not out of bound
                if (i - dp[i - 1] >= 2) {
                    dp[i] = dp[i - 1] +  dp[i - dp[i -1] - 2] + 2;
                } else {
                    dp[i] = dp[i - 1] + 2;
                }
            }
            maxLen = Math.max(maxLen, dp[i]);
        }
        
        return maxLen;
    }
}

**_My code :_**
**_See paper notes if you cannot understand this code below_**

 public int longestValidParentheses(String s) {
        if(s.isEmpty()) return 0;
        int sLen = s.length();
        
        int[] dp = new int[sLen];
        int maxLen = 0;
        
        for (int i = 1; i < sLen; i++) {
            char current = s.charAt(i);
            
            if (current == '(') continue;
            if (s.charAt(i - 1) == '(') {
                if (i - 2 >= 0) {
                    dp[i] = dp[i - 2] + 2;
                } else {
                    dp[i] = 2;
                }
            } else if (i - dp[i - 1] - 1 >= 0 && s.charAt(i - dp[i - 1] - 1) == '(') {
                if (i - dp[i- 1] - 2 >= 0){
                    dp[i] = dp[i - 1] + dp[i - dp[i - 1] - 2] + 2;
                }else {
                    dp[i] = dp[i - 1] + 2;
                }
            }
            maxLen = Math.max(maxLen, dp[i]);
        } 
      return maxLen;  
    }
