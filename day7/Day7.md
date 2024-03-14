# Day 7: 代码随想录算法训练营

## Topic:
- String
- Two Pointers
- Reverse String

## Summary:
- Use two pointers to figured out String reversal tasks
- It is important to handle edge cases



## LeetCode Problem:

**[Recourse](https://programmercarl.com/0344.%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC)**

LeetCode 344. Reverse String
- This problem requires reversing a given string. You can utilize the two-pointer approach, starting from both ends of the string and swapping characters at corresponding positions.

```java
class Solution {
    public void reverseString(char[] s) {
        int l = 0;
        int r = s.length - 1;
        while (l < r) {
            char temp = s[l];
            s[l] = s[r];
            s[r] = temp;
            l++;
            r--;
        }
    }
}
```

LeetCode 541. Reverse String II
- employ the two-pointer technique to process segments of 2k length, reversing the first k characters in each segment.
``` java
class Solution {
    public String reverseStr(String s, int k) {
        char[] res = s.toCharArray();
        for (int i = 0; i < s.length(); i += 2 * k) {
                int start = i;

                int end = Math.min(s.length() - 1, start + k -1);

                while (start < end) {
                    char temp = res[start];
                    res[start] = res[end];
                    res[end] = temp;
                    start++;
                    end--;
                }
        } 
        
        return new String(res);
    }
}
```
  
LeetCode 151. Reverse Words in a String
- really hard to do in place operation： O(1) space complexity
- first find last word start and end, then last second word, then next.
``` java
public class Solution {
    public String reverseWords(String s) {
        StringBuilder result = new StringBuilder();
        int end = s.length();
        int i = s.length() - 1;

        // 找到最后一个单词的结束位置
        while (i >= 0 && s.charAt(i) == ' ') {
            i--;
        }
        end = i + 1;

        // 逐个添加单词
        while (i >= 0) {
            // 找到单词的开始位置
            while (i >= 0 && s.charAt(i) != ' ') {
                i--;
            }
            // 添加单词
            if (i + 1 < end) {
                if (result.length() > 0) {
                    result.append(' ');
                }
                result.append(s.substring(i + 1, end));
            }
            // 跳过单词间的空格
            while (i >= 0 && s.charAt(i) == ' ') {
                i--;
            }
            // 更新下一个单词的结束位置
            end = i + 1;
        }

        return result.toString();
    }
}
```

卡码网 54：
``` java
import java.util.*;
class Main {
    public static void main (String[] args) {
        /* code */
        Scanner in = new Scanner(System.in);
        String s = in.nextLine();
        StringBuilder res = new StringBuilder()
        
        for (int i = 0; i < s.length(); i++) {
            if (Character.isDigit(s.charAt(i))) {
                res.append("number");
            } else {
                res.append(s.charAt(i));
            }
        }
        System.out.println(res);
    }
}
```
