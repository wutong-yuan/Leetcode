# 93. Restore IP Addresses

**# 93. Restore IP Addresses**
# 

class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> result = new ArrayList<>();
        int n = s.length();
        StringBuilder sb = new StringBuilder();
        for (int a = 1; a <= 3; a++)
            for (int b = 1; b <= 3; b++) 
                for (int c = 1; c <= 3; c++)
                    for (int d = 1; d <= 3; d++) {
                        if (a + b + c + d == n) {
                            int n1 = Integer.parseInt(s.substring(0, a));
                            int n2 = Integer.parseInt(s.substring(a, a + b));
                            int n3 = Integer.parseInt(s.substring(a + b, a + b + c));
                            int n4 = Integer.parseInt(s.substring(a + b + c));
                            if( n1 <= 255 && n2 <= 255 && n3 <= 255 && n4 <= 255) {
                                sb.append(n1).append('.').
                                    append(n2).append('.').
                                    append(n3).append('.').
                                    append(n4);
                                if (sb.length() == n + 3) result.add(sb.toString());
                                sb.delete(0, sb.length());
                            }
                        }
                    }
        return result;
    }
}
