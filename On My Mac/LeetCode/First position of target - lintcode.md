# First position of target - lintcode

// **version** 1: **with** jiuzhang **template**

**class** Solution {
    /**
     * @param nums: The integer array.
     * @param target: Target to find.
     * @return: The first position of target. Position starts from 0.
     */
    public **int** binarySearch(**int**[] nums, **int** target) {
        **if** (nums == **null** || nums.length == 0) {
            **return** -1;
        }
        
        **int** start = 0, end = nums.length - 1;
        **while** (**start** + 1 < **end**) {
            **int** mid = **start** + (**end** - **start**) / 2;
            **if** (nums[mid] == target) {
                end = mid;
            } **else** **if** (nums[mid] < target) {
                start = mid;
                // **or** start = mid + 1
            } **else** {
                end = mid;
                // **or** end = mid - 1
            }
        }
        
        **if** (nums[**start**] == target) {
            **return** **start**;
        }
        **if** (nums[**end**] == target) {
            **return** **end**;
        }
        **return** -1;
    }
}

# Last Position of target -Lintcode

public **class** Solution {
    /*
     * @param nums: An integer array sorted in ascending order
     * @param target: An integer
     * @return: An integer
     */
    public **int** lastPosition(**int**[] nums, **int** target) {
        // **write** your code here
        **if** (nums == **null** || nums.length == 0) {
            **return** -1;
        }
        **int** start = 0;
        **int** end = nums.length - 1;
        **while** (**start** + 1 < **end**) {
            **int** mid = **start** + (**end** - **start**) / 2;
            **if** (nums[mid] == target) {
                start = mid;
            } **else** **if** (nums[mid] < target) {
                start = mid;
            } **else** {
                end = mid;
            }
        }
        **if** (nums[**end**] == target) {
            **return** **end**;
        } **else** **if** (nums[**start**] == target) {
            **return** **start**;
        } **else** {
            **return** -1;
        }
    }
}

Explanation in python:

**class** **Solution**:
    # @param nums: The integer array
    # @param target: Target number to find
    # @return the first position of target in nums, position start from 0 
    def binarySearch(self, nums, target):
        **if** **not** nums:
            **return** -1
            
        start, **end** = 0, len(nums) - 1
        # 用 start + 1 < end 而不是 start < end 的目的是为了避免死循环
        # 在 first position of target 的情况下不会出现死循环
        # 但是在 last position of target 的情况下会出现死循环
        # 样例：nums=[1，1] target = 1
        # 为了统一模板，我们就都采用 start + 1 < end，就保证不会出现死循环
        **while** start + 1 < **end**:
            # python 没有 overflow 的问题，直接 // 2 就可以了
            # java和C++ 最好写成 mid = start + (end - start) / 2
            # 防止在 start = 2^31 - 1, end = 2^31 - 1 的情况下出现加法 overflow
            mid = (start + **end**) // 2
            
            # > , =, < 的逻辑先分开写，然后在看看 = 的情况是否能合并到其他分支里
            **if** nums[mid] < target:
                # 写作 start = mid + 1 也是正确的
                # 只是可以偷懒不写，因为不写也没问题，不会影响时间复杂度
                # 不写的好处是，万一你不小心写成了 mid - 1 你就错了
                start = mid
            elif nums[mid] == target:
                **end** = mid
            **else**: 
                # 写作 end = mid - 1 也是正确的
                # 只是可以偷懒不写，因为不写也没问题，不会影响时间复杂度
                # 不写的好处是，万一你不小心写成了 mid + 1 你就错了
                **end** = mid
                
        # 因为上面的循环退出条件是 start + 1 < end
        # 因此这里循环结束的时候，start 和 end 的关系是相邻关系（1和2，3和4这种）
        # 因此需要再单独判断 start 和 end 这两个数谁是我们要的答案
        # 如果是找 first position of target 就先看 start，否则就先看 end
        **if** nums[start] == target:
            **return** start
        **if** nums[**end**] == target:
            **return** **end**

        
        **return** -1

