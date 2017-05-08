[28. Implement strStr()](https://leetcode.com/problems/implement-strstr/)

### 原题目

Implement strStr().
Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

### 翻译

实现方法 strStr().
在草垛(haystack)中返回针(needle)的索引，如果不存在就返回-1

### 解决思路

这道题目的意思比较清晰就是在一个字符串中查找一个字符串在其中第一次出现的索引的位置。

### 代码示例-Java

```
/**
 * Created by yumodev on 9/19/16.
 */
public class Leetcode_0028_StrStr {

    /**
     * 暴力法
     * @param haystack
     * @param needle
     * @return
     */
    public static int strStr(String haystack, String needle){
        if (haystack == null || needle == null || needle.length() == 0){
            return 0;
        }

        for (int i = 0; i < (haystack.length() - needle.length()); i++){
            if (haystack.charAt(i) != needle.charAt(0)) {
                continue;
            }

            int j = 1;
            for (;j < needle.length(); j++){
                if (needle.charAt(j) != haystack.charAt(i+j)){
                    break;
                }
            }

            if (needle.length() == j){
                return i;
            }
        }

        return -1;
    }

    public static void main(String[] args){
        String haystack = "aaa";
        String needle = "aaaa";

        long startTime = System.nanoTime();
        int result = strStr(haystack, needle);
        long endTime = System.nanoTime();
        long time = endTime - startTime;

        System.out.println(" strStr:" + result + " time:" + time);
    }
}
```
