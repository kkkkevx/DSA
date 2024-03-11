# Day 5: 代码随想录算法训练营

## Topic:
- HashTable
- HashMap
- HashSet

## Summary:
- **哈希表**： "When we need to quickly determine whether an element appears in a collection, we should consider using hash tables."
- **HashMap and HashTable** utilize an array, linked list, and red-black tree. When the size of the linked list exceeds 8, it can be converted into a red-black tree to improve efficiency.
- **LinkedHashMap / LinkedHashSet**: Maintain the order in which elements are inserted into collections.
- **TreeSet / TreeMap**: Customize the order.
- Array (int[]) can be used as HashTable when kning that the index of the array corresponds something. Like int[26] each index can represent one alphabet character
- Need more familiar with Stream API like convert to array

## LeetCode 349. 两个数组的交集
**[Problem](https://leetcode.cn/problems/intersection-of-two-arrays/description/)**

**[Recourse](https://programmercarl.com/0349.%E4%B8%A4%E4%B8%AA%E6%95%B0%E7%BB%84%E7%9A%84%E4%BA%A4%E9%9B%86.html#%E5%90%8E%E8%AE%B0)** 

``` java
import java.util.*;

class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set1 = new HashSet<>();
        Set<Integer> set2 = new HashSet<>();

        for (int num : nums1) {
            set1.add(num);
        }

        for (int num : nums2) {
            if (set1.contains(num)) {
                set2.add(num);
            }
        }

        int[] intArray = set2.stream().mapToInt(Integer::intValue).toArray();

        return intArray;


    }
}
```

## LeetCode 242. 有效的字母异位词
**[Problem](https://leetcode.cn/problems/valid-anagram/)**

**[Recourse](https://programmercarl.com/0242.%E6%9C%89%E6%95%88%E7%9A%84%E5%AD%97%E6%AF%8D%E5%BC%82%E4%BD%8D%E8%AF%8D.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)** 

``` java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;

        int[] dic = new int[26];

        for (int i = 0; i < s.length(); i++) {
            dic[s.charAt(i) - 'a']++;
        }

        for (int i = 0; i < t.length(); i++) {
            dic[t.charAt(i) - 'a']--;
        }

        for (int i : dic) {
            if (i != 0) return false;
        }

        return true;
    }
}
```

## LeetCode 202. 快乐数
**[Problem](https://leetcode.cn/problems/happy-number/description/)**

**[Recourse](https://programmercarl.com/0202.%E5%BF%AB%E4%B9%90%E6%95%B0.html)** 

**Important** This question focuses on avoiding infinite loops. Utilize HashSet to prevent such occurrences.

``` java
class Solution {
    public boolean isHappy(int n) {
        Set<Integer> record = new HashSet<>();

        while (n != 1 && !record.contains(n)) {
            record.add(n);
            n = nextNumber(n);
        }

        return n ==1;
    }

    private int nextNumber(int n) {
        int res = 0;
       while (n > 0) {
        int tmp = n % 10;
        res += tmp * tmp;
        n /= 10;
       }

       return res;
    }
}
```
## LeetCode 1. 两数之和
**[Problem](https://leetcode.cn/problems/two-sum/description/)**

**[Recourse](https://programmercarl.com/0001.%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C.html#%E6%80%9D%E8%B7%AF)** 

``` java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> record = new HashMap<>();
        int[] res = new int[2];

        for (int i = 0; i < nums.length; i++) {
            int tmp = target - nums[i];
            if (record.containsKey(tmp)) {
                res[0] = i;
                res[1] = record.get(tmp);
                break;
            }

            record.put(nums[i], i);

        }
        return res;
    }
}
```
