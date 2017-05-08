[27. Remove Element](https://leetcode.com/problems/remove-element/)

### 原题目
Given an array and a value, remove all instances of that value in place and return the new length.
Do not allocate extra space for another array, you must do this in place with constant memory.
The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Example:
Given input array nums = [3,2,2,3], val = 3
Your function should return length = 2, with the first two elements of nums being 2.

### 翻译

给定一个数组和一个值Value，删除所有值等于Value的元素，返回新的数组长度。
不要为另一个数组分配额外的空间，您必须使用常量内存来进行此操作。
元素的顺序可以改变。 除了新的长度，你不必关心其它。
比如：输入数组=` [3,2,2,3]`, val = 3
你的方法将返回长度为=`2`.

### 解题思路

在一个数组中删除值为val的元素，返回新数组的长度。这个只需要遍历一遍数组即可，
也可以通过收尾指针遍历一遍数组。

### 代码示例-Java


```
/**
 * Created by yumodev on 9/18/16.
 */
public class Leetcode_0027_RemoveElement {

    public static int removeElement(int[] nums, int val){
        if (nums == null || nums.length == 0){
            return 0;
        }


        int i = 0;
        for (int j = 0; j < nums.length; j++){
            if (nums[j] != val){
                nums[i] = nums[j];
                i++;
            }
        }

        return i;
    }

    public static void main(String[] args){
        int[] nums = {3,2,2,3};
        int value = 3;
        long startTime = System.nanoTime();
        int result = removeElement(nums, value);
        long endTime = System.nanoTime();
        long time = endTime - startTime;

        System.out.println(" removeElement:" + result + " time:" + time);
    }
}
```
