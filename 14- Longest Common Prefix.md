# 14. Longest Common Prefix

**# 14. Longest Common Prefix**

class Solution {
    public String longestCommonPrefix(String[] strs) {
       if (strs.length == 1)  return strs[0];
        
        String first = strs[0];
        int i = 0;
        
        for (; i < first.length(); i++) {
            for (int j = 1; j < strs.length; j++) {
                if (i > strs[j].length() - 1) return first.substring(0, i);
                if (first.charAt(i) != strs[j].charAt(i)) {
                    return first.substring(0, i);
                }
            }
        }
        
        return first.substring(0, i);
    }
}

// TC: worest case we need to go through all the characters in strs. O(S)
