# 13. Roman to Integer

**# 13. Roman to Integer**

class Solution {
    public int romanToInt(String s) {
        Map<String, Integer> map = new HashMap<>();
        map.put("M", 1000);
        map.put("D", 500);
        map.put("C", 100);
        map.put("L", 50);
        map.put("X", 10);
        map.put("V", 5);
        map.put("I", 1);

        
        
        int sum = 0;
        int i = 0;
        
        while (i < s.length() - 1) {
            String current = s.substring(i, i + 1);
            String next = s.substring(i + 1, i + 2);
            
            int currentVal = map.get(current);
            int nextVal = map.get(next);
            if (currentVal < nextVal) {
                sum -= currentVal;
            } else {
                sum += currentVal;
            }
            i++;
        }
        
        if (i < s.length()) {
            sum += map.get(s.substring(i));
        }
        
        return sum;
    }
}
