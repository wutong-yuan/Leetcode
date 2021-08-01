# 8. String to Integer (atoi)

**# 8. String to Integer (atoi)**# 

class Solution {
    public int myAtoi(String s) {
        int n = s.length();
        if ( n == 0) return 0;
        int indexPointer = 0;
        
        // step 1: check all white spaces and move the pointer to pass all white spaces
        while (indexPointer < n && s.charAt(indexPointer) == ' ') {
            indexPointer++;
        }
        
        // step 2: before we check the positive or negavtive sign, we need to make sure 
        // after the process of step 1, the substring still valid
        // if the input string is "           ", then the following code would have an 
        // out of bound error if we don't check the length 
        int sign = 1;
        if (indexPointer < n) {
            if (s.charAt(indexPointer) == '+') {
                indexPointer++;
            } else if (s.charAt(indexPointer) == '-') {
                sign = -1;
                indexPointer++;
            }
        }
        
        // step 3: get the digits
        int total = 0;
        while (indexPointer < n && Character.isDigit(s.charAt(indexPointer))) {
            int digit = s.charAt(indexPointer) - '0';
            
            if (Integer.MAX_VALUE / 10 < total ||
               (Integer.MAX_VALUE / 10 == total && Integer.MAX_VALUE % 10 < digit)) {
                return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
            }
            
            total = total * 10 + digit;
            indexPointer++;
        }
        
        return total * sign;
    }
}
