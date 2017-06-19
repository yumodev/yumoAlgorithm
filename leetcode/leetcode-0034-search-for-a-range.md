<h1 align='center'>34、Search for a Range</h1>

[题目地址](https://leetcode.com/problems/search-for-a-range/)

### 英文题目

Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.
Your algorithm's runtime complexity must be in the order of O(log n).
If the target is not found in the array, return [-1, -1].

For example,
Given [5, 7, 7, 8, 8, 10] and target value 8,
return [3, 4].

### 中文翻译

给定一个升序排序整数数组，查找给定目标值的起始和结束位置。你的算法复杂度必须为O(log n).
如果数组中查不到目标返回[-1, -1]
举例 ：
数组 [5, 7, 7, 8, 8, 10] 和 目标值 8,
返回 [3, 4].

### 解题思路

题目的主要意思就是找到目标值在数组上出现的起始和结束位置，结合要求的复杂度为O(log n).就知道采取二分找到的方法。
先通过二分查找找到目标值所在的位置为 arr[mid] == target. 然后分别以mid为起点向前后循环查找其起始和终止位置。
### 代码示例-Java

```
public class Leetcode_0034_search_for_a_range {

    /**
     * 使用二分查找算法。
     * @param nums
     * @param target
     * @return
     */
    public static int[] searchRange(int[] nums, int target) {
        if (nums == null){
            return new int[]{-1,-1};
        }

        int begin = 0, end = nums.length -1, beginIndex = -1, endIndex = -1;
        while (begin <= end){
            int mid = (begin + end) / 2;
            if (nums[mid] == target){
                beginIndex = mid;
                endIndex = mid;
                while (beginIndex > 0 && nums[beginIndex -1] == target){
                    beginIndex = beginIndex -1;
                }

                while (endIndex < nums.length - 1 && nums[endIndex + 1] == target){
                    endIndex = endIndex + 1;
                }
                break;
            }else if (nums[mid] < target){
                begin = mid + 1;
            }else if (nums[mid] > target){
                end = mid - 1;
            }
        }
        return new int[]{beginIndex, endIndex};
    }

    /**
     * 一种更有效率的二分查找算法。
     * @param nums
     * @param target
     * @return
     */
    public static int[] searchRange1(int[] nums, int target) {
        if (nums == null){
            return new int[]{-1,-1};
        }

        int begin = 0, end = nums.length -1, beginIndex = -1, endIndex = -1;
        while (begin <= end){
            int mid = begin + (end - begin) / 2;
            if (nums[mid] == target){
                beginIndex = mid;
                endIndex = mid;
                while (beginIndex > 0 && nums[beginIndex -1] == target){
                    beginIndex = beginIndex -1;
                }

                while (endIndex < nums.length - 1 && nums[endIndex + 1] == target){
                    endIndex = endIndex + 1;
                }
                break;
            }else if (nums[mid] < target){
                begin = mid + 1;
            }else if (nums[mid] > target){
                end = mid - 1;
            }
        }
        return new int[]{beginIndex, endIndex};
    }

    public static void test(int[] nums, int target){
        long startTime = System.nanoTime();
        int[] result = searchRange1(nums, target);
        long endTime = System.nanoTime();
        System.out.println(String.format("time :" + (endTime - startTime)+" result: [%d, %d]", result[0], result[1]));
    }


    public static void main(String[] args){
        test(new int[]{1}, 1);
        test(new int[]{2,2}, 2);
        test(new int[]{5,7,7,8,8,10}, 8); // 0
    }
}

```
