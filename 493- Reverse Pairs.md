# 493. Reverse Pairs

**493. Reverse Pairs **

import java.util.ArrayList;

class Solution {

    public  int reversePairs(int[] nums) {
        return mergeSort(nums, 0, nums.length - 1);
    }
    public int mergeSort(int[] nums, int low, int high) {
        if (low >= high) return 0;

        int mid = low + (high - low) / 2;
        int inv = mergeSort(nums, low, mid);
        inv += mergeSort(nums, mid + 1, high);
        inv += merge(nums, low, mid, high);

        return inv;
    }
    public int merge(int[] nums, int low, int mid, int high) {
        int cnt = 0;
        int j = mid + 1;
        for (int i = low; i <= mid; i++) {
            while (j <= high && nums[i] > (2 * (long)nums[j])) {
                j++;
            }
            cnt += (j - (mid + 1));
        }
        int[] temp = new int[high - low + 1];
       for (int l = low, r = mid + 1, k = 0; l <= mid || r <= high;) {
           if (l <= mid && ((r > high) || nums[l] < nums[r])) {
               temp[k++] = nums[l++];
           } else {
               temp[k++] = nums[r++];
           }
        }
        for (int i = 0; i < temp.length; i++) {
            nums[low + i] = temp[i];
        }
        return cnt;
    }
}
