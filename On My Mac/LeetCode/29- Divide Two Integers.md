# 29. Divide Two Integers

**29. Divide Two Integers**
**
**
**https://www.jiuzhang.com/problem/divide-two-integers/**** **
**
**
class Solution {
    public int divide(int dividend, int divisor) {
//         if (divisor == 0) {
//              return dividend >= 0? Integer.MAX_VALUE : Integer.MIN_VALUE;
//         }
        
//         if (dividend == 0) {
//             return 0;
//         }
**_        Above not necessary_**
**
**

        // In Java, the integer range is -2147483648 to 2147483647, which means, Integer.Min = -2147483648. If we do Integer.Min / -1, then we would get 2147483648 in math. However, integer in java can have max value of 2147483647.  2147483648 is bigger than the integer max value in java, this is integer overflow. So we need to separate this case.
        if (dividend == Integer.MIN_VALUE && divisor == -1) {
            return Integer.MAX_VALUE;
        }
        
        
        
        int a = Math.abs(dividend);
        int b = Math.abs(divisor);
        int result = 0;
        
        while ( a - b >= 0) {
            int temp = b;
            int count = 1;
            while (a - (temp << 1) >= 0) {
                temp <<= 1;
                count <<= 1;
            }
            a -= temp;
            result += count;
        }
        return (dividend > 0) == (divisor > 0) ? result : -result;    
    }
}
