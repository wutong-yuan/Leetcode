# 40 Combination sum 2

Second time code:
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> combination = new ArrayList<>();
        
        helper(candidates, target, result, combination, 0);
        return result;
    }
    
    private void helper(int[] candidates, int target, List<List<Integer>> result, List<Integer> combination, int startIndex) {
        if (target == 0) {
            result.add(new ArrayList<>(combination));
        }
        for (int i = startIndex; i < candidates.length; i++) {
            // need to skip duplicates
            if (i >= 1 && candidates[i] == candidates[i - 1] && i > startIndex) {
                continue;
            }
            
            if(candidates[i] > target) {
                break;
            }
            
            combination.add(candidates[i]);
            helper(candidates, target - candidates[i], result, combination, i + 1);
            combination.remove(combination.size() - 1);
        }
    }
}

https://www.youtube.com/watch?v=G1fRTGRxXU8  - this video contains the explanation for the duplicate check and the regular way to draw a recursion tree for an array

public List<List<Integer>> combinationSum2(int[] candidates, int target) {
   List<List<Integer>> list = new LinkedList<List<Integer>>();
   Arrays.sort(candidates);
   backtrack(list, new ArrayList<Integer>(), candidates, target, 0);
   return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int[] cand, int remain, int start) {
   
   if(remain < 0) return; /** no solution */
   else if(remain == 0) list.add(new ArrayList<>(tempList));
   else{
      for (int i = start; i < cand.length; i++) {
         if(i > start && cand[i] == cand[i-1]) continue; /** skip duplicates */
         tempList.add(cand[i]);
         backtrack(list, tempList, cand, remain - cand[i], i+1);
         tempList.remove(tempList.size() - 1);
      }
   }
}

i > start: before explaining this, first recall what start is? Start points to the index which we start with in the first place before entering the for loop. It is the starting value from which we started picking up numbers. Since it's the starting point, so we will definitely take this number. i indicates the index which we are currently processing. Mind that in one recursive call stack the value of cur is not going to change but the value of i will keep on changing. If this is clear, then i > cur is simple to understand, it means that we are currently considering a position which is greater than cur. 

i>curr means position curr has been processed and we have found all the combinations starting from position curr by doing dfs. Therefore if cand[curr+1]==cand[curr] there is no need to process position curr+1 as it will provide combinations which have already been found by dfs from position curr hence we skip the step to avoid duplicate combinations. —> it is the depth

Now, consider the second condition cand[i] == cand[i - 1], we are considering an index which is greater then cur because that must be true if we are checking this condition, meaning we have already taken the number which is at cur, so if the number after cur has the same value, then we won't consider it again because that will be duplication. And that explains the condition.

I tried my best to explain it, hope it helps.

class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, new ArrayList<Integer>(), candidates, target, 0);
        return result;
    }
    
    private void backtrack(List<List<Integer>> result, ArrayList<Integer> tempList, int[] candidates, int remain, int start) {
        if(remain < 0) return;
        if(remain == 0) {
            result.add(new ArrayList<>(tempList));
            return;
        }
        for (int i = start; i < candidates.length; i++ ) {
            if(i > start && candidates[i] == candidates[i - 1]) {
                continue;
            }
            tempList.add(candidates[i]);
            backtrack(result, tempList, candidates, remain - candidates[i], i + 1);
            tempList.remove(tempList.size() - 1);
        }

    }
}
