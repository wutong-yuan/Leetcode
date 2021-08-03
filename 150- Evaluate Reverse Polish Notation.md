# 150. Evaluate Reverse Polish Notation

**# 150. Evaluate Reverse Polish Notation**

# 

**_Approach 1 - slower_**

class Solution {
    private static final Map<String, BiFunction<Integer, Integer, Integer>> OPERATIONS = new HashMap<>();
    static {
        OPERATIONS.put("+", (a, b) -> a + b);
        OPERATIONS.put("-", (a, b) -> a - b);
        OPERATIONS.put("*", (a, b) -> a * b);
        OPERATIONS.put("/", (a, b) -> a / b);

    }
    public int evalRPN(String[] tokens) {
        int length = tokens.length;
        int currentPosition = 0;
        
        while (length > 1) {
            while (!OPERATIONS.containsKey(tokens[currentPosition])) {
                currentPosition++;
            }  
            
            String operation = tokens[currentPosition];
            int number1 = Integer.parseInt(tokens[currentPosition - 2]);
            int number2 = Integer.parseInt(tokens[currentPosition - 1]);
            
            BiFunction<Integer, Integer, Integer> operator = OPERATIONS.get(operation);
            int result = operator.apply(number1, number2);
            tokens[currentPosition] = String.valueOf(result);
            delete2AtIndex(tokens, currentPosition - 2, length);
            currentPosition--;
            length -= 2;           
        }
        
        return Integer.parseInt(tokens[0]);
    }
    
    private void delete2AtIndex(String[] tokens, int index, int length) {
        for (int i = index; i < length - 2; i++) {
            tokens[i] = tokens[i + 2];
        }
    }
}

**_Approach 2 Use stack  - faster_**

class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stack = new Stack<>();
        int result = 0;
        
        for (String token : tokens) {
            if (!"+-*/".contains(token)) {
                stack.push(Integer.parseInt(token)); 
                continue;
            }
            String operator = token;
            int number2 = stack.pop();
            int number1 = stack.pop();
            
            if (token.equals("+")) {
                result = number1 + number2;       
            } else if (token.equals("-")) {
                result = number1 - number2;
            } else if (token.equals("*")) {
                result = number1 * number2;
            } else if (token.equals("/")) {
                result = number1 / number2;
            }
            
            stack.push(result);
        }
        
        return stack.pop();
    }
}

![150- Evaluate Reverse Polish Notation](images/150- Evaluate%20Reverse%20Polish%20Notation.png)

