# 65. Valid Number

**# 65. Valid Number**

# See the article on Leetcode 
**_Approach 1:_**
class Solution {
    public boolean isNumber(String s) {
        boolean seeDigit = false;
        boolean seeExponent = false;
        boolean seeDot = false;
        
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if(Character.isDigit(c))  {
                seeDigit = true;
            } else if (c == '+' || c == '-') {
                if (i > 0 && s.charAt(i - 1) != 'e' && s.charAt(i - 1) != 'E') {
                    return false;
                }
            }else if (c == 'e' || c == 'E') {
                if (seeExponent || !seeDigit) return false;
                seeExponent = true;
                seeDigit = false;        
            } else if (c == '.') {
                if (seeExponent || seeDot) return false;
                seeDot = true;
            } else {
                return false;
            }
        }
        return seeDigit;
    }
}

