[15. 3Sum](https://leetcode.com/problems/3sum/)

### 原题目

Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note: The solution set must not contain duplicate triplets.

### 翻译

给定还有`n`个整数的数组`s`，在数组s有三个元素`a,b,c`,使其`a + b + c = 0`? 在这个数组中，找出所有独特的总和为`0`的三元组。
注意：结果中不能包含重复的三元组。

### 解决思路

这个题目的主要意思是在一个数组中找出所有总和为0且不重复的三元组。可以使用的穷举的方法求的结果，但是这个效率比较差，并且判定三元组是否重复也是个麻烦事儿。除了穷举算法以外，我们还可以将问题进行分解，解决步骤如下
1. 首先对数组S进行升序排序
2. 第一重循环数组S,确定第一个数 a. 现在我们要取第二个数b和第三个数c,使其b + c = -a 此时就转换为获取唯一且和为-c的二元组的问题了。
3. 第二重循环中，第二个数b和第三个数c分别从两端往中间扫。
   如果b + c = -a，得到一个三元组，然后第二个数往前移，第三个数往后移
   如果b + c < -a, 第二个数往前移。
   如果b + c > -a, 第三个数往后移。
4. 第二重循环结束后，继续循环数组，确定第一个数字。为了不产生重复的三元组。
   当第一个数字 a>0时 跳出第一重循环。
   当第一个数字 a 重复出现时跳过第二重循环。

   流程图如下：


### 代码示例-Java


```
package com.yumodev.java.airthmetic.leetcode;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashSet;
import java.util.List;
import java.util.Set;

/**
 * Created by yumodev on 17/3/29.
 * Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.
 */

public class Leetcode_0015_3sum {
    /**
     * 穷举法
     *
     * @param nums
     * @return
     */
    public static List<List<Integer>> threeSum(int[] nums) {
        if (nums.length < 3) {
            return new ArrayList<>();
        }

        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();
        for (int i = 0; i < nums.length - 2; i++) {
            for (int j = i + 1; j < nums.length - 1; j++) {
                for (int z = j + 1; z < nums.length; z++) {
                    if (nums[i] + nums[j] + nums[z] == 0) {
                        List<Integer> list = new ArrayList<>();
                        list.add(nums[i]);
                        list.add(nums[j]);
                        list.add(nums[z]);
                        if (result.contains(list)) {
                            continue;
                        }
                        result.add(list);
                    }
                }
            }
        }
        return result;
    }


    /**
     * @param nums
     * @return
     */
    public static List<List<Integer>> threeSum1(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        if (nums.length < 3) {
            return result;
        }

        Arrays.sort(nums);

        for (int i = 0; i < nums.length - 2; i++) {
            if (nums[i] > 0) {
                break;
            }

            if (i > 0 &&  nums[i] == nums[i-1]){
               continue;
            }

            int twoNum = 0 - nums[i];
            int begin = i + 1;
            int end = nums.length - 1;
            int temp;
            while (begin < end) {
                 temp = nums[begin] + nums[end];
                 if (temp == twoNum) {
                    result.add(Arrays.asList(nums[i], nums[begin], nums[end]));
                    while (begin < end && nums[begin] == nums[begin +1]){
                        begin ++;
                    }

                    while (begin < end && nums[end] == nums[end -1]){
                        end --;
                    }

                    begin ++;
                    end --;
                } else if (temp < twoNum) {
                    begin++;
                } else {
                    end--;
                }
            }
        }
        return result;
    }

    public static void test(int[] num){
        long startTime = System.nanoTime();
        List<List<Integer>> result = threeSum1(num);
        long endTime = System.nanoTime();
        System.out.println(String.format("time :" + (endTime - startTime) + " result: %s", result.toString()));
    }
    public static void main(String[] args) {
        test(new int[]{0,0,0,0});
        test(new int[]{-2,0,1,1,2});
        test(new int[]{-1,0,1,2,-1,-4});
    }
}
```
