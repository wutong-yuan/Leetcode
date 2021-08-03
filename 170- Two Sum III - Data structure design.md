# 170. Two Sum III - Data structure design

**# 170. Two Sum III - Data structure design**

- **_Use array list _**

class TwoSum {
    ArrayList<Integer> list;

    /** Initialize your data structure here. */
    public TwoSum() {
       list = new ArrayList<Integer>();  
    }
    
    /** Add the number to an internal data structure.. */
    public void add(int number) {
        this.list.add(number);            
    }
    
    /** Find if there exists any pair of numbers which sum is equal to the value. */
    public boolean find(int value) {
        int i = 0;
        int j = list.size() - 1;
        int sum = 0;
        Collections.sort(list);
        while (i < j) {
            sum = list.get(i) + list.get(j);
            if (sum < value) {
                i++;    
            } else if (sum > value) {
                j--;
            } else {
                return true;
            }
        }
        
        return false;
    }
}

/**
 * Your TwoSum object will be instantiated and called as such:
 * TwoSum obj = new TwoSum();
 * obj.add(number);
 * boolean param_2 = obj.find(value);
 */

**_Use hashSet - faster_**

public class TwoSum {
    Map<Integer, Integer> map = new HashMap<>();
    /**
     * @param number: An integer
     * @return: nothing
     */
    public void add(int number) {
        // write your code here
        map.put(number, map.getOrDefault(number, 0) + 1);
    }

    /**
     * @param value: An integer
     * @return: Find if there exists any pair of numbers which sum is equal to the value.
     */
    public boolean find(int value) {
        // write your code here
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            int reminder = value - entry.getKey();
            if (map.containsKey(reminder)) {
                if (reminder == entry.getKey() && map.get(reminder) >= 2) {
                    return true;
                } else if (reminder != entry.getKey()) {
                    return true;
                }
            }
        }
        return false;
    }
}
