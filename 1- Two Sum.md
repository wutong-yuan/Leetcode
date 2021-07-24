# 1. Two Sum

**# 1. Two Sum**
**
**
**Use HashMap**
class Solution {
    public int[] twoSum(int[] nums, int target) {
        // map: <value, index>
        Map<Integer, Integer> map = new HashMap<>();
        
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[] { map.get(complement), i};
            }
            map.put(nums[i], i);
        }
        
        return null;
    
    }
}**
**
**
**

**_Use two pointers - a little complicated_**

class Pair {
    int val;
    int index;
    
    public Pair(int val, int index) {
        this.val = val;
        this.index = index;
    }
}
class Solution {
    
    private Comparator<Pair> pairComparator = new Comparator<>() {
       public int compare(Pair a, Pair b)  {
           return a.val - b.val;
       }
    };
    
    public int[] twoSum(int[] nums, int target) {
        Pair[] pair = sortPair(nums);
        int left = 0;
        int right = pair.length - 1;
        
        int[] result = new int[2];
        while (left <= right) {
            int sum = pair[left].val + pair[right].val;
            if ( sum < target) {
                left++;
            } else if (sum > target) {
                right--;
            } else {
                int leftIndex = pair[left].index;
                int rightIndex = pair[right].index;
                result[0] = leftIndex;
                result[1] = rightIndex;
               return result;
            }
        }
        return null;
    }
    
    private Pair[] sortPair(int[] nums) {
        Pair[] pair = new Pair[nums.length];
        for (int i = 0; i < nums.length; i++) {
            pair[i] = new Pair(nums[i], i);
        }
        Arrays.sort(pair, pairComparator);
        return pair;
    }
}
