# 60. Permutation Sequence

**60. Permutation Sequence**
**
**
**https://www.youtube.com/watch?v=wT7gcXLYoao&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=56**** **
**
**
class Solution {
    
    public String getPermutation(int n, int k) {
        int factorial = 1;
        ArrayList<Integer> numbers = new ArrayList<>();
        //Below is calculating (n-1)!
        for (int i = 1; i < n; i++) {
            factorial *= i;
            //Add 1, 2, 3 .... n-1 to numbers
            numbers.add(i);
        }
        //Add last number to numbers list
        numbers.add(n);
        
        String ans = "";
        // k=17 means 16th permutations
        k = k - 1;
        while (true) {
            ans += numbers.get(k / factorial);
            numbers.remove(k / factorial);
            if(numbers.size() == 0) {
                break;
            }
            k = k % factorial;
            // Get the (n - 1)! each time
            factorial = factorial / numbers.size();
        }
        return ans;
    }
}**
**
**
**
**
**
