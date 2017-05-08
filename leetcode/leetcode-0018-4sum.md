[18. 4Sum](https://leetcode.com/problems/4sum/)

### 原题目

Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.
Note: The solution set must not contain duplicate quadruplets.

    For example, given array S = [1, 0, -1, 0, -2, 2], and target = 0.

    A solution set is:
    [
      [-1,  0, 0, 1],
      [-2, -1, 1, 2],
      [-2,  0, 0, 2]
    ]

### 翻译

给定一个含有n个整数的数组S,其中有a,b,c,d四个元素的和等于 target? 找出所有不同的和为target的四元组。
注意：结果中不能包含重复的四元组。

    举个例子, 给定数组 S = [1, 0, -1, 0, -2, 2], 和 target = 0.

    结果如下:
    [
      [-1,  0, 0, 1],
      [-2, -1, 1, 2],
      [-2,  0, 0, 2]
    ]

### 解决思路

求和为target的四元组,我们可以转换为求b+c+d = taret - a, 这样就转换为求三元组的问题了。解决方案参照[3Sum](./Leetcode_0015_3sum.md)


### 代码示例-Java


```
package com.yumodev.java.airthmetic.leetcode;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

/**
 * Created by yumodev on 17/3/30.
 * Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target?
 * Find all unique quadruplets in the array which gives the sum of target.
 */

public class Leetcode_0018_4sum {

    public static List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> result = new ArrayList<>();
        if (nums == null || nums.length < 4) {
            return result;
        }

        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 3; i++) {
            if (i != 0 && nums[i] == nums[i -1]){
                continue;
            }

            if (nums[i] > 0 && nums[i] > target) {
                break;
            }

            for (int j = i + 1; j < nums.length - 2; j++) {
                if ((j != i + 1) && (nums[j] == nums[j-1])){
                    continue;
                }
                if (nums[i] + nums[j] > target && nums[i] + nums[j] > 0) {
                    break;
                }

                for (int k = j + 1; k < nums.length - 1; k++) {
                    if ((k != j + 1) && (nums[k] == nums[k-1])){
                        continue;
                    }
                    for (int z = k + 1; z < nums.length; z++) {
                        if (nums[i] + nums[j] + nums[k] + nums[z] == target) {
                            result.add(Arrays.asList(nums[i], nums[j], nums[k], nums[z]));
                            break;
                        }
                    }
                }
            }
        }

        return result;
    }


    public static List<List<Integer>> fourSum1(int[] nums, int target) {
        List<List<Integer>> result = new ArrayList<>();
        if (nums == null || nums.length < 4) {
            return result;
        }

        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 3; i++) {
            if (i != 0 && nums[i] == nums[i -1]){
                continue;
            }

            if (nums[i] > 0 && nums[i] > target) {
                break;
            }

            for (int j = i + 1; j < nums.length - 2; j++) {
                int temp = nums[i] + nums[j];
                if ((j != i + 1) && (nums[j] == nums[j-1])){
                    continue;
                }
                if ( temp > target && temp > 0) {
                    break;
                }

                int twoNum = target - temp;
                int begin = j + 1;
                int end = nums.length - 1;
                while (begin < end){
                    temp = nums[begin] + nums[end];
                    if (twoNum == temp){
                        result.add(Arrays.asList(nums[i], nums[j], nums[begin], nums[end]));
                        begin ++;
                        while (begin < end && nums[begin] == nums[begin-1]){
                            begin++;
                        }

                        end--;
                        while (begin < end && nums[end] == nums[end + 1]){
                            end--;
                        }
                    }else if (temp < twoNum){
                        begin ++;
                    }else{
                        end --;
                    }
                }
            }
        }

        return result;
    }

    public static void test(int[] num, int target) {
        long startTime = System.nanoTime();
        List<List<Integer>> result = fourSum1(num, target);
        long endTime = System.nanoTime();
        System.out.println(String.format("time :" + (endTime - startTime) + " result: %s", result.toString()));
    }

    public static void main(String[] args) {
        test(new int[]{1, 0, -1, 0, -2, 2}, 0);//[-1,0,0,1],[-2,-1,1,2],[-2,0,0,2]
        test(new int[]{-3,-2,-1,0,0,1,2,3}, 0);
        test(new int[]{1,-2,-5,-4,-3,3,3,5}, -11);//[-5,-4,--3,1]
        test(new int[]{-1,0,-5,-2,-2,-4,0,1,-2}, -9);//
        test(new int[]{-482,-468,-465,-460,-451,-428,-426,-415,-411,-405,-396,-394,-372,-370,-368,-361,-358,-353,-352,-334,-318,-300,-287,-273,-251,-241,-239,-218,-215,-212,-187,-185,-170,-145,-123,-112,-73,-63,-58,-36,-19,34,42,47,85,113,126,128,134,180,181,199,206,221,229,242,243,255,262,270,305,372,393,405,420,427,428,433,446,458,469,471,486
        }, -3254);
    }
}


```
