# Two sum:

1. Two sum:

## Given an array of integers nums and an integer target, return *## indices of the two numbers such that they add up to target*## .
## You may assume that each input would have ***## exactly*****##  one solution**## , and you may not use the *## same*##  element twice.
## You can return the answer in any order.
##  
**## Example 1:**## 

**Input:** nums = [2,7,11,15], target = 9
**Output:** [0,1]
**Output:** Because nums[0] + nums[1] == 9, we return [0, 1].
**## Example 2:**## 

**Input:** nums = [3,2,4], target = 6
**Output:** [1,2]
**## Example 3:**## 

**Input:** nums = [3,3], target = 6
**Output:** [0,1]
##  
**## Constraints:**## 

* 2 <= nums.length <= 103
* -109 <= nums[i] <= 109
* -109 <= target <= 109
* **Only one valid answer exists.**

Accepted
3,725,197
Submissions
8,065,612

Mistab

![Two sum-](images/Two%20sum-.png)

Mistakes made:
![Two sum--1](images/Two%20sum--1.png)

![Two sum--2](images/Two%20sum--2.png)

![Two sum--3](images/Two%20sum--3.png)

![Two sum--4](images/Two%20sum--4.png)

**_The input length is >=2 per the problem description._**
**_Hence we can use the hashmap to store. _**
**_If the input is [3,3], it is OK_**

![Two sum--5](images/Two%20sum--5.png)

Two pass hash map

public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        map.put(nums[i], i);
    }
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement) && map.get(complement) != i) {
            return new int[] { i, map.get(complement) };
        }
    }
    throw new IllegalArgumentException("No two sum solution");
}

![Two sum--6](images/Two%20sum--6.png)

One pass Hash Map

public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[] { map.get(complement), i };
        }
        map.put(nums[i], i);
    }
    throw new IllegalArgumentException("No two sum solution");
}

![Two sum--7](images/Two%20sum--7.png)

