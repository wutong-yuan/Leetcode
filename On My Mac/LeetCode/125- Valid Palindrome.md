# 125. Valid Palindrome

**# 125. Valid Palindrome**

# 

**_Use extra space_**

class Solution {
    public boolean isPalindrome(String s) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < s.length(); i++) {
            char curr = s.charAt(i);
            if(Character.isAlphabetic(curr)) {
                sb.append(Character.toLowerCase(curr));
            } else if (Character.isDigit(curr)) {
                sb.append(curr);
            }
        }
        
        char[] sArray = sb.toString().toCharArray();
        for (int i = 0; i < sArray.length / 2; i++) {
            if (sArray[i] != sArray[sArray.length - 1 - i]) {
                return false;
            }
        }
        
        return true;
    }
}

**_Not use extra space _**

class Solution {
    public boolean isPalindrome(String s) {
        int left = 0;
        int right = s.length() - 1;
        
        while (left < right) {
            
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }
            while(left < right && !Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }
            
            if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) {
               return false; 
            }
            left++;
            right--;
        }
        return true;
    }
}
