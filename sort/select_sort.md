## 选择排序

### 介绍

    选择排序的思想就是每次从待排序中选择一个最小的数，然后放到待排序的数组的前面，属于不稳定排序。
    算法复杂度为

### 算法特点

* 不稳定排序
* 时间复杂度:O($n^2$)
* 空间复杂度:O(1)

### 代码示例-Java

```
public class SelectSort {

    /**
     * 选择排序
     * @param nums
     * @return
     */
    public static int[] sort(int[] nums){
        if (nums == null || nums.length <= 0){
            return nums;
        }

        for (int i = 0; i < nums.length ; i++){
            int minIndex = i;
            for (int j = i + 1; j < nums.length; j++){
                if (nums[j] < nums[minIndex]){
                    minIndex = j;
                }
            }

            int temp = nums[minIndex];
            nums[minIndex] = nums[i];
            nums[i] = temp;
        }

        return nums;
    }

    public static void test(int[] nums){
        System.out.println(String.format("before sort: %s", Arrays.toString(nums)));
        long startTime = System.nanoTime();
        int[] result = sort(nums);
        long endTime = System.nanoTime();
        System.out.println(String.format("time :" + (endTime - startTime)+" result: %s", Arrays.toString(result)));
    }


    public static void main(String[] args){
        test(new int[]{4,3,2,1});
    }
}

```


