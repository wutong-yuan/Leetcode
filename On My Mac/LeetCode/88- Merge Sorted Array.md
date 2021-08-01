# 88. Merge Sorted Array

**# 88. Merge Sorted Array**

**Keep three pointers, p1 p2 and p**
**P1 = m -1**
**P2 = n -1**
**P = n + m -1**
**Then we start from the end and move forward**
**Compare p1 and p2, assign the bigger one to p position**

class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        //2, 2, 3, 0, 0, 0 
        //1, 3, 5
        
        int pointer1 = m - 1;
        int pointer2 = n - 1;
        int pointer = m + n - 1;
        while (pointer1 >= 0 && pointer2 >= 0) {
            if (nums1[pointer1] < nums2[pointer2]) {
                nums1[pointer] = nums2[pointer2];
                pointer2--;
                pointer--;
            } else {
                nums1[pointer] = nums1[pointer1];
                pointer--;
                pointer1--;
            }
        }
        if (pointer2 >= 0) {
            for (int i = 0; i <= pointer2; i++) {
                nums1[i] = nums2[i];
            }
        }
        
    }
}
