# 123. Best Time to Buy and Sell Stock III

**# 123. Best Time to Buy and Sell Stock III**

**_Approach 1 _**
class Solution {
    public int maxProfit(int[] prices) {
        int length = prices.length;
        if (length <= 1) return 0;
        
        int leftMin = prices[0];
        int rightMax = prices[length - 1];
        
        int[] leftProfits = new int[length];
        int[] rightProfits = new int[length + 1];
        
        for (int l = 1; l < length; l++) {
            leftProfits[l] = Math.max(leftProfits[l - 1], prices[l] - leftMin);
            leftMin = Math.min(leftMin, prices[l]);
            
            int r = length - 1 - l;
            rightProfits[r] = Math.max(rightProfits[r + 1], rightMax - prices[r]);
            rightMax = Math.max(rightMax, prices[r]);
        }
        
        int maxProfit = 0;
        for (int i = 0; i < length; i++) {
            maxProfit = Math.max(maxProfit, leftProfits[i] + rightProfits[i + 1]);
        }
        return maxProfit;
    }
}

**_Approach 2 - one pass _**

class Solution {
    public int maxProfit(int[] prices) {
        int minCostSoFar = Integer.MAX_VALUE;
        int maxProfitSoFar = Integer.MIN_VALUE;
        
        int secondPurchaseCost = Integer.MAX_VALUE;
        int secondSoldProfit = Integer.MIN_VALUE;
        
        for (int price : prices) {
            minCostSoFar = Math.min(price, minCostSoFar);
            maxProfitSoFar = Math.max(maxProfitSoFar, price - minCostSoFar);
            
            secondPurchaseCost = Math.min(secondPurchaseCost, price - maxProfitSoFar);
            secondSoldProfit = Math.max(secondSoldProfit, price - secondPurchaseCost);           
        }        
        return secondSoldProfit;
    }
}
