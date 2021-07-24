# 17. Letter Combinations of a Phone Number

**# 17. Letter Combinations of a Phone Number**

https://www.youtube.com/watch?v=0snEunUacZY 
**_DFS approach_**
class Solution {
    public List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<>();
        // be careful here. If digits is empty, the dfs function would return [""].
        // but per the request, we need to return []
        // so we do it here
        if (digits == null || digits.isEmpty()) return result;
        
        String[] map = {
            "",
            "",
            "abc",
            "def",
            "ghi",
            "jkl",
            "mno",
            "pqrs",
            "tuv",
            "wxyz"        
        };
        
        String current = "";
        dfs(digits, result, 0, current, map);  
        return result;
    } 
    
    private void dfs(String digits, List<String> result, int index, String current, String[] map) {
        //length equal means that we have appended all the needed characters. 
        // for example the digits is "23", when we have "ad", we need to return
        if (current.length() == digits.length()) {
            result.add(current);
            return;
        }
        // the current digit starts from the first digit in the digits --> 2
        int currDigit = Character.getNumericValue(digits.charAt(index));
        //for the current digit, we need to get its corresponding character list --> abc
        char[] currCharList = map[currDigit].toCharArray();
        // for a, we go deep to get the next character. index + 1 means go to the next number in digits
        // while we do this, we need to add the a to the current to become "a"
        // during the recursive call, we would get currentDigit -> 3, then get the "def"
        // after we append d to "a" (current + c) --> "ad" ---> return 
        // then add "e" to "a" --> "ae" return 
        // then add "f" to "a" --> "af" return 
        // for b, do the same thing
        for (char c : currCharList) {
            dfs (digits, result, index + 1, current + c, map);
        }
    }
}

**_Use linked list - BFS_**

class Solution {
    public List<String> letterCombinations(String digits) {
        LinkedList<String> result = new LinkedList<>();
        if (digits == null || digits.isEmpty()) {
            return result;
        }
        String[] mapping = new String[] {"0", "1", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};

        String current = "";
        result.add(current);
        
        for (int i = 0; i < digits.length(); i++) {
            int digit = Character.getNumericValue(digits.charAt(i));
            char[] charList = mapping[digit].toCharArray();
            
            while (i == result.peek().length()) {
                current = result.remove();
                for (char c : charList) {
                    result.add(current + c);
                }
            }
        }
        
        return result;
    }
}
