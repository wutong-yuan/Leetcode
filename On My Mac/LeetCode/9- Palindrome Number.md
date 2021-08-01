# 9. Palindrome Number

**# 9. Palindrome Number**
# 

public boolean isPalindrome(int x) {
        if (x < 0) return false;
        if (x < 10) return true;
        
        int tempX = x;
        int reversedX = 0;
        
        while (tempX > 0) {
            int lastDigit = tempX % 10;
            reversedX = reversedX * 10 + lastDigit;
            tempX = tempX / 10;
        }
        
        if (reversedX == x) return true;
        return false;
    }
