# LintCode 382 · Triangle Count

**# LintCode 382 · Triangle Count**

Similar to twoSum, see paper notes for details 

My solution - easy to understand
**Take the last element as the target to see if there are any sum of the two elements before it are greater than it**
**Then move the target to the left**

public class Solution {
    /**
     * @param S: A list of integers
     * @return: An integer
     */
    public int triangleCount(int[] S) {
        // write your code here

        if (S == null || S.length < 3) return 0;
        Arrays.sort(S);

        int count = 0;
        for (int i = S.length - 1; i >=2; i--) {
            int left = 0;
            int right = i - 1;
**// no need to add the bold code because if left == I, then right = I -1, will fail the while loop**
            while (left < right** && left != i**) {
                int sum = S[left] + S[right];
                if (sum > S[i]) {
                    count += (right - left);
                    right--;
                } else {
                    left++;
                }
            }
        }
        return count;
    }
}

**Jiuzhang**
public class Solution {
    /**
     * @param S: A list of integers
     * @return: An integer
     */
    public int triangleCount(int[] S) {
        // write your code here
        if (S == null || S.length < 3) return -1;
        int count = 0;
        Arrays.sort(S);
        for (int i = 0; i < S.length; i++) {
            int left = 0; 
            int right = i - 1;
            while (left < right) {
                if (S[left] + S[right] > S[i]) {
                    count += right - left;
                    right--;
                } else {
                    left++;
                }
            }
        }
        return count;
    }
}

