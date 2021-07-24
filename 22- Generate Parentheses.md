# 22. Generate Parentheses

**# 22. Generate Parentheses**# 

**https://www.youtube.com/watch?v=s9fokUqJ76A**** **
**
**
**
**
**
**
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        StringBuilder sb = new StringBuilder();
        sb.append("");
        dfs(result, n, 0, 0, sb);
        return result;
    }
    
    private void dfs(List<String> result, int n, int openCount, int closeCount, StringBuilder sb) {
        if (openCount == n && openCount == closeCount) {
            result.add(sb.toString());
        }
        
        if (openCount < n) {
            sb.append("(");
            dfs(result, n, openCount + 1, closeCount, sb);
            sb.setLength(sb.length() - 1);
        }
        
        if (closeCount < openCount) {
            sb.append(")");
            dfs(result, n, openCount, closeCount + 1, sb);
            sb.setLength(sb.length() - 1);
        }
    }
}

