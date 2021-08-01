# Buy and sell stock 2

https://www.youtube.com/watch?v=Q-8JkdUliVM&feature=emb_logo 

class Solution {
    public int maxProfit(int[] prices) {
        
        int profit = 0;
        
        for(int i = 1; i< prices.length; i++) {
            if(prices[i] > prices[i-1]) {
                profit += prices[i] - prices[i-1];
            } 
        }
         return profit;
    }
}

