<h1 align='center'>35、Search Insert Position</h1>

[题目地址](https://leetcode.com/problems/search-insert-position/)

### 英文题目
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Here are few examples.

    [1,3,5,6], 5 → 2
    [1,3,5,6], 2 → 1
    [1,3,5,6], 7 → 4
    [1,3,5,6], 0 → 0

### 中文翻译

给定一个已排序的数组和一个值target，返回target在这个数组中出现的位置，如果不存在，
就返回target应该在数组中插入的位置。
假定数组中不存在重复的值。
下面是一些例子

    [1,3,5,6], 5 → 2
    [1,3,5,6], 2 → 1
    [1,3,5,6], 7 → 4
    [1,3,5,6], 0 → 0

### 解题思路

这道题目的意思就是在一个已排序的数组中，查找一个数字，如果查到就返回其索引，如果查不到就返回应该插入的位置。其实这道题目就是一道查找的变形，可以使用二分查找的方法解决。

1. arr[mid] == target。说明target在数组中存在。mid就是结果。
2. arr[mid] > target。那么target存在于arr[begin ~ (mid-1)] 中间。如果target > arr[mid -1],就说明数组中不存在target，那么mid就是target适合插入的位置。
3. arr[mid] < target。那么target存在于arr[(mid+1) ~ end] 中间。如果target < arr[mid + 1],就说明数组中不存在target，那么 `mid + 1`就是target适合插入的位置。

如果数组中不存在这个问题，依然使用二分查找方法解决。

### 代码示例-Java

```
public class Leetcode_0035_search_insert_position {

    /**
     * 最笨的方法,循环遍历。
     * @param nums
     * @param target
     * @return
     */
    public static int searchInsert(int[] nums, int target) {
        if (nums == null){
            return 0;
        }

        int begin = 0;
        int end = nums.length -1;
        while (begin <= end){
            int mid = (begin + end) / 2;
            if (nums[mid] == target ){
                return mid;
            }else if (nums[mid] < target){
                begin = mid + 1;
                if (begin < nums.length && nums[begin] > target){
                    return begin;
                }
            }else{
                end = mid -1;
                if (end >= 0 && nums[end] < target){
                    return end + 1;
                }
            }
        }

       return end + 1;
    }


    public static void test(int[] nums, int target){
        long startTime = System.nanoTime();
        int result = searchInsert(nums, target);
        long endTime = System.nanoTime();
        System.out.println(String.format("time :" + (endTime - startTime)+" result: %s", result));
    }


    public static void main(String[] args){
        test(new int[]{1,3}, 2); // 1
        test(new int[]{1,3}, 0); // 0
        test(new int[]{1,3,5,6}, 5); // 2
        test(new int[]{1,3,5,6}, 2); // 1
        test(new int[]{1,3,5,6}, 7); // 4
        test(new int[]{1,3,5,6}, 0); // 0
    }
}
```
