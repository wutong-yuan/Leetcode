# 6. ZigZag Conversion

**# 6. ZigZag Conversion**
**
**
**https://www.youtube.com/watch?v=CPamjPdCvIk**** **

class Solution {
    public String convert(String s, int numRows) {
       int n = s.length();
        char[] sArray = s.toCharArray();
        
        StringBuilder[] sb = new StringBuilder[numRows];
        
        for (int i = 0; i < numRows ; i++) {
            sb[i] = new StringBuilder();
        }
        
        int index = 0;
        while (index < n) {
            for (int i = 0; i < numRows && index < n; i++) {
                sb[i].append(sArray[index]);
                index++;
            }
            
            for (int j = numRows - 2; j >= 1 && index < n; j--) {
                sb[j].append(sArray[index]);
                index++;
            }
        }
        
        for (int i = 1; i < numRows; i++) {
            sb[0].append(sb[i]);
        }
        
        return sb[0].toString();
    }
    
}

