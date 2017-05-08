[16. 3Sum Closest](https://leetcode.com/problems/3sum-closest/)

### 原题目

Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

    For example, given array S = {-1 2 1 -4}, and target = 1.
    The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

### 翻译

给定一个含有n个整数的数组S,在数组S中寻找三个数字，它们的和最接近一个给定的数字target。返回这三个整数的和。你可以认为每一个输入都有一个确定的输出。

    举个例子,给定数组 S = {-1 2 1 -4}, 和 target = 1.
    最接近target 的和是 2. (-1 + 2 + 1 = 2).

### 解决思路

这个题目和[3Sum](https://leetcode.com/problems/3sum/)非常的相似。

1. 对数组S进行升序排序。
2. 从数组中选取一个数，然后在剩下的数组中声明两个首尾指针，移动选取两个数。如果三个数的和等于targe，那就直接返回，如果三个数的和小于target那么首指针向后移动，如果三个数的和大于target,那就尾指针向前移动。

为了提高比较的效率我们可以将已经和target比较过得和，放到set中。


### 代码示例-Java


```
package com.yumodev.java.airthmetic.leetcode;

import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;

/**
 * Created by yumodev on 17/3/30.
 */

public class Leetcode_0016_3sum_closest {

    /**
     * 先用最笨的方法
     * @param nums
     * @param target
     * @return
     */
    public static int threeSumClosest(int[] nums, int target) {
        if (nums == null || nums.length < 3){
            return 0;
        }

        Arrays.sort(nums);

        int temp;
        int closest = nums[0] + nums[1] + nums[2];
        Set<Integer> sets = new HashSet<>();
        sets.add(closest);
        for (int i = 0; i < nums.length-2; i++){
//            if (nums[i] >= target){
//                break;
//            }
            for(int j = i + 1; j < nums.length - 1; j++){
                for (int k = j + 1; k < nums.length; k++){
                    temp = nums[i] + nums[j] + nums[k];
                    if (temp == target){
                        closest = temp;
                        break;
                    }
                    if (sets.contains(temp)){
                        continue;
                    }
                    if (Math.abs(closest - target) > Math.abs(temp - target)){
                        closest = temp;
                    }
                    sets.add(temp);
                }

                if (closest == target){
                    break;
                }
            }

            if (closest == target){
                break;
            }
        }

        return closest;
    }


    /**
     * 先用最笨的方法
     * @param nums
     * @param target
     * @return
     */
    public static int threeSumClosest1(int[] nums, int target) {
        if (nums == null || nums.length < 3){
            return 0;
        }

        Arrays.sort(nums);

        int temp;
        int closest = nums[0] + nums[1] + nums[2];
        Set<Integer> sets = new HashSet<>();
        sets.add(closest);
        for (int i = 0; i < nums.length-2; i++){
            int begin = i + 1;
            int end = nums.length -1;
            while (begin < end){
                temp = nums[i] + nums[begin] + nums[end];
                if (temp == target){
                    closest = target;
                    break;
                }

                if (!sets.contains(temp)){
                    if (Math.abs(closest - target) > Math.abs(temp - target)){
                        closest = temp;
                    }
                    sets.add(temp);
                }

                if (temp > target){
                    end --;
                }else if (temp < target){
                    begin ++;
                }
            }

            if (closest == target){
                break;
            }
        }

        return closest;
    }

    public static void test(int[] nums, int target){
        long startTime = System.nanoTime();
        int result = threeSumClosest1(nums, target);
        long endTime = System.nanoTime();
        System.out.println(String.format("time :" + (endTime - startTime)+" result: %s", result));
    }

    public static void main(String[] args){
        test(new int[]{1,2,4,8,16,32,64,128},82);//82
        test(new int[]{-1,2,1,-4}, 1);//2
        test(new int[]{6,-18,-20,-7,-15,9,18,10,1,-20,-17,-19,-3,-5,-19,10,6,-11,1,-17,-15,6,17,-18,-3,16,19,-20,-3,-17,-15,-3,12,1,-9,4,1,12,-2,14,4,-4,19,-20,6,0,-19,18,14,1,-15,-5,14,12,-4,0,-10,6,6,-6,20,-8,-6,5,0,3,10,7,-2,17,20,12,19,-13,-1,10,-1,14,0,7,-3,10,14,14,11,0,-4,-15,-8,3,2,-5,9,10,16,-4,-3,-9,-8,-14,10,6,2,-12,-7,-16,-6,10},
        -52); //-52
    }
}

```
