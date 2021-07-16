# 30. Substring with Concatenation of All Words

**30. Substring with Concatenation of All Words**
**
**
**
**
**https://thecodingsimplified.com/find-substrings-formed-using-concatenation-of-all-given-words/**** **
**
**
class Solution {
    //input s = "barfoothefoobarman", words = ["foo","bar"]
    public List<Integer> findSubstring(String s, String[] words) {
        if (s == null || s.length() == 0 || words == null || words.length == 0) {
            return new ArrayList<>();
        }
        // create a hashmap to store the string in the words[] with its frequency
        Map<String, Integer> frequencyMap = new HashMap<>();
        // if the frequency map alreay contains the word, we will add one,
        // otherwise, we put it in the map with frequency 1
        for (String word : words) {
            frequencyMap.put(word, frequencyMap.getOrDefault(word, 0) + 1);
        }
        
        int eachWordLength = words[0].length();
        int totalWords = words.length;
        List<Integer> result = new ArrayList<>();
        // No need to go through the left the characters if the total length left 
        // is less than the total characters in the words. 
        // barfoothefoob"arman" --> no need to go through the "arman"
        // (less than 6 characters) because it
        // won't satify the target,which we need to include both "foo" and "bar"
        // 6 characters
        for (int i = 0; i <= s.length() - totalWords * eachWordLength; i++) {
            //add a counter to check if we have seen all the words in the 
            // target list
            int counter = 0;
            // create map to store the words that we have seen 
            Map<String, Integer> seenWords = new HashMap<>();
            //Go through each word one by one, two words in total
            for (int j = 0; j < totalWords; j++) {
                // eachWord has a length of 3. we check the string s by word
                int wordIndex = i + j * eachWordLength;
                // word = "bar" from the beginning, s.subString(0, 3)
                // inclusive 0 not 3
                String word = s.substring(wordIndex, wordIndex + eachWordLength);
                //if the current word we are seeing is not the target word,
                // just break out of this for loop of j and check the next i
                if (!frequencyMap.containsKey(word)) {
                    break;
                }
                // if the current word in the target word, we just add it to the 
                // seenMap
                seenWords.put(word, seenWords.getOrDefault(word, 0) + 1);
                counter++;
                // if the word we have seen is more than frequencyMap, 
                // like "barbarfoo....", we only need one bar, and one foo. So we 
                // will skip the first bar by breaking out of the j loop from here
                if(seenWords.get(word) > frequencyMap.getOrDefault(word, 0)) {
                    break;
                }
                
                if(counter == totalWords) {
                    result. add(i);
                }
            }
        }
        return result;
    }
}

class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        
        if (s.length() == 0 || s.length() < p.length() || p.length() == 0) {
            return new ArrayList<>();
        }
        
        Map<Character, Integer> targetMap = new HashMap<>();
        ArrayList<Integer> result = new ArrayList<>();
        int targetLength = p.length();
        int sLength = s.length();
        
        for (int i = 0; i < targetLength; i++) {
            char character = p.charAt(i);
            targetMap.put(character, targetMap.getOrDefault(character, 0) + 1); 
        }
        
        for(int j = 0; j < sLength - targetLength; j++) {
            Map<Character, Integer> seenMap = new HashMap<>();
            char charS = s.charAt(j);
        
            if(targetMap.containsKey(charS)) {
                seenMap.put(charS, seenMap.getOrDefault(charS, 0) + 1);
            }
            
            if(seenMap.keySet().equals(targetMap.keySet())) {
                result.add(j);
            }
            
        }
        return result;
    }
}

