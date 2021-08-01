# Use Arrays.sort

# 

**_Use Arrays.sort _**
class Solution {
    public int findKthLargest(int[] nums, int k) {
        Arrays.sort(nums);
        return nums[nums.length - k];
    }
}

**_Use quickSort_**
class Solution {
    public int findKthLargest(int[] nums, int k) {
        return quickSort(nums, 0, nums.length - 1, k);
    }
    
    private int quickSort(int[] nums, int start, int end, int k) {
        if (start <= end) {
            int p = partition(nums, start, end);
            if (p == nums.length - k) return nums[p];
            if (p > nums.length - k) {
                return quickSort(nums, start, p - 1, k);
            }
            if (p < nums.length - k) {
                return quickSort(nums, p + 1, end, k);
            }
        }
        return -1;
    }
    
    private int partition(int[] nums, int start, int end) {
        int pivot = end;
        int p = start;
        for (int i = start; i < end; i++) {
            if (nums[i] <= nums[pivot]) {
                swap(nums, i, p);
                p++;
            }
        }
        swap(nums, p, pivot);
        return p;
    }
    
    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}

**_Use heap _**
Adding a element into a heap cost O(logn) time.
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> queue = new PriorityQueue<>();
        
        for (int val : nums) {
            queue.offer(val);
            
            if (queue.size() > k) {
                queue.poll();
            }
        }
        return queue.poll();
    }
}

