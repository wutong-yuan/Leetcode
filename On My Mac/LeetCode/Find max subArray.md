# Find max subArray

Left = 1；
right= 1；
sum = A[1];
tempSum = 0;
tempLeft = 0;
For I=2 to A.length
     TempSum = MAX(A[i], tempSum + A[i])            
      If tempSum == A[I];    
 // because tempSum is the bigger one of A[I] and tempSum + A[I], if tempSum == A[I], this means that the sum of all the elements before i is less or equal to zero. This is the position we need to remember. The very left side.
            tempLeft = i;       // we set the left. 
      If temSum > sum   // we update the sum. If the temSum is bigger, this means the very right number we are checking now is positive, we will update the right side as well.  Because our goal is to make sure all the elements on the right side is negative or zero.
            sum = tempSum;  // we update the sum 
            right = i // we update the right side
            left = tempLeft;   // tempLeft only moves when tempSum == A[i], meaning the sum of the elements before i is less than or equal to zero
// if the temp sum is bigger, meaning the sum of the elements on the left is negative or equal to zero. 
Return (left, right, sum)

Notes:
The algorithm is to make sure the sum of the left side of the max SubArray is less than or equal to zero and the sum of the right side of the max subArray is less than or equal to zero. 
How?
For the left side, we are using tempSum to track. tempSum is the sum of all the elements on and before the current one in the beginning. If the current element A[i] is bigger than tempSum + A[I], this means the current element is positive and the sum of all the elements before it is less than zero or zero. Then we update tempSum to A[i] and move the left pointer to the current element. At the same time, we need to update the tempSum as well because from now on, we don’t care the elements before the current one any more. We will just move forward and do the same thing for the future element. Compare the updated tempSum with the tempSum + A[i]  for the upcoming element. 

tempSum = MAX(A[i], tempSum + A[i])  
tempLeft = i;   

But only if tempSum == A[I] doesn’t necessarily mean that temSum is the max subArray. For example, 2, 4, -6, 4. A[4] = 4, tempSum = 2+4-6+4=4. But 4 < 2+4 (the sum of the first two elements.) So before we move on, we need to check the tempSum with sum. The sum is the current max SubArray. The sum we start from the first element. If the second element is positive, tempSum will be temSum +A[2] = 0 +A[2]

For the right side, only if the tempSum > sum, which means, the current element is positive, we need to move the right pointer to the current element because this is the end of the current max subArray.

    public int maxSubArray(int[] nums) {
        int left = 0;
        int right = 0;
        int sum = nums[0];
        int tempSum = 0;
        int tempLeft = 0;

        for (int i = 0; i < nums.length; i++) {
            tempSum = Math.max(nums[i], tempSum + nums[i]);
            if (tempSum == nums[i]) {
                tempLeft = i;
            }
            if (tempSum > sum) {
                sum = tempSum;
                right = i;
                left = tempLeft;
            }
        }
        int max = 0;
        for (int i = left; i<= right; i++ ) {
            max += nums[i];
        }
        
        return max;
    }

https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/ 

 public static int findMaxSubArray(int[] array) {
    int maxSoFar = Integer.*MIN_VALUE*;
    int maxEndingHere = 0;
    for (int i = 0; I < array.length, i++）

        maxEndingHere = maxEndingHere + array[i];
        if (maxSoFar < maxEndingHere) {
            maxSoFar = maxEndingHere;
        }

        if(maxEndingHere < 0) {
            maxEndingHere = 0;
        }
    }

    return maxSoFar;
}

Example : {-1,- -2, -3}
maxEndingHere is used to track all the positive contiguous segments of the array. If the maxEndingHere is less than zero, we just set it to zero. We use maxSoFar to keep track the current max subArray. We set it to the minimum value of an integer. 
When i = 0, maxEndingHere = maxEndingHere + array[0] = 0 + (-1) = -1;
maxSoFar = Integer.MIN_VALUE < maxEndingHere (-1), maxSoFar = -1;
If maxEndingHere is less than Zero, this means, the sum of the current subarray is less than zero. Then we just send this to zero. At the same time, we use maxSoFar to track the real sum. 

The purpose of the maxEndingHere is just to check the subarray to see if this is positive or negative. If this is negative, then we don’t care. We only care when it is not negative. 

**_Further optimize: _**
 **int** max_so_far = array[0], max_ending_here = 0;  
  
    **for** (**int** i = 0; i < size; i++)  
    {  
        max_ending_here = max_ending_here + a[i]; 
        **if** (max_ending_here < 0)  
            max_ending_here = 0;  
          
        /* Do not compare for all elements. Compare only  when max_ending_here > 0.  */
        **else** **if** (max_so_far < max_ending_here)  
            max_so_far = max_ending_here;  
          
    }  
    **return** max_so_far;  

https://atekihcan.github.io/CLRS/E04.01-05/ 

