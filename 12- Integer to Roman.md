# 12. Integer to Roman

**# 12. Integer to Roman**
# 

**_Approach 1:_**
class Solution {
    public int romanToInt(String s) {
        
        Map<String, Integer> map = new HashMap<>();
        map.put("M", 1000);
        map.put("CM", 900);
        map.put("D", 500);
        map.put("CD", 400);
        map.put("C", 100);
        map.put("XC", 90);
        map.put("L", 50);
        map.put("XL", 40);
        map.put("X", 10);
        map.put("IX", 9);
        map.put("V", 5);
        map.put("IV", 4);
        map.put("I", 1);

        
        
        int sum = 0;
        int i = 0;
        
        while (i < s.length() - 1) {
            String currentString = s.substring(i, i + 1);
            String nextString = s.substring(i + 1, i + 2);
            String two = s.substring(i, i + 2);

            int current = map.get(currentString);
            if (nextString != null) {
                
            }
            int next = map.get(nextString);

            int number = 0;
            if (current < next) {
                number = map.get(two);
                i += 2;
            } else {
                number = map.get(currentString);
                i++;
            }

            sum += number;
        }

        if (i < s.length()) {
            sum += map.get(s.substring(i));
        }
        return sum;
    }
}

**_Approach 2:_**
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
