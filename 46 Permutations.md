# 46 Permutations

# 46 **# Permutations**
**
**
**This approach runs faster but use extra space to store the freq**
**
**
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
**                freq[i] = false; —— be careful to add this back**
            }
        }
    }
}

This approach use the tempList itself, slower but not use extra space

class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> tempList = new ArrayList<>();

        backtrack(result, tempList, nums);
        return result;
    }
    
    public void backtrack(List<List<Integer>> list, List<Integer> tempList, int[] nums)  {
        if(tempList.size() == nums.length) {
            list.add(new ArrayList<>(tempList));
            return;
        } 
        
        for(int i = 0; i < nums.length; i++) {
            if(!tempList.contains(nums[i]) {
                tempList.add(nums[i]);
                backtrack(list, tempList, nums);
                tempList.remove(tempList.size() - 1);
            }
        }
    }
}
