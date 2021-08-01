# Buy and sell stock

![Buy and sell stock](images/Buy%20and%20sell%20stock.png)

![Buy and sell stock-1](images/Buy%20and%20sell%20stock-1.png)

package com.yuanyuan;

import java.util.ArrayList;
import java.util.List;

public class Main {

    public int maxProfit (int[] prices){
//        List<Integer> row = new ArrayList<Integer>(rowIndex + 1);
//
//        if(rowIndex < 0) {
//            return row;
//        }
//        // add the first row. First row is always [1].
//        row.add(1);
//        // since we have already added the first row, we will
//        // start from the second row, which has index of 1. We will
//        // override the first row to get the second row all the way
//        // until we reach our goal.
//        for(int i = 1; i <= rowIndex; i++) {
//            // Since the first and last element will always be 1,
//            // we already added the first element above. we won't change it.
//            // We will add last one later via row.add(). So we only
//            // need to override the middle ones. The total number of
//            // elements in the middle would be previous row.size() -1.
//            // Previous means the row before we override. For example,
//            // if our target row is row6, row.size is size of row5.
//            // So j has a range of row.size() -1. In addition, we will
//            // start from the right and loop to the left.
//            // See attached picture for reason
//
//            for(int j = row.size() - 1; j > 0; j--) {
//                // row[j]= row[j] + row[j-1]
//                row.set(j, row.get(j) + row.get(j - 1));
//            }
//            // add the last element of the row
//            row.add(1);
//        }
//        return row;
        int miniPrice = Integer.*MAX_VALUE*;
        int maxProfit = 0;

        for (int i = 0; i < prices.length - 1; i++) {
            if (prices[i] < miniPrice) {
                miniPrice = prices[i];
            } else if((prices[i] - miniPrice) > maxProfit) {
                maxProfit = prices[i] - miniPrice;
            }
        }
        return maxProfit;

    }
}

