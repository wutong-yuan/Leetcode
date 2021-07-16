# 126 WordLadder  II

# 126 WordLadder **#  II**# 

class Solution {
    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        Set<String> dict = new HashSet<>();
        for (int i = 0; i < wordList.size(); i++) {
            dict.add(wordList.get(i));
        }
        
        List<List<String>> ladders = new ArrayList<>();
        Map<String, List<String>> map = new HashMap<>();
        Map<String, Integer> distance = new HashMap<>();
        
        dict.add(beginWord);
        dict.add(endWord);
        
        bfs(map, distance, endWord, beginWord, dict);
        
        List<String> path = new ArrayList<>();
        
        dfs(ladders, path, beginWord, endWord, distance, map);
        
        return ladders;
    }
    
    private void dfs (List<List<String>> ladders, List<String> path, String crt, String end, Map<String, Integer> distance, Map<String, List<String>> map) {
        path.add(crt);
        if (crt.equals(end)) {
            ladders.add(new ArrayList<String>(path));
        } else {
            for (String next : map.get(crt)) {
            if (distance.containsKey(next) && distance.get(crt) == distance.get(next) + 1) {
                    dfs(ladders, path, next, end, distance, map);
                }
            }
        }   
        path.remove(path.size() - 1);
    }
    
    private void bfs(Map<String, List<String>> map, Map<String, Integer> distance, String start, String end, Set<String> dict) {
        Queue<String> q = new LinkedList<String>();
        q.offer(start);
        distance.put(start, 0);
        for (String s : dict) {
            map.put(s, new ArrayList<String>());
        }
        
        while (!q.isEmpty()) {
            String crt = q.poll();
            
            List<String> nextList = expand(crt, dict);
            for (String next : nextList) {
                map.get(next).add(crt);
                if (!distance.containsKey(next)) {
                    distance.put(next, distance.get(crt) + 1);
                    q.offer(next);
                }
            }
        }
    }
    
    private List<String> expand(String crt, Set<String> dict) {
        List<String> expansion = new ArrayList<String>();
        
        for (int i = 0; i < crt.length(); i++) {
            for (char ch = 'a'; ch <= 'z'; ch++) {
                if (ch != crt.charAt(i)) {
                    String expanded = crt.substring(0, i) + ch + 
                        crt.substring(i + 1);
                    if (dict.contains(expanded)) {
                        expansion.add(expanded);
                    }
                }
            }
        }
        return expansion;
    }
}

class Solution {
    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        Set<String> dict = new HashSet<>();
        List<List<String>> result = new ArrayList<>();
        List<String> path = new ArrayList<>();
       
        
        for (int i = 0; i < wordList.size(); i++) {
            dict.add(wordList.get(i));
            depthMap.put(wordList.get(i), 0);
        }
        
         Map<String, List<String>> connectionMap = getConnection(beginWord, dict);
         Map<String, Integer> depthMap = new HashMap<>();
         
        
        int depth = bfs(beginWord, endWord, dict, depthMap, connectionMap);
        
        dfs(beginWord, depth, depthMap, connectionMap, result, path);
        
        
        
        
        return result;
    }
    
    private void dfs(String beginWord, int depth, Map<String, Integer> depthMap, Map<String, List<String>> connectionMap, List<List<String>> result, List<String> path) {
        if () {
            
        }
        
        path.add();
        dfs();
        path.remove();
        
    }
    
    private int bfs (String beginWord, String endWord, Set<String> dict, Map<String, Integer> depthMap, Map<String, List<String>> connectionMap) {
        Queue<String> queue = new LinkedList<>();
        Set<String> set = new HashSet<>();
        int depth = 0;
        
        queue.offer(beginWord);
        set.add(beginWord);
        
        while (!queue.isEmpty()) {
            depth++;
            String currentWord = queue.poll();
            int size = queue.size();
            
            for (int i = 0; i < size; i++) {
               for (String word : connectionMap) {
                   if (set.contains(word)){
                       continue;
                   }
                   queue.offer(word);
                   set.add(word);
                   depthMap.put(word, depth);
               }
            }
        }
        return depth;
    }
    
    private List<String> getConnection(String beginWord, Set<String> dict) {
        List<String> wordList = new ArrayList<>();
        char[] wordArray = beginWord.toCharArray();
        
        for (int i = 0; i < wordArray.length; i++) {
            for (char c = 'a'; c <'z'; c++) {
                if (c == wordArray[i]) continue;
                String newWord = getNewWord(wordArray, i, c);
                if (dict.contains(newWord)) {
                    wordList.add(newWord);
                }
            }
        }
        return wordList;
    }
    
    private String getNewWord(char[] wordArray, int index, char c) {
        char[] temp = wordArray;
        temp[index] = c;
        return temp.toString();      
    }
}
