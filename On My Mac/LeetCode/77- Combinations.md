# 77. Combinations

**# 77. Combinations**

class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> tempList = new ArrayList<>();
        
        backtrack(result, tempList, 1, k, n);
        
        return result;
    }
    
    private void backtrack(List<List<Integer>> result, List<Integer> tempList, int start, int k, int n) {
        if (tempList.size() == k) {
            result.add(new ArrayList(tempList));
            return;
        }
        
        for (int i = start; i <= n; i++) {
            tempList.add(i);
            backtrack(result, tempList, i + 1, k, n);
            tempList.remove(tempList.size() - 1);
        }
    }
}
