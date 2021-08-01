# 59 · 3Sum Closest

**# 59 · 3Sum Closest**

## Be careful about the skipping code below. We skip when we meet the requirement.
## Compare with threeSum 

public class Solution {
    /**
     * @param numbers: Give an array numbers of n integer
     * @param target: An integer
     * @return: return the sum of the three integers, the sum closest target.
     */
    public int threeSumClosest(int[] numbers, int target) {
        // write your code here
        if (numbers == null || numbers.length < 3) return 0;
        Arrays.sort(numbers);

        int minSum = Integer.MAX_VALUE;
        int minDiff = Integer.MAX_VALUE;

        for (int i = 0; i < numbers.length; i++) {
**            if (i > 0 && numbers[i] == numbers[i - 1]) continue;**
            int left = i + 1;
            int right = numbers.length - 1;

            while (left < right) {
                int threeSum = numbers[left] + numbers[right] + numbers[i];
                if (threeSum == target) {
                    return threeSum;
                } else if (threeSum > target) {
                    right--;
                    **while (left < right && numbers[right] == numbers[right + 1]) {**
**                        right--;**

                    }
                } else {
                    left++;
                    **while (left < right && numbers[left] == numbers[left - 1]) {**
**                        left++;**

                    }
                }
                int tempDiff = Math.abs(threeSum - target);
                if (tempDiff < minDiff) {
                    minDiff = tempDiff;
                    minSum = threeSum;
                }
            }
        }
        return minSum;
    }
}
