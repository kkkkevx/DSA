# Day 8: 代码随想录算法训练营

## Topic:
- String
- KMP

## Summary:
- KMP is really hard for me. I will come back to overcome it.
- I solved solution by other solutions
- 移动匹配 （判断字符串s是否由重复子串组成，只要两个s拼接在一起，里面还出现一个s的话，就说明是由重复子串组成）


## Leetcode Probelm

**[Recourse](https://programmercarl.com/0028.%E5%AE%9E%E7%8E%B0strStr.html#%E6%80%BB%E7%BB%93)**


Leetcode 28. 找出字符串中第一个匹配项的下标

``` java
class Solution {
    /**
        时间复杂度 O(n * m)
        空间 O(n + m)
     */
    public int strStr(String haystack, String needle) {
        // 获取 haystack 和 needle 的长度
        int n = haystack.length(), m = needle.length();
        // 将字符串转换为字符数组，方便索引操作
        char[] s = haystack.toCharArray(), p = needle.toCharArray();

        // 遍历 haystack 字符串
        for (int i = 0; i < n - m + 1; i++) {
            // 初始化匹配的指针
            int a = i, b = 0;
            // 循环检查 needle 是否在当前位置开始匹配
            while (b < m && s[a] == p[b]) {
                // 如果当前字符匹配，则移动指针
                a++;
                b++;
            }
            // 如果 b 等于 m，说明 needle 已经完全匹配，返回当前位置 i
            if (b == m) return i;
        }

        // 如果遍历完毕仍未找到匹配的子串，则返回 -1
        return -1;
    }
}

```

Leetcode 459 重复的子字符串

it is smart way to solve this problem. 去头去尾看中间有没有形成重复的str
移动匹配

``` java
class Solution {
    public boolean repeatedSubstringPattern(String s) {
        String str = s + s;
        return str.substring(1, str.length() - 1).contains(s);
    }
}
```
