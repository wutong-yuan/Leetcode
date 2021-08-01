# 127. Word Ladder

**# 127. Word Ladder**

class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {

        int steps = 0;
        Set<String> dict = new HashSet<>();
        for (int i = 0; i < wordList.size(); i++) {
            dict.add(wordList.get(i));
        }

        Queue<String> queue = new LinkedList<>();
        Set<String> set = new HashSet<>();
        queue.offer(beginWord);
        set.add(beginWord);

        while (!queue.isEmpty()) {
            steps++;
            int size = queue.size();
            for (int j = 0; j < size; j++) {
                String currentWord = queue.poll();
                if(currentWord.equals(endWord)) {
                    return steps;
                }
                
                for (String nextWord : getNextWord(currentWord, dict)) {
                    if (!set.contains(nextWord)) {
                        queue.offer(nextWord);
                        set.add(nextWord);
                    }
                }
            }

        }

        return 0;
    }

    private ArrayList<String> getNextWord(String word1, Set<String> dict) {
        ArrayList<String> nextWordList = new ArrayList<>();
        
        for (int i = 0; i < word1.length(); i++) {
            for (char c = 'a'; c <= 'z'; c++) {
                if (c == word1.charAt(i)) continue;
                String newWord = replace(word1, c, i);
                if (dict.contains(newWord)) {
                    nextWordList.add(newWord);
                }
            }
        }   
        return nextWordList;
    }

    private String replace(String word, char c, int index) {
        char[] chars = word.toCharArray();
        chars[index] = c;
        return new String(chars);
    }
  
}
