# 直接插入排序

## 直接插入排序的原理

 1. 将第一个元素和第二个元素进行比较排序，形成一个有序的序列。
 2. 将第三个元素插入已排序的序列中，形成一个新的有序序列。
 3. 依次将后面的元素插入到前面的有序序列中。

## 算法分析

 |正序 | 反序 
---|---|---
比较次数 | n-1 | n*(n-1)/2 
移动次数 | 0  | n*(n-1)/2

## 直接插入排序特点

* 属于稳定排序
* 直接插入排序的平均算法复杂度为:O（ n^2 ）
* 直接插入排序的空间复杂度为:O ( 1 )
* 插入排序对部分有序的数组十分高效，适合小规模数组

## 代码示例


```java
/**
 * 使用for循环的直接插入。
 * @param nums
 * @return
 */
public static void insertSort(int[] nums){
    if (nums == null || nums.length <= 1) return;

    for (int i = 1; i < nums.length; i++){
        int temp = nums[i];
        int j = i;
        for (; j > 0 && nums[j] >= temp; j--){
            nums[j] = nums[j - 1];
        }
        nums[j] = temp;
    }
}

 /**
 * 使用While循环进行排序
 * @param nums
 */
public static void insertSort1(int[] nums) {
    if (nums == null || nums.length <= 1) return;

    for (int i = 1; i < nums.length; i++) {
        int temp = nums[i];
        int j = i;
        while (j > 0 && nums[j] >= temp){
            nums[j] = nums[j-1];
            j--;
        }

        nums[j] = temp;
    }
}
```

