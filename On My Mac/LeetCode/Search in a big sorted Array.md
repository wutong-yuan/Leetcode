# Search in a big sorted Array

# 

Search in a big sorted Array

https://www.jiuzhang.com/solutions/search-in-a-big-sorted-array/ 

**## 描述**
中文
给一个按照升序排序的非负整数数组。这个数组很大以至于你只能通过固定的接口 ArrayReader.get(k) 来访问第k个数(或者C++里是ArrayReader->get(k))，并且你也没有办法得知这个数组有多大。
找到给出的整数target第一次出现的位置。你的算法需要在O(logk)的时间复杂度内完成，k为target第一次出现的位置的下标。
如果找不到target，返回-1。

如果你访问了一个不可访问的下标（比如越界），ArrayReader 会返回2,147,483,647。
**## 样例**
**样例 1:**

输入: [1, 3, 6, 9, 21, ...], target = 3
输出: 1
**样例 2:**

输入: [1, 3, 6, 9, 21, ...], target = 4
输出: -1
**## 挑战**
O(logn)的时间复杂度，n是target第一次出现的下标。
 

////////////// 方法2 二分

/**
 * Definition of ArrayReader:
 * 
 * class ArrayReader {
 * public:
 *     int get(int index) {
 *          // return the number on given index, 
 *          // return 2147483647 if the index is invalid.
 *     }
 * };
 */
**class** **Solution** {
public:
    /*
     * @param reader: An instance of ArrayReader.
     * @param target: An integer
     * @return: An integer which is the first index of target.
     */
    int searchBigSortedArray(ArrayReader * reader, int target) {
        int l = 0, r = 1, mid;
        **while** (reader->**get**(r) < target)     // 越界返回INT_MAX, 必然大于target, 所以没有关系
            r <<= 1;
        
        **while** (l < r) {
            mid = (l + r) >> 1;
            **if** (reader->**get**(mid) >= target)
                r = mid;
            **else**

                l = mid + 1;
        }
        
        **if** (reader->**get**(l) == target)
            **return** l;
        **else**

            **return** -1;
    }
};
	
