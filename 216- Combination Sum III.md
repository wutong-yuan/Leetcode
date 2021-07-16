# 216. Combination Sum III

**216. Combination Sum III**
**
**
**https://leetcode.com/problems/combination-sum-iii/discuss/60614/Simple-and-clean-Java-code-backtracking****.**
**
**
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> ans = new ArrayList<>();
        combination(ans, new ArrayList<Integer>(), k, 1, n);
        return ans;
    }
    
    public void combination(List<List<Integer>> ans, List<Integer> combo, int k, int start, int n) {
        if(combo.size() > k) {
            return;
        }
        if(combo.size() == k && n == 0) {
            List<Integer> li = new ArrayList<Integer>(combo);
            ans.add(li);
            return;
        }
        for (int i = start; i <= n && i<= 9; i++) {
            combo.add(i);
            combination(ans, combo, k, i + 1, n - i);
            combo.remove(combo.size() - 1);
        }
    }
}**
**
**
**
