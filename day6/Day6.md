# Day 6: 代码随想录算法训练营

## Topic:
- HashTable
- HashMap
- HashSet

## Summary:
- Hash tables provide efficient lookups and insertions by mapping keys to values using a hash function.
- Understanding the problem requirements is crucial for effective problem-solving.
- Handling edge cases, such as empty inputs or special characters, is essential to ensure robust code.
- Avoiding duplicate calculations and optimizing code can improve efficiency and readability.
- Choosing the appropriate data structure, such as hash tables for lookups and mappings, is vital for solving different types of problems effectively.
- 双指针法通常适用于求解 <span style="color: red;">有序</span> 数组或链表中 <span style="color: red;">固定长度</span> 的问题，并且能够利用双指针夹逼的性质来降低时间复杂度。

## LeetCode Problems:
[recourse](https://programmercarl.com/0454.%E5%9B%9B%E6%95%B0%E7%9B%B8%E5%8A%A0II.html)

### LeetCode 454. Four Sum II

You've used a HashMap named record to store the sum of all pairs from nums1 and nums2 as keys and their corresponding frequency as values.
Then, you've iterated over nums3 and nums4 and checked for the complement of the sum (-1 * (a + b)) in the record map. If found, you've added the frequency of that complement to the result res.

``` java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        Map<Integer, Integer> record = new HashMap<>();
        int res = 0;

        for (int a : nums1) {
            for (int b : nums2) {
                record.put(a+b, record.getOrDefault((a + b),0) + 1);
            }
        }

        for (int a : nums3) {
            for (int b : nums4) {
                res += record.getOrDefault(-(a+b), 0);
            }
        }

        return res;
    }
}
```

### LeetCode 383. Ransom Note

Implemented a hash table to store the frequency of each character in the ransom note.
Iterated through the magazine, decrementing the frequency count for each character encountered.
Checked if any character frequency became negative, indicating the inability to construct the ransom note from the magazine.

class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        // o(n) o(1)
        if (ransomNote.length() > magazine.length()) return false;

        int[] dic = new int[26];

        for (int i = 0; i < magazine.length(); i++) {
            dic[magazine.charAt(i) - 'a']++;
        }

        for (int i = 0; i < ransomNote.length(); i++) {
            dic[ransomNote.charAt(i) - 'a']--;
        }

        for (int i = 0; i < dic.length; i++) {
            if (dic[i] < 0) return false;
        }

        return true;
    }
}

### LeetCode 15. Three Sum

Sorted the array to use the double-pointer technique.
Fixed one number and used two pointers to find the other two numbers summing to zero.
Handled duplicates by skipping equal elements and avoiding redundant calculations.

``` java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {

        //也可以用set去做去重 就是比较慢 只要能确保三元组中元素顺序是对的
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();

        for (int i = 0; i < nums.length - 2; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue; // 去重

            int left = i + 1;
            int right = nums.length - 1;

            while (left < right) {
                if ((nums[i] + nums[left] + nums[right]) > 0) {
                    right--; // 大了往左去
                } else if ((nums[i] + nums[left] + nums[right]) < 0) {
                    left++; // 小了往右去
                } else {
                    res.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    
                    //去重
                    while (left < right && nums[left] == nums [left + 1]) left++;
                    while (left < right && nums[right] == nums[right - 1]) right--;

                    left++;
                    right--;
                }
            }
        }
        return res;
    }
}
```

### LeetCode 18. Four Sum

Applied a similar approach to three-sum, fixing two numbers and employing double pointers to find the other two numbers summing to the target value.
Addressed duplicate combinations to ensure unique quadruplets.

``` java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();

        for (int i = 0; i < nums.length; i++) {
                if (i > 0 && nums[i] == nums[i - 1]) continue; // 去重

            for (int j = i + 1; j < nums.length - 2; j++) {
                if (j > i + 1 && nums[j] == nums[j - 1]) continue; // 去重

                int left = j + 1;
                int right = nums.length - 1;

                while (left < right) {
                    long sum = (long) nums[i] + nums[j] + nums[left] + nums[right];
                    if (sum > target) {
                        right--; // 大了往左去
                    } else if (sum < target) {
                        left++; // 小了往右去
                    } else {
                        res.add(Arrays.asList(nums[i], nums[j], nums[left], nums[right]));
                        
                        //去重
                        while (left < right && nums[left] == nums [left + 1]) left++;
                        while (left < right && nums[right] == nums[right - 1]) right--;

                        left++;
                        right--;
                    }
                }
            }
        }
        return res;
    }
}
```
