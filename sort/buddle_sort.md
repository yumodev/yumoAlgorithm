# 冒泡排序

## 冒泡排序的原理

1. 比较相邻的两个元素，如果第一个元素大于第二个元素，就交互两个元素的位置。
2. 将序列中剩余的元素重复第一步的比较。
3. 重复所有的元素，进行上面的比较

## 冒泡排序的特点

冒泡排序的算法复杂度为：O（ n^2 ）


## 代码示例


```java

 /**
 * 常规冒泡排序
 * @param nums
 * @return
 */
public static int[] bubbleSort(int[] nums){
    if (nums == null || nums.length <= 1){
        return nums;
    }

    for (int i = 0; i< nums.length; i++){
        for (int j = 0; j < nums.length - 1; j++){
            if (nums[j] > nums[j + 1]){
                int temp = nums[j];
                nums[j] = nums[j+1];
                nums[j+1] = temp;
            }
        }
    }
    return nums;
}
```

