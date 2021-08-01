# Lintcode 462 · Total Occurrence of Target

# Lintcode **# 462 · Total Occurrence of Target**
**
**
**It is pretty similar to  34. the first and last position **
**
**
public class Solution {
    /**
     * @param A: A an integer array sorted in ascending order
     * @param target: An integer
     * @return: An integer
     */
    public int totalOccurrence(int[] A, int target) {
        int n = A.length;
        // write your code here
        if(A == null || A.length == 0) return 0;
        if(A[n - 1] < target || A[0] > target) return 0;
        int start = 0;
        int end = n - 1;
        int counter = 0;
        int firstPosition = findFirst(start, end, A, target);
        int lastPosition = findLast(start, end, A, target);
        if(firstPosition < 0 || lastPosition < 0) return 0;
        counter = lastPosition - firstPosition + 1;
        return counter;       
    }

    public int findFirst(int start, int end, int[] A, int target) {
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if(A[mid] == target || A[mid] > target) {
                end = mid;
            }else if (A[mid] < target) {
                start = mid;
            }
        }
        if(A[start] == target) return start;
        if(A[end] == target) return end;
        return -1;
    }

    public int findLast(int start, int end, int[] A, int target) {
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if(A[mid] == target || A[mid] < target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        if(A[end] == target) return end;
        if(A[start] == target) return start;
        return -1;
    }
}
