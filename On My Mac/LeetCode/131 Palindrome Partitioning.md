# 131 Palindrome Partitioning

# 131 **# Palindrome Partitioning**
**
**
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), s, 0);
        return result;
    }
    
    private void backtrack(List<List<String>> result, ArrayList<String> tempList, String s, int start) {
        if(start == s.length()) {
            result.add(new ArrayList<>(tempList));
            return;
        }
        for (int i = start; i < s.length(); i++) {
            if (isPalindrome(start, i, s)) {
                tempList.add(s.substring(start, i + 1)); 
                backtrack(result, tempList, s, i + 1);
                tempList.remove(tempList.size() - 1);
            }
        }
    }
    
    private boolean isPalindrome(int start, int end, String s) {
        while (start < end) {
            if(s.charAt(start++) != s.charAt(end--)) {
                return false;
            }
        }
        return true;
    }
}**
**
**
**
**Second time: from jiuzhang**
**
**
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> result = new ArrayList<>();
        List<String> subset = new ArrayList<>();
        helper(s, result, subset, 0);
        return result;
    }

    private void helper(String s, List<List<String>> result, List<String> subset, int startIndex ) {
        if (startIndex == s.length()) {
            result.add(new ArrayList<>(subset));
            return;
        }

        for (int i = startIndex; i < s.length(); i++) {
            String subString = s.substring(startIndex, i + 1);
            if (!isPalindrome(subString)) {
                continue;
            }
            subset.add(subString);
            helper(s, result, subset, i + 1);
            subset.remove(subset.size() - 1);
        }

    }

    private boolean isPalindrome(String s) {
        if (s == null || s.length() == 0) return false;
        int size = s.length();

        if (size == 1) return true;
        for (int i = 0; i <= size / 2 ; i++) {
            if (s.charAt(i) != s.charAt(size - 1 - i)) {
                return false;
            }
        }
        return true;
    }
}
