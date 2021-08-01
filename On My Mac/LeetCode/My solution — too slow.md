# My solution — too slow

# 

My solution — too slow

class WordDistance {
    String[] wordsDict;

    public WordDistance(String[] wordsDict) {
        this.wordsDict = wordsDict;
        
    }
    
    public int shortest(String word1, String word2) {
        int index1 = -1;
        int index2 = -1;
        int result = this.wordsDict.length;
        for (int i = 0; i < this.wordsDict.length; i++) {
            if (this.wordsDict[i].equals(word1)) {
                index1 = i;
            } else if (this.wordsDict[i].equals(word2)) {
                index2 = i;
            }
            
            if(index1 != -1 && index2 != -1) {
                result = Math.min(result, Math.abs(index1 - index2));
            }
        }
    return result;
    }
}

/**
 * Your WordDistance object will be instantiated and called as such:
 * WordDistance obj = new WordDistance(wordsDict);
 * int param_1 = obj.shortest(word1,word2);
 */

