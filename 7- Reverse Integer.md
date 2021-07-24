# 7. Reverse Integer

**# 7. Reverse Integer**

**_My solution - brute force_**
class Solution {
    public int reverse(int x) {
        if (x == Integer.MIN_VALUE || x == Integer.MAX_VALUE) return 0;
        
        boolean isPositive = x > 0;
        x = Math.abs(x);
        String s = String.valueOf(x);
        char[] sArray = s.toCharArray();
        StringBuilder sb = new StringBuilder();
        
        for (int i = sArray.length - 1; i >= 0; i--) {
            sb.append(sArray[i]);
        }
        
        String reversedS = sb.toString();
        long reversedX = Long.valueOf(reversedS);
        if (reversedX > Integer.MAX_VALUE) return 0;
        
        int reversedInt = Integer.valueOf(reversedS);
        
        if (isPositive) {
            return reversedInt;
        }
        return (-1) * reversedInt;
    }
}

![7- Reverse Integer](images/7- Reverse%20Integer.png)

