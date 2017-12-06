
# 选择排序

## 介绍

 1. 选择待排序序列中选择最小的元素，然后和待排序序列的第一个元素交换位置
 2. 将剩下的待排序序列中选择最小的元素，和待排序序列的第二个元素交换位置
 3. 重复以上步骤，直到将整个数组都排序。

 因为在不断的选择剩余最小的元素，所以称之为选择排序
  
## 算法特点

* 不稳定排序
* 交换次数固定为`n-1`次交换
* 比较次数也固定为`(n-1)*n/2`次
* 选择排序的时间复杂度和数据的输入无关

## 代码示例-Java

```
 /**
 * 简单选择排序
 * @param nums
 * @return
 */
public static void selectSort(int[] nums){
    if (nums == null || nums.length <= 0) return;

    int minIndex, temp;
    for (int i = 0; i < nums.length ; i++){
        minIndex = i;
        for (int j = i + 1; j < nums.length; j++){
            if (nums[j] < nums[minIndex]){
                minIndex = j;
            }
        }

        temp = nums[minIndex];
        nums[minIndex] = nums[i];
        nums[i] = temp;
    }
}

```


