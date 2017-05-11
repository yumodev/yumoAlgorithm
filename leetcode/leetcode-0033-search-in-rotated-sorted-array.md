<h1 align='center'>33、Search in Rotated Sorted Array</h1>

[题目地址](https://leetcode.com/problems/search-in-ratated-sorted-array/)

### 英文题目

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.
(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).
You are given a target value to search. If found in the array return its index, otherwise return -1.
You may assume no duplicate exists in the array.

### 中文翻译

假设以升序排列的数组在您预先知道的枢轴上旋转
(比如, 0 1 2 4 5 6 7 旋转为 4 5 6 7 0 1 2).
你将被给定一个Value。如果在数组中查找到Value就返回其索引。，否则就返回-1.
假定数组中不存在重复的数据。

### 解题思路

这道题目的第一反应就是使用二分查找来解决问题，可是使用二分查找算法的数组通常都是有序的，但是题目给定的
数据却不是有序的。但是题目的数组是由一个有序的旋转等来，那么它的特点就是这个数组分为了两部分，每部分都是有序的。
所以这就为使用二分查找算法来解决这个问题带来了可能性。

如果`nums[mid] == target` 那么mid就是要找到的索引。
如果`nums[mid] != target `, 现在就要判断target是出现在左半边还是右半边了。假定如果`mid < end`的时候，假定出现在右半边, 如果`target > nums[mid] && target <= nums[end]`,那么`begin = mid + 1`, 否则 `end = mid -1`. 如果`mid > end`的时候，假定出现在左半边, 如果`target > nums[begin] && target <= nums[end]`,那么 `end = mid - 1,` 否则 `begin = mid + 1`;

### 代码示例-Java

```
public class Leetcode_0033_search_in_rotated_sorted_array {

    public static int search(int[] nums, int target){
        if (nums == null || nums.length < 1){
            return -1;
        }
        int result = -1;
        int begin = 0;
        int end = nums.length -1;

        while (begin <= end){
            int mid = (begin + end) / 2;
            if (nums[mid] == target){
                result = mid;
                break;
            }else if (nums[mid] < nums[end]){
                if (target > nums[mid] && target <= nums[end]){
                    begin = mid + 1;
                }else{
                    end = mid -1;
                }
            }else{
                if (target >= nums[begin] && target<nums[mid]){
                    end = mid -1;
                }else{
                    begin = mid + 1;
                }
            }
        }
        return result;
    }

    public static void test(int[] nums, int target){
        long startTime = System.nanoTime();
        int result = search(nums, target);
        long endTime = System.nanoTime();
        System.out.println(String.format("time :" + (endTime - startTime)+" result: %s", result));
    }

    public static void main(String[] args){
        test(new int[]{3, 5, 1}, 3); // 0
        test(new int[]{4, 5, 6, 7, 0, 1, 2}, 1); //5
        test(new int[]{1}, 1); // 0
    }
}

```
