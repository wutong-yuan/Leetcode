# 89. Gray Code

**# 89. Gray Code**
https://leetcode.wang/leetCode-89-Gray-Code.html 

class Solution {
    public List<Integer> grayCode(int n) {
        List<Integer> result = new ArrayList<>();
        result.add(0);
        for (int i = 0; i < n; i++) {
            int add = 1 << i;
            for (int j = result.size() - 1; j >= 0; j--) {
                result.add(result.get(j) + add);
            }
        }
        
        return result;
    }
}
![89- Gray Code](images/89- Gray%20Code.png)

![89- Gray Code-1](images/89- Gray%20Code-1.png)

![89- Gray Code-2](images/89- Gray%20Code-2.png)

