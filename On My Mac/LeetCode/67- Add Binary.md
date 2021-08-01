# 67. Add Binary

**# 67. Add Binary**

# 

**_Simplified solution: - same idea less code_**
class Solution {
    public String addBinary(String a, String b) {
        StringBuilder sb = new StringBuilder();
        
        int pointerA = a.length() - 1;
        int pointerB = b.length() - 1;
        
        int sum = 0;
        int carry = 0;
        while (pointerA >= 0 || pointerB >= 0) {
            sum = 0;
            sum += carry;
            if (pointerA >= 0) sum += Character.getNumericValue(a.charAt(pointerA));
            if (pointerB >= 0) sum += Character.getNumericValue(b.charAt(pointerB));
            sb.insert(0, sum % 2);
            carry = sum / 2;
            pointerA--;
            pointerB--;
        }
        
        if (carry == 1) sb.insert(0, '1');
        
        return sb.toString();
    }
}

**_My solution :_**

class Solution {
    public String addBinary(String a, String b) {

        StringBuilder sb = new StringBuilder();
        int aLen = a.length();
        int bLen = b.length();
        int pA = aLen - 1;
        int pB = bLen - 1;
        
        int carry = 0;
        int sum = 0;
        while (pA >= 0 || pB >= 0) {
            if (pA < 0) {
                sum = Character.getNumericValue(b.charAt(pB)) + carry;
            } else if (pB < 0) {
                sum = Character.getNumericValue(a.charAt(pA)) + carry;
            } else {
                int digitA = Character.getNumericValue(a.charAt(pA));
                int digitB = Character.getNumericValue(b.charAt(pB));
                sum = digitA + digitB + carry;
            }
                       
            if (sum == 0) {
                sb.insert(0, '0');
                carry = 0;
            } else if (sum == 1) {
                sb.insert(0, '1');
                carry = 0;
            } else if (sum == 2) {
                sb.insert(0, '0');
                carry = 1;
            } else if (sum == 3) {
                sb.insert(0, '1');
                carry = 1;
            }
            pA--;
            pB--;  
            }       
        
        if (carry == 1) {
            sb.insert(0, '1');
        }
        
        return sb.toString();
    }
}
