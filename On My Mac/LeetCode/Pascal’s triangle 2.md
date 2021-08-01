# Pascal’s triangle 2

Pascal’s triangle 2

![Pascal’s triangle 2](images/Pascal’s%20triangle%202.png)

**_Option 1 - _**we can get the Pascal’s triangle first and return the respective row. Be careful, the requirement is rowIndex-th row, meaning there will be rowIndex + 1 rows in total.
Row index starts from 0.

**_Option 2:_**
Algorithm 
Rule: for the value of each element in each row, 
value(rowIndex, columnIndex) = 
value(rowIndex -1, columnIndex - 1) + value(rowIndex - 1, columnIndex)

We can use recursive calls to implement this.

Recursion ends when:
First row is just [1];
First number of each row value(n,0) = 1
Last number of each row value(n, n) = 1, row = column

class Solution {
  private int getNum(int row, int col) {
    if (row == 0 || col == 0 || row == col) {
      return 1;
    }

    return getNum(row - 1, col - 1) + getNum(row - 1, col);
  }

  public List<Integer> getRow(int rowIndex) {
    List<Integer> ans = new ArrayList<>();

    for (int i = 0; i <= rowIndex; i++) {
      ans.add(getNum(rowIndex, i));
    }

    return ans;
  }
}

![Pascal’s triangle 2-1](images/Pascal’s%20triangle%202-1.png)

**_Option 3:_**
https://www.youtube.com/watch?v=tTYU4PAiqOE 
**_ _**
package com.yuanyuan;

import java.util.ArrayList;
import java.util.List;

public class Main {

    public List<Integer>  getRow(int rowIndex){
        List<Integer> row = new ArrayList<Integer>(rowIndex + 1);

        if(rowIndex < 0) {
            return row;
        }
        // add the first row. First row is always [1].
        row.add(1);
        // since we have already added the first row, we will
        // start from the second row, which has index of 1. We will 
        // override the first row to get the second row all the way
        // until we reach our goal. 
        for(int i = 1; i <= rowIndex; i++) {
            // Since the first and last element will always be 1, 
            // we already added the first element above. we won't change it.
            // We will add last one later via row.add(). So we only
            // need to override the middle ones. The total number of
            // elements in the middle would be previous row.size() -1. 
            // Previous means the row before we override. For example, 
            // if our target row is row6, row.size is size of row5. 
            // So j has a range of row.size() -1. In addition, we will 
            // start from the right and loop to the left.
            // See attached picture for reason

            for(int j = row.size() - 1; j > 0; j--) {
                // row[j]= row[j] + row[j-1]
                row.set(j, row.get(j) + row.get(j - 1));
            }
            // add the last element of the row
            row.add(1);
        }
        return row;
    }
}

**_Option 4: Math_**

![Pascal’s triangle 2-2](images/Pascal’s%20triangle%202-2.png)

![Pascal’s triangle 2-3](images/Pascal’s%20triangle%202-3.png)

    List<Integer> row = new ArrayList<>();
    row.add(1);
    for(int k = 1; k<= rowIndex; k++) {
        row.add((int) (row.get(k-1) * (long) (rowIndex - k + 1) / k));
    }
    return row;
}

