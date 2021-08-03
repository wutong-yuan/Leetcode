# 189. Rotate Array

**# 189. Rotate Array**
# 

https://www.youtube.com/watch?v=BHr381Guz3Y 
**_Use extra space_**
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k = k % n;
        
        ArrayList<Integer> temp = new ArrayList<>();
        for (int i= 0; i < n; i++ ) {
            temp.add(nums[i]);   
        }
        
        for (int i = 0; i < n; i++) {
            nums[(i + k) % n] = temp.get(i);
        }
    }
}

**_Use reverse_**

class Solution {
    public void rotate(int[] nums, int k) {
        k %= nums.length;
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }
    
    public void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}

