# 20. Valid Parentheses

**# 20. Valid Parentheses**

# 

class Solution {
    public boolean isValid(String s) {
       Stack<Character> stack = new Stack<>();
        
        for (char c : s.toCharArray()) {
            if (c == '{') {
                stack.push('}');
            } else if (c == '[') {
                stack.push(']');
            } else if (c == '(') {
                stack.push(')');
            } else if (stack.isEmpty() || stack.pop() != c) {
                return false;
            }
        }
        
        return stack.isEmpty();
    }
}

![20- Valid Parentheses](images/20- Valid%20Parentheses.png)

