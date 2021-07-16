# 56. Merge Intervals

**56. Merge Intervals**
**
**
**https://www.youtube.com/watch?v=2JzRBPFYbKE&list=PLgUwDviBIf0rPG3Ictpu74YWBQ1CaBkm2&index=7**** **
**
**
**
**
Arrays.sort(arrayName, (a, b) -> Integer.compare(b[0],a[0])); //decreasing order
    
Arrays.sort(arrayName, (a, b) -> Integer.compare(a[0],b[0]); //increasing order

class Solution {
    public int[][] merge(int[][] intervals) {
        List<int[]> res = new ArrayList<>();
        Arrays.sort(intervals, (a , b) -> a[0] - b[0]);
        
        int start = intervals[0][0];
        int end = intervals[0][1];
        
        for (int[] i : intervals) {
            // first interation, i[0] = 1 end = 3 and end will be the same as i[1] 
            // after that, end will be the second element in the previous group
            // and i[0] will be the first element in the second group
            // if i[0] <= end, means overlap. Need to update the end, keep start as is
            if(i[0] <= end) {
                end = Math.max(end, i[1]);
            } else {
                // no overlap, add this pair to the final result
                res.add(new int[] {start, end});
                // move the start and end pointer to the current group, which has no overlap
                // with previous one
                start = i[0];
                end = i[1];
            }
        }
        res.add(new int[] {start, end});
**        return res.toArray(new int[0][]); // reason for this modification is that on the top we are returning in[][] on this method. If we change this to List<int[], we can just return res as below.**
    }
}

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {
    public static void main(String[] args) {
        int[][] intervals = {{1,3}, {2,6}, {8,10}, {15, 18}};
        List<int[]> result = *merge*(intervals);
        for(int i = 0; i < result.size(); i++) {
            System.*out*.println(Arrays.*toString*(result.get(i)));
        }
    }
    public static List<int[]> merge(int[][] intervals) {
        List<int[]> res = new ArrayList<>();

        // if(intervals.length == 0 || intervals == null) {
        //     return res.toArray(new int[0][]);
        // }

        Arrays.*sort*(intervals, (a, b) -> a[0] - b[0] );

        int start = intervals[0][0];
        int end = intervals[0][1];

        for (int[] i : intervals) {
            if(i[0] <= end) {
                end = Math.*max*(end, i[1]);
            } else {
                res.add(new int[] {start, end});
                start = i[0];
                end = i[1];
            }
        }
        res.add(new int[] {start, end});
        return res;
    }
}

