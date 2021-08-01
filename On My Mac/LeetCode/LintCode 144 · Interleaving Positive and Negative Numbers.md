# LintCode 144 · Interleaving Positive and Negative Numbers

# LintCode **# 144 · Interleaving Positive and Negative Numbers**

先把正负数 partition 开，然后再相向双指针进行交换。

public class Solution {
    /*
     * @param A: An integer array.
     * @return: nothing
     */
    public void rerange(int[] A) {
        // write your code here
        int numOfPostive = 0;
        int numOfNegavtive = 0;
        for (int i = 0; i < A.length; i++) {
            if (A[i] > 0) {
                numOfPostive++;
            } else {
                numOfNegavtive++;
            }
        }
        
**// isPositiveGreater will be used to make sure the one with more elements are on the left side when we partition**
        boolean isPositiveGreater = (numOfPostive > numOfNegavtive);
**//isSameLength rely on our partition because we will start from index 1 not index 0 to do the swap. **
        boolean isSameLength = (numOfPostive == numOfNegavtive);

        partition(A, isPositiveGreater);
        interLeave(A, isSameLength);
    }

    private void partition(int[] A, boolean isPositiveGreater) {
        int flag = isPositiveGreater ? 1 : -1;
        int left = 0; 
        int right = A.length - 1;
        while (left <= right) {
**// within the boundary, if the positives numbers are greater and the current number is a positive, we keep moving this left pointer. **
**// if the negative numbers are greater and the current number is a negative, we keep moving this left pointer**

            while (left <= right && A[left] * flag > 0) {
                left++;
            }

            while (left <= right && A[right] * flag < 0) {
                right--;
            }

            if (left <= right) {
                int temp = A[left];
                A[left] = A[right];
                A[right] = temp;
                left++;
                right--;
            }
        }
    }
    private void interLeave(int[] A, boolean isSameLength) {

**// be careful here. We start from the second element**
        int left = 1;
        int right = A.length - 1;
        if (isSameLength) {
            right = A.length - 2;
        }
        while (left <= right) {
            int temp = A[left];
            A[left] = A[right];
            A[right] = temp;

            left += 2;
            right -= 2;
        }
    }
}
