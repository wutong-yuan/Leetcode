# 28. Implement strStr()

**# 28. Implement strStr()**
# 

class Solution {
    public int strStr(String haystack, String needle) {
        if (needle.isEmpty()) return 0;
        if(haystack.isEmpty()) return -1;
        
        int hLen = haystack.length();
        int nLen = needle.length();
        if (hLen < nLen) return -1;

        for (int i = 0; i <= hLen - nLen; i++) { 
            int j = 0;
            while (j < nLen && haystack.charAt(i + j) == needle.charAt(j)) {
                j++;              
            }
            if (j == nLen) {
                return i;
            }
        }       
       return -1; 
    }
}
