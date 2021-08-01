# 140. Word Break II

**# 140. Word Break II**
# 

**_See paper notes for dry run examples_**

class Solution {
    private int maxLength = 0;
    public List<String> wordBreak(String s, List<String> wordDict) {
        Map<Integer, List<String>> map = new HashMap<>();
        Set<String> set = new HashSet<>();
        
        for (String word : wordDict) {
            set.add(word);
            maxLength = Math.max(maxLength, word.length());
        }
        
        return helper(s, set, 0, map);
    }
    
    private List<String> helper(String s, Set<String> set, int start, Map<Integer, List<String>> map) {
        List<String> list = new ArrayList<String>();
        
        if (start == s.length()) {
            list.add("");
        }
        
        if (map.containsKey(start)) {
            return map.get(start);
        }
        
        for (int i = start; i < s.length() && i - start + 1 <= maxLength; i++) {
            String subString = s.substring(start, i + 1);
            if (set.contains(subString)) {
                List<String> nextList = helper(s, set, i + 1, map);
                for (String next : nextList) {
                    // reach the end of s
                    if (next == "") {
                        list.add(subString + next);
                    }else {
                        list.add(subString + " " + next);
                    }
                }
            }
        }
        map.put(start, list);
        return list;
    }
}

![140- Word Break II](images/140- Word%20Break%20II.png)

