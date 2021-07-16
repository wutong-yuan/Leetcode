# 49. Group Anagrams

**# 49. Group Anagrams**# 

public List<List<String>> groupAnagrams(String[] strs) {
    if (strs.length == 0) {
        return new ArrayList();
    }
    Map<String, List> ans = new HashMap<String, List>();
    // Iterate the string strs, for each element, create a char array to store
    // eat --> ca = { e, a, t}
    for (String s : strs) {
        char[] ca = s.toCharArray();
        // sort ca to {a, e, t}
        Arrays.*sort*(ca);
        // key ---> "aet"
        String key = String.*valueOf*(ca);
        // add the key to the answer map and create a new arraylist to store
        // the string element from the input
        if (!ans.containsKey(key)) {
            // key("aet"), value (empty array list)
            ans.put(key, new ArrayList());
        }
        // add the original string element "eat" to the empty array list create above
        ans.get(key).add(s);
    }
    // the map value method return a collection view of the values in the hashmap
    // Initial Mappings are: {20=Geeks, 25=Welcomes, 10=Geeks, 30=You, 15=4}
    // The collection is: [Geeks, Welcomes, Geeks, You, 4]
    // for this example, it would return ["are", "ear", "era"] for ans.values(). Then
    // add all the other values in this final Array List.
    // Finally it would return [["bat"],["nat","tan"],["ate","eat","tea"]].
    return new ArrayList(ans.values());
}

