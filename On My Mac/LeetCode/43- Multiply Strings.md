# 43. Multiply Strings

**# 43. Multiply Strings**

# 

class Solution {
    public String multiply(String num1, String num2) {
        if (num1.equals("0")|| num2.equals("0")) {
           return "0"; 
        }
        int n1 = num1.length();
        int n2 = num2.length();
        
        int[] resultArray = new int[n1 + n2];
        
        for (int i = num1.length() - 1; i >= 0; i--) {
            for (int j = num2.length() - 1; j >= 0; j--) {
                int digit1 = Character.getNumericValue(num1.charAt(i));
                int digit2 = Character.getNumericValue(num2.charAt(j));
                int multiply = digit1 * digit2;
    
                int p1 = i + j;
                int p2 = i + j + 1;
                
         **       int sum = multiply + resultArray[p2];**
**                resultArray[p1] += sum / 10;**
**                resultArray[p2] = sum % 10;    **           
            }
        }
        
        StringBuilder sb = new StringBuilder();
        int index = 0;
        while (index < resultArray.length) {
            if (resultArray[index] == 0) index++;
            break;
        }
        
        for (int i = index; i < resultArray.length; i++) {
            sb.append(resultArray[i]);
        }
        if (sb.length() == 0) return "0";
        return sb.toString();
    }
}
