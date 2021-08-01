# 46 Permutations

**46 Permutations**

class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        backtrack(result, new ArrayList<>(), nums, 0);
        return result;
    }
    
    
    public void backtrack(List<List<Integer>> list, ArrayList<Integer> tempList, int[] nums, int start) {
        if (tempList.size() == nums.length) {
            list.add(new ArrayList<>(tempList));
        } else {
             for(int i = 0; i < nums.length; i++) {
                if(tempList.contains(nums[i])) continue;
                tempList.add(nums[i]);
                backtrack(list, tempList, nums, i+1);
                tempList.remove(tempList.size() - 1);
            }
        }            
    }

**## Using extra space:**

class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> tempList = new ArrayList<>();
        boolean freq[] = new boolean[nums.length];
        backtrack(result, tempList, nums, freq);
        return result;
    }
    
    public void backtrack(List<List<Integer>> list, List<Integer> tempList, int[] nums, boolean[] freq)  {
        if(tempList.size() == nums.length) {
            list.add(new ArrayList<>(tempList));
            return;
        } 
        
        for(int i = 0; i < nums.length; i++) {
            if(!freq[i]) {
                tempList.add(nums[i]);
                freq[i] = true;
                backtrack(list, tempList, nums, freq);
                tempList.remove(tempList.size() - 1);
                freq[i] = false;
            }
        }
    }
}

## Optimization with no extra space:

class Solution {
    public List<List<Integer>> permute(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, nums, 0);
        return result;
    }
    
    public void backtrack(List<List<Integer>> result, 
                         int[] nums, int index) {
        if(index == nums.length) {
            ArrayList<Integer> tempList = new ArrayList<>();
            for (int i = 0; i < nums.length; i++) {
                tempList.add(nums[i]);
            }
            result.add(new ArrayList<>(tempList));
        }
        
        for (int j = index; j < nums.length; j++) {
            swap(index, j, nums);
            backtrack(result, nums, index + 1);
            swap(index, j, nums);
        }
    }
    
    public void swap(int i, int j, int[] nums) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    
}

    

