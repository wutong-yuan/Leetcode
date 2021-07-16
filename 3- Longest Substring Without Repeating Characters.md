# 3. Longest Substring Without Repeating Characters

**3. Longest Substring Without Repeating Characters**

public static int lengthOfLongestSubstring(String s) {
    int[] chars = new int[128];

    int n = s.length();
    int right = 0;
    int left = 0;
    int res = 0;
    while ( right < n) {
        // represent the character at position right in the given string
        char r = s.charAt(right);
        // represent the occurrence of the character r. The default value
        // was 0 for all the elements in the array chars
        chars[r]++;
        // > 1 means that the right character appears more than once.

        while (chars[r] > 1) {
            // Then we need to reduce the occurrence of the left character
            // because we will move the left pointer to the next position
            // and start a new window
            char l = s.charAt(left);
            chars[l]--;
            // to contract the window by moving the left pointer to the right
            left++;
        }

        res = Math.*max*(res,right - left + 1);
        // keep expanding the window by moving the right pointer
        right++;
    }
    return res;
}

**Optimization of the above approach**

public static int lengthOfLongestSubstring(String s) {
    // The initial values are null for this array chars
    Integer[] chars = new Integer[128];

    int n = s.length();
    int right = 0;
    int left = 0;
    int res = 0;
    while ( right < n) {
        // represent the character at position right in the given string
        char r = s.charAt(right);
        // default value for the index is null per first line - initialization of the array
        Integer index = chars[r];
        // check if the character appears before. If it did, the index will be updated to the 
        // corresponding position number of the string per the statement below "chars[r] = right".
        //It represents the previous occurrence position of the index.
        // if the character appears again, and the index is between the left pointer and right pointer
        // we will move the left pointer to index + 1 position.
        if (index != null && index >= left && index < right) {
            left = index + 1;
        }
        res = Math.*max*(res,right - left + 1);
        // update the key of the r element, which is also the index, in the array to be the right position.
        chars[r] = right;
        // keep expanding the window by moving the right pointer
        right++;
    }
    return res;
}

![3- Longest Substring Without Repeating Characters](images/3- Longest%20Substring%20Without%20Repeating%20Characters.png)

