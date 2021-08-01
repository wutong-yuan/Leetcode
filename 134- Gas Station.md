# 134. Gas Station

**# 134. Gas Station**

**_Brute force - n^2_**
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int n = gas.length;
        
        for (int i = 0; i <= n - 1; i++) {
            int pointer = i;
            int sum = 0;
            while (pointer <= 2 * n - 1) {
                if (pointer == i + n) return i;
                if(pointer > n - 1) {
                    sum += gas[pointer - n] - cost[pointer - n];
                } else {
                    sum += gas[pointer] - cost[pointer];  
                }
                
                if (sum >= 0) {
                    pointer++;
                } else {
                    break;
                }
            }
        }
        
       return - 1; 
        
    }
}

**_Greedy _**
**_
_**
**_See video _**
**_https://www.youtube.com/watch?v=lJwbPZGo05A_****_ _**
**_The reason it works because it is guaranteed that there is one solution _**
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int sumG = 0;
        int sumC = 0;
        for (int i = 0; i < gas.length; i++) {
            sumG += gas[i];
            sumC += cost[i];
        }
        if (sumG < sumC) return -1;
        
        int total = 0;
        int index = 0;
        for (int i = 0; i < gas.length; i++) {
            total += gas[i] - cost[i];
            
            if (total < 0) {
                total = 0;
                index = i + 1;
            }
        }
        
        return index;
    }
}
