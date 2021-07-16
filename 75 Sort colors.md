# 75 Sort colors

https://www.youtube.com/watch?v=oaVa-9wmpns&list=PLgUwDviBIf0rPG3Ictpu74YWBQ1CaBkm2&index=3

使用一次扫描的办法。 设立三根指针，left, index, right。定义如下规则：

* left 的左侧都是 0（不含 left）

* right 的右侧都是 2（不含 right）

index 从左到右扫描每个数，如果碰到 0 就丢给 left，碰到 2 就丢给 right。碰到 1 就跳过不管。

class Solution {
    public void sortColors(int[] nums) {
        int low = 0;
        int high = nums.length - 1;
        int middle = 0;
        
        while (middle <= high) {
            if(nums[middle] == 0) {
                swap(middle++, low++, nums);
            }else if (nums[middle] == 1) {
                middle++;
            }else if (nums[middle] == 2) {
                swap(middle, high--, nums);
            }          
        }
    }
    
    public void swap(int i, int j, int[] nums) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;      
    }
}

