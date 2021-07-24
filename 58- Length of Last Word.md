# 58. Length of Last Word

**# 58. Length of Last Word**
# 

https://www.youtube.com/watch?v=1vZswirL8Y8 
class Solution {
    public int lengthOfLastWord(String s) {
        if(s.equals(" ")) return 0;
        
        int length = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) != ' ') {
                length++;
                // we do the length > 0 because if length == 0 at this point, it means
                // the above length++ was not executed at all
                // this means, we are seeing consective " "s. 
                // we need to continue to move i to see if there is any character that is 
                // not " ". For example "a            ". In order to eliminate all the " "
                // we need to move i. 
                // if length > 0 means we started to count and see some non" " 
                // character already. we just return this last word length. 
            } else if (length > 0) {
                 return length;
            }
        }
        
        return length;
    }
}
