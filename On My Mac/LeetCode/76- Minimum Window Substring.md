# 76. Minimum Window Substring

# 

**76. Minimum Window Substring**
# 

# Algorithm

1. Use two pointers: start and end to represent a window.
2. Move end to find a valid window.
3. When a valid window is found, move start to find a smaller window.

public static String minWindow(String s, String t) {

    // input: s = "ADOBECODEBANC", t = "ABC"
    // Initialize a map array to store the characters in string t.
    // The default value for each element in this array is 0
    // the indexes of this array are those characters in t
    int[] map = new int[128];
    // For each character in the string t, count the occurrence
    for (char c : t.toCharArray()) {
        // appear once, we do ++, --> 1
        map[c]++;
    }
    int start = 0, end = 0, minStart = 0, minLen = Integer.*MAX_VALUE*, counter = t.length();
    // the outside while loop below is used to get the candidate window by expanding the right pointer,
    // which is the end pointer. once the candidate window was found, it will start to contract the window
    // by moving the start pointer to the right using the second loop.
    while (end < s.length()) {
        // end = 0, c1 = A (in string s)
        final char c1 = s.charAt(end);
        // if map contains c1, meaning target string t contains 'A'
        if (map[c1] > 0) {
            // counter decrease by 1 because we found 1 target character "A"
            counter--;
        }
        // decrease the occurrence of "A" in map array by 1
        map[c1]--;
        // move the right pointer by 1. Now the window is 0-1
        end++;
        // while the window contains all the target characters, we continue to contract it
        // by moving the left pointer to the right and update the minLen
        while (counter == 0) {
            if (minLen > end - start) {
                minLen = end - start;
                minStart = start;
            }
            // before we move the left pointer, increase the demand of this character. 
            // if this is the target character, since we need to move to the next character
            // we increase the demand by 1. Ad we reduce it by 1 when the right pointer passes, 
            // if the value in the map array is 0 or less meaning, the current window already has this character
            // no need to increase our counter. If the value is greater than 0, meaning we need to have this 
            // character in the window, we need to move the end pointer to the right until the counter equals to 
            // 3
            final char c2 = s.charAt(start);
            map[c2]++;
            if (map[c2] > 0) {
                counter++;
            }
            //move the start pointer to the right
            start++;
        }
    }
    return minLen == Integer.*MAX_VALUE *? "" : s.substring(minStart, minStart + minLen);
}

https://leetcode.com/problems/minimum-window-substring/discuss/26808/Here-is-a-10-line-template-that-can-solve-most-'substring'-problems 

**_# Template:_**
## For most substring problem, we are given a string and need to find a substring of it which satisfy some restrictions. A general way is to use a hashmap assisted with two pointers. The template is given below.
## 

int findSubstring(string s){
        vector<int> map(128,0);
        int counter; // check whether the substring is valid
        int begin=0, end=0; //two pointers, one point to tail and one  head
        int d; //the length of substring

        for() { /* initialize the hash map here */ }

        while(end<s.size()){

            if(map[s[end++]]-- ?){  /* modify counter here */ }

            while(/* counter condition */){ 
                 
                 /* update d here if finding minimum*/

                //increase begin to make it invalid/valid again
                
                if(map[s[begin++]]++ ?){ /*modify counter here*/ }
            }  

            /* update d here if finding maximum*/
        }
        return d;
  }

## Here is the java version based on templated code with optimisation (using array instead of map). The runtime dropped for e.g. in min window from 143ms -> 7ms.
## 

**## Minimum window**## 

## 

  public String minWindow(String s, String t) {
    int [] map = new int[128];
    for (char c : t.toCharArray()) {
      map[c]++;
    }
    int start = 0, end = 0, minStart = 0, minLen = Integer.MAX_VALUE, counter = t.length();
    while (end < s.length()) {
      final char c1 = s.charAt(end);
      if (map[c1] > 0) counter--;
      map[c1]--;
      end++;
      while (counter == 0) {
        if (minLen > end - start) {
          minLen = end - start;
          minStart = start;
        }
        final char c2 = s.charAt(start);
        map[c2]++;
        if (map[c2] > 0) counter++;
        start++;
      }
    }

    return minLen == Integer.MAX_VALUE ? "" : s.substring(minStart, minStart + minLen);
  }
## 

**## Longest Substring - at most K distinct characters**## 

## 

  public int lengthOfLongestSubstringKDistinct(String s, int k) {
    int[] map = new int[256];
    int start = 0, end = 0, maxLen = Integer.MIN_VALUE, counter = 0;

    while (end < s.length()) {
      final char c1 = s.charAt(end);
      if (map[c1] == 0) counter++;
      map[c1]++;
      end++;

      while (counter > k) {
        final char c2 = s.charAt(start);
        if (map[c2] == 1) counter--;
        map[c2]--;
        start++;
      }

      maxLen = Math.max(maxLen, end - start);
    }

    return maxLen;
  }
## 

**## Longest Substring - at most 2 distinct characters**## 

## 

public int lengthOfLongestSubstringTwoDistinct(String s) {
    int[] map = new int[128];
    int start = 0, end = 0, maxLen = 0, counter = 0;

    while (end < s.length()) {
      final char c1 = s.charAt(end);
      if (map[c1] == 0) counter++;
      map[c1]++;
      end++;

      while (counter > 2) {
        final char c2 = s.charAt(start);
        if (map[c2] == 1) counter--;
        map[c2]--;
        start++;
      }

      maxLen = Math.max(maxLen, end - start);
    }

    return maxLen;
  }
## 

**## LongestSubstring - without repeating characters**## 

## 

  public int lengthOfLongestSubstring2(String s) {
    int[] map = new int[128];
    int start = 0, end = 0, maxLen = 0, counter = 0;

    while (end < s.length()) {
      final char c1 = s.charAt(end);
      if (map[c1] > 0) counter++;
      map[c1]++;
      end++;

      while (counter > 0) {
        final char c2 = s.charAt(start);
        if (map[c2] > 1) counter--;
        map[c2]--;
        start++;
      }

      maxLen = Math.max(maxLen, end - start);
    }

    return maxLen;
  }

