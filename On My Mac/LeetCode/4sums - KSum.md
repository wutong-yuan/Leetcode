# 4sums - KSum
https://leetcode.com/problems/4sum/discuss/8609/My-solution-generalized-for-kSums-in-JAVA

If you have already read and implement the 3sum and 4sum by using the sorting approach: reduce them into 2sum at the end, you might already got the feeling that, all ksum problem can be divided into two problems:

1. 2sum Problem
2. Reduce K sum problem to K – 1 sum Problem

Therefore, the ideas is simple and straightforward. We could use recursive to solve this problem. Time complexity is O(N^(K-1)).

public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        return kSum(nums, 0, 4, target);
    }
    private List<List<Integer>> kSum (int[] nums, int start, int k, int target) {
        int len = nums.length;
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if(k == 2) { //two pointers from left and right
            int left = start, right = len - 1;
            while(left < right) {
                int sum = nums[left] + nums[right];
                if(sum == target) {
                    List<Integer> path = new ArrayList<Integer>();
                    path.add(nums[left]);
                    path.add(nums[right]);
                    res.add(path);
                    while(left < right && nums[left] == nums[left + 1]) left++;
                    while(left < right && nums[right] == nums[right - 1]) right--;
                    left++;
                    right--;
                } else if (sum < target) { //move left
                    left++;
                } else { //move right
                    right--;
                }
            }
        } else {
            for(int i = start; i < len - (k - 1); i++) {
                if(i > start && nums[i] == nums[i - 1]) continue;
                List<List<Integer>> temp = kSum(nums, i + 1, k - 1, target - nums[i]);
                for(List<Integer> t : temp) {
                   t.add(0, nums[i]);
                }                    
                res.addAll(temp);
            }
        }
        return res;
    }

![4sums - KSum](images/4sums%20-%20KSum.png)

**Summarized solution **
**https://www.youtube.com/watch?v=-vu9GpZfqLY&t=618s**** **
**
**
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        return KSumRecursion(nums, 0, 3, 0);           
    }
    
    public List<List<Integer>> KSumRecursion(int[] nums, int index, int k, int target) {
        if(k == 2) {
            return twoSum(nums, index, nums.length - 1, target);
        }
        
        ArrayList<List<Integer>> resultList = new ArrayList<List<Integer>>();
        for (int i = index; i < nums.length - k + 1; i++) {
            List<List<Integer>> tempList = KSumRecursion(nums, i + 1, k - 1, target - nums[i]);
            if(tempList != null && tempList.size() > 0) {
                for (List<Integer> list : tempList) {
                list.add(0, nums[i]);
                }
                resultList.addAll(tempList);
            }
            while (i < nums.length - k + 1 && nums[i] == nums[i + 1]) {
                i++;
            }
        }
        return resultList;      
    }
    
    public List<List<Integer>> twoSum(int[] nums, int left, int right, int target) {
        ArrayList<List<Integer>> resultList = new ArrayList<>();
        while(left < right) {
            int sum = nums[left] + nums[right];
            if(sum < target) {
                left++;
            } else if (sum > target) {
                right--;
            } else {
                ArrayList<Integer> tempList = new ArrayList<>();
                tempList.add(nums[left]);
                tempList.add(nums[right]);
                resultList.add(tempList);
                while(left < right && nums[left] == nums[left + 1]) {
                    left++;
                }
                while(left < right && nums[right] == nums[right - 1]) {
                    right--;
                }
                
                left++;
                right--;
            }
        }
        return resultList;
    }
}

## Concise and beats 100%:
## 

public List<List<Integer>> fourSum(int[] nums, int target) {
    List<List<Integer>> result = new ArrayList<>();
    Arrays.sort(nums);
    kSum(result, new ArrayList<>(), nums, 0, target, 4);
    return result;
}

// General kSum solution. Assumes that k >= 2 and that nums is sorted.
private void kSum(List<List<Integer>> result, List<Integer> tuple, int[] nums, int start, int target, int k) {
**    // Not enough elements or **
**    // elements are guaranteed to sum up to > target (choose min element k times is already too much) or**
**    // elements are guaranteed to sum up to < target (even choosing the max element k times is too little).**
**    if (nums == null || start + k > nums.length || nums[start] * k > target || nums[nums.length - 1] * k < target) return;   **
**    **

    // Base case is 2sum.
    if (k == 2) {
        int l = start, r = nums.length - 1;
        while (l < r) {
            int sum = nums[l] + nums[r];
            if (sum < target) {
                l++;
            } else if (sum > target) {
                r--;
            } else {
                assert (sum == target);
                List<Integer> temp = new ArrayList<>(tuple);
                temp.add(nums[l]); temp.add(nums[r]);
                result.add(temp);
                
                l++;
                while (l < r && nums[l - 1] == nums[l]) l++;    // Skip duplicates.
            }
        }
    } else {
        for (int i = start; i < nums.length; ++i) {
            if (i > start && nums[i - 1] == nums[i]) continue;   // Skip duplicates.
            tuple.add(nums[i]);
            kSum(result, tuple, nums, i + 1, target - nums[i], k - 1);
            tuple.remove(tuple.size() - 1);  // Backtrack.
        }
    }
}

Variances:

**16. 3Sum Closest**
**259. 3Sum Smaller**
**My solution**
class Solution {
    public int threeSumSmaller(int[] nums, int target) {
        Arrays.sort(nums);
        int counter = 0;
        for (int i = 0; i < nums.length - 3 + 1; i++) {
            int left = i + 1;
            int right = nums.length - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum < target) {
                    counter += right - left;
                    left++;
                } else {
                    right--;
                }
            }  
        }
        return counter;
    }
}**
**

class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    Arrays.sort(nums);
    kSum(result, new ArrayList<>(), nums, 0, 0, 3);
    return result;
}

// General kSum solution. Assumes that k >= 2 and that nums is sorted.
private void kSum(List<List<Integer>> result, List<Integer> tuple, int[] nums, int start, int target, int k) {
    // Not enough elements or 
    // elements are guaranteed to sum up to > target (choose min element k times is already too much) or
    // elements are guaranteed to sum up to < target (even choosing the max element k times is too little).
    if (nums == null || start + k > nums.length || nums[start] * k > target || nums[nums.length - 1] * k < target) return;   
    
    // Base case is 2sum.
    if (k == 2) {
        int l = start, r = nums.length - 1;
        while (l < r) {
            int sum = nums[l] + nums[r];
            if (sum < target) {
                l++;
            } else if (sum > target) {
                r--;
            } else {
                assert (sum == target);
                List<Integer> temp = new ArrayList<>(tuple);
                temp.add(nums[l]); temp.add(nums[r]);
                result.add(temp);
                
                l++;
                while (l < r && nums[l - 1] == nums[l]) l++;    // Skip duplicates.
            }
        }
    } else {
        for (int i = start; i < nums.length; ++i) {
            if (i > start && nums[i - 1] == nums[i]) continue;   // Skip duplicates.
            tuple.add(nums[i]);
            kSum(result, tuple, nums, i + 1, target - nums[i], k - 1);
            tuple.remove(tuple.size() - 1);  // Backtrack.
        }
    }
}
}

## Non-sort solution 
![4sums - KSum-1](images/4sums%20-%20KSum-1.png)

![4sums - KSum-2](images/4sums%20-%20KSum-2.png)

