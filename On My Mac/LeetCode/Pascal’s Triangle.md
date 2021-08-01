# Pascal’s Triangle 

**_Key points:_**

Create triangle List first
Create rows —> triangle.add()
Create elements for each row ——> row.add()

When you add the element to an array, it adds at the end of the array

Code and explanation:

package com.yuanyuan;

import java.util.ArrayList;
import java.util.List;

public class Main {

**    public List<List<Integer>> generate(int numsRows) {**
        // create a object triangle, with a type of ArrayList. the elements
        // within this array list, this is a list of integers
**        List<List<Integer>> triangle = new ArrayList<List<Integer>> ();**

        // case 1: if the user request zero rows they get zero row
    **    if(numsRows == 0) {**
**            return triangle;**
**        }**

        // case 2: first row is always [1]
        // create a empty first row object first before we add elements to the first row array
        **triangle.add(new ArrayList<>());**

        // add one element [1] to the first array list because the first element is always 1
**        triangle.get(0).add(1);**

        // The first for loop, we create rows for this triangle. For the loop within this loop,
        // we create elements for each row
**        for(int rowNum = 1; rowNum < numsRows; rowNum++) {**
            // create the second (index is 1 but it is the second row) row object
            // with a type of Integer ArrayList.
**            List<Integer> row = new ArrayList<>();**
            // create a preRow object, and assign the value to it. if we start
            // from the first row, within this loop, the first preRow is
            // the first row, which is array [1]
**            List<Integer> preRow = triangle.get(rowNum - 1);**
            // add the first elements for the second row, which is the row (index is 1).
            // Right now, the array is empty. If we do add(), it would be the first element
            // in this array
         **   row.add(1);**
**            for (int j = 1; j < rowNum; j++) {**

                // each row, the element (other than the first and last of each row) is equal
                // to the sum of the elements above-and-to-the-left (index j-1) and
                // above-and-to-the-right (index j)
**                row.add(preRow.get(j-1) + preRow.get(j));**
            }
            // the add method --->Append the specified element to the end of this list
**            row.add(1);**

            **triangle.add(row);**
**        }**
**        return triangle;**
    }
}

![Pascal’s Triangle](images/Pascal’s%20Triangle.png)

