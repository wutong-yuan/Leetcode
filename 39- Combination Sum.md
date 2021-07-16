# 39. Combination Sum

**39. Combination Sum**

First time:

class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(candidates);
        backtrack(result, new ArrayList<Integer>(), candidates, target, 0);
        return result;
    }
    
    public void backtrack(List<List<Integer>> result, List<Integer> temp, int[] candidates, int remain, int start ) {
        if(remain < 0) {
            return;
        } 
        if (remain == 0) {
            result.add(new ArrayList<>(temp));
        } else {
            for (int i = start; i < candidates.length** && i < remain**; i++) { // can speed up a little
                temp.add(candidates[i]);
                backtrack(result, temp, candidates, remain - candidates[i], i );
                temp.remove(temp.size() - 1);
            }
        }
    }
}

Second time:
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> combination = new ArrayList<>();      
        
        Arrays.sort(candidates);
        helper(candidates, target, result, combination, 0);    
        return result;
    }
    
    public void helper(int[] candidates, int target, List<List<Integer>> result, 
                       List<Integer> combination, int startIndex) {
        if (target == 0) {
            result.add(new ArrayList<>(combination));
            // return;
        }
        
        for (int i = startIndex; i < candidates.length; i++) {
**_            if(candidates[i] > target) break; // otherwise, it would cause stackoverflow_**
            
            combination.add(candidates[i]);
            helper(candidates, **target - candidates[i]**, result, combination, i);
            combination.remove(combination.size() - 1);
        }
    }
}
