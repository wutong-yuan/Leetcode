# 71. Simplify Path

**# 71. Simplify Path**

 class Solution {
    public String simplifyPath(String path) {
        Stack<String> stack = new Stack<>();
        
        for (String current : path.split("/")) {
          **  if (current.equals("..")) {**
**                if(!stack.isEmpty()){**
**                    stack.pop();**
**                }**

            } else if (!current.equals("") && !current.equals(".")) {
                stack.push(current);
            }
        }
        
        
        if (stack.isEmpty()) return "/";
        
        StringBuilder sb = new StringBuilder();
        for (String dir :  stack) {
            sb.append("/");
            sb.append(dir);
        }
        return sb.toString();
    }
}

![71- Simplify Path](images/71- Simplify%20Path.png)

