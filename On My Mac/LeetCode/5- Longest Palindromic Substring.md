# 5. Longest Palindromic Substring

**# 5. Longest Palindromic Substring**

https://www.youtube.com/watch?v=XYQecbcd6_c 
# 

class Solution {
    
    private String result = "";
    private int maxLength = 0;
    
    public String longestPalindrome(String s) {
        int n = s.length();
        
        if (n == 1) return s;
        
        for (int i = 0; i < n; i++) {
            helper(s, i, i); 
            helper(s, i, i + 1);          
        }
        
        return result;
    }
    
    private void helper(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
           if (right - left + 1 > maxLength) {
                maxLength = right - left + 1;
                result = s.substring(left, right + 1);
            }  
            
            left--;
            right++;        
        }           
    }
}

Brute force 
 class Solution {
    public String longestPalindrome(String s) {
        
        int maxLength = 0;
        String result = "";
        if (s.length() == 1) {
            return s;
        }
        
        for (int i = 0; i < s.length(); i++) {
            for (int j = i + 1; j < s.length() + 1; j++) {
                String sub = s.substring(i, j);
                if (isPalindrome(sub)) {
                    if (sub.length() > maxLength) {
                        maxLength = sub.length();
                        result = sub;
                    }
                }   
            }
        }
        
        return result;
    }
    
    private boolean isPalindrome(String s) {
        String reversedS = reverse(s);
        if (reversedS.equals(s)) {
            return true;
        }
        return false;
    }
    
    private String reverse(String s) {
        StringBuilder sb = new StringBuilder();
        for (int i = s.length() - 1; i >= 0; i--) {
            sb.append(s.charAt(i));
        }
        
        String reversedS = sb.toString();
        
        return reversedS;
    }
}
