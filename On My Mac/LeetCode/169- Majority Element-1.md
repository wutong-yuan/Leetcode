# 169. Majority Element

**# 169. Majority Element**

**_Approach 1: Brute Force_**

public static int majorityElement(int[] nums) {

    for(int i = 0; i < nums.length; i++) {
        int count = 0;
        for(int j = 0; j < nums.length; j++) {
            if(nums[j] == nums[i]) {
                count++;
            }
            if(count > nums.length / 2) {
                return nums[i];
            }
        }
    }
    return -1;
}

![169- Majority Element-1](images/169- Majority%20Element-1.png)

We initialize the count within the for loop, meaning each time, when we iterate the array nums elements, we set count to zero. 
If we do it like the first screenshot above, the count will be added each time. After we finish the iteration for the first element, it will be added even on the second element. But each time, when we switch the array element, we want to count from zero again. 

![169- Majority Element-1-1](images/169- Majority%20Element-1-1.png)

**_Approach 2:_**

* n Hashmap(key-value pair), at value, maintain a count for each element(key) and whenever the count is greater than half of the array length, return that key(majority element).   
* **Algorithm:**
	1. Create a hashmap to store a key-value pair, i.e. element-frequency pair.
	2. Traverse the array from start to end.
	3. For every element in the array, insert the element in the hashmap if the element does not exist as key, else fetch the value of the key ( array[i] ), and increase the value by 1
	4. If the count is greater than half then print the majority element and break.
	5. If no majority element is found print “No Majority element”

![169- Majority Element-1-2](images/169- Majority%20Element-1-2.png)

public static int majorityElement(int[] nums) {

    Map<Integer, Integer> numsMap = new HashMap<>();

    if(nums.length == 1) {
        return nums[0];
    }

    for (int i = 0; i <nums.length; i++) {
        if(numsMap.containsKey(nums[i])) {
            int count = numsMap.get(nums[i]) + 1;
            if(count > nums.length / 2) {
                return nums[i];
            } else {
                numsMap.put(nums[i], count);
            }
        } else {
            numsMap.put(nums[i], 1);
        }
    }
    return -1;
}

**_Approach 3:  Sorting_**

![169- Majority Element-1-3](images/169- Majority%20Element-1-3.png)

**_Approach 4: Boyer-Moore Voting Algorithm _**

Algorithm
Step 1: Find the candidate for the majority element 
Step 2: Verify that whether the candidate is a majority element or not

Step 1:
Assume the first element is the majority element and the count is one
* Finding the candidate, as a start, we set the first element as the candidate in the beginning
* Use a count variable to store the counts 
* Compare the candidate to the next element. 
* If they are the same, increase the count by one
* If they are not the same, reduce the count by one
* Check if the count reaches 0, then set the candidate to the current element and the count to 1

Step 2:
* If the count is bigger than 2/n, then we find the one we want, we just return the value of this element
* Note: the count may not be the real count of this elements in this array. But it would be sufficient to show this is the one we  need. As long as it exists, use this algorithm will always get the element.
* Explanation: https://www.youtube.com/watch?v=n5QY3x_GNDg 

**_Two situations:_**

If it is possible that there may be no majority element in this array, we need to track the count of the majority element to see if count > length / 2. If yes, it is the majority. If not, there may be no majority element in this array, we will return -1 then.

public static int majorityElement(int[] nums) {
    int n = nums.length;
    int candidateIndex = 0;
    int countForCandidate = 1;
    int countForMajority = 0;

// we find the candidate element first
    for(int i = 1; i < n; i++) {
        if (nums[candidateIndex] == nums[i]) {
            countForCandidate++;
        } else {
            countForCandidate--;
        }
        if (countForCandidate == 0) {
            countForCandidate = 1;
            candidateIndex = i;
        }
    }

// Then we check the existence number to see if that is greater than length / 2
    for(int i = 0; i < n; i++) {
        if(nums[i] == nums[candidateIndex]) {
            countForMajority++;
        }
        if(countForMajority > n / 2) {
            return nums[candidateIndex];
        }
    }
    return -1;
}

**We can also split it into two methods:**
**First — find the candidate:**
public static int findCandidate (int[] nums) {
    int n = nums.length;
    int index = 0;
    int count = 1;
    for(int i = 1; i < n; i++) {
        if(nums[index] == nums[i]) {
            count++;
        } else {
            count--;
        }
        if(count == 0) {
            index = i;
            count = 1;
        }
    }
    return nums[index];
}

**Then we check the count to see if that is bigger than length / 2**
    int candidate = *findCandidate*(nums);
    int count = 0;
    for (int i = 0; i < nums.length; i++) {
        if(nums[i] == candidate) {
            count++;
        }
        if(count > nums.length / 2) {
            return candidate;
        }
    }
    return -1;
}

**Situation 2: if there must be a majority element in this array, we won’t care about the count. As long as we find the candidate number, we would just return it. **
class Solution {
    public int majorityElement(int[] nums) {
        int count = 0;
        Integer candidate = null;

        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            count += (num == candidate) ? 1 : -1; // see below of the breakdown of this statment
        }

        return candidate;
    }
}

**Breakdown:**
int count = 0;
Integer candidate = null;

for(int num : nums) {

    if(count == 0) {
        candidate = num;
    }

    if(num == candidate) {
        count = count + 1;
    } else {
        count = count - 1;
    }
}
return candidate;

