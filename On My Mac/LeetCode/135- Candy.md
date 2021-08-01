# 135. Candy

**# 135. Candy**

**_O(N) with O(N) two arrays_**

class Solution {
    public int candy(int[] ratings) {
        int n = ratings.length;
        int[] left = new int[n];
        int[] right = new int[n];
        
        left[0] = 1;
        // from left to right
        Arrays.fill(left, 1);
        Arrays.fill(right, 1);
        for (int i = 1; i < n; i++ ) {
            if (ratings[i] > ratings[i - 1]) {
                left[i] = left[i - 1] + 1;
            }
        } 
        
        right[n -1] = 1;
        for (int i = n - 2; i >= 0; i--) {
            if(ratings[i] > ratings[i + 1]) {
                right[i] = right[i + 1] + 1;
            }
        }
        
        int result = 0;
        for (int i = 0; i < n; i++) {
            result += Math.max(left[i], right[i]); 
        }
        
        return result;
    }
}

**_With one array _**
class Solution {
    public int candy(int[] ratings) {
        int n = ratings.length;
        int[] result = new int[n];
        
        // from left to right
        Arrays.fill(result, 1);
        for (int i = 1; i < n; i++ ) {
            if (ratings[i] > ratings[i - 1]) {
                result[i] = result[i - 1] + 1;
            }
        } 

        for (int i = n - 2; i >= 0; i--) {
            if(ratings[i] > ratings[i + 1]) {
                result[i] = Math.max(result[i], result[i + 1] + 1);
            }
        }
        
        int sum = 0;
        for (int i = 0; i < n; i++) {
            sum += result[i]; 
        }
        
        return sum;
    }
}

**_With O(1) space_**

class Solution {
    public int candy(int[] ratings) {
        int result = 1;
        int up = 0;
        int down = 0;
        int peak = 0;
        
        
        for (int i = 1; i < ratings.length; i++) {
            if (ratings[i] > ratings[ i - 1]) {
                up++;
                peak = up;
                down = 0;
                result += 1 + up;
            } else if (ratings[i] == ratings[i - 1]) {
                peak = 0;
                up = 0;
                down = 0;
                result++;
            } else {
                up = 0;
                down++;
                result += down;
                if (peak < down) {
                    result++;
                }
            }
        }
        
        return result;
    }
}

