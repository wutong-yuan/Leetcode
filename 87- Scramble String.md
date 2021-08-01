# 87. Scramble String

**# 87. Scramble String**
https://www.youtube.com/watch?v=sETxfdHwxc0

class Solution {
    
    public boolean isScramble(String s1, String s2) {
        if (s1.length() != s2.length()) return false;
        Map<String, Boolean> map = new HashMap<>();
        return helper(s1, s2, map);
    }
    
    public boolean helper(String s1, String s2, Map<String, Boolean> map) {
        StringBuilder sb = new StringBuilder();
        sb.append(s1).append(s2);
        String key = sb.toString();
        if(map.containsKey(key)) {
            return map.get(key);
        }
        if (s1.equals(s2)) {
            map.put(key, true);
            return true;
        }
        
        int[] letters = new int[26];
        for (int i = 0; i < s1.length(); i++) {
            letters[s1.charAt(i) - 'a']++;
            letters[s2.charAt(i) - 'a']--;
        }
        
        for (int i = 0; i < 26; i++) {
            if (letters[i] != 0) return false;
        }
        
        for (int i = 1; i < s1.length(); i++) {
            if (helper(s1.substring(0, i), s2.substring(0, i), map) &&
               helper(s1.substring(i), s2.substring(i), map)) return true;
            if (helper(s1.substring(0, i), s2.substring(s2.length() - i), map) &&
               helper(s1.substring(i), s2.substring(0, s2.length() - i), map)) return true;
        }
        
        map.put(key, false);
        return false;
    }
    
}
