# Day 10: 代码随想录算法训练营

## Topic:
- Queue
- Heap

## Summary:
- 单调队列（队列已经排好序了）
- 大小顶堆要多熟悉还是很少用 写代码的时候会卡
- lambda 表达式 多练
- 到了今天查java 文档的速度倒是越来越快 加油



## Leetcode Problem 滑动窗口最大值

Leetcode 239
```java
class MyQueue {
    Deque<Integer> queue;

    public MyQueue(){
        queue = new ArrayDeque<>();
    }

    void poll(int num) {
        if (!queue.isEmpty() && queue.peek() == num) {
            queue.poll();
        }
    }

    void add(int num) {
        while (!queue.isEmpty() && queue.getLast() < num) {
            queue.removeLast();
        }

        queue.add(num);
    }

    int peek() {
        return queue.peek();
    }
}

class Solution {

    public int[] maxSlidingWindow(int[] nums, int k) {
        MyQueue queue = new MyQueue();
        int[] res = new int[nums.length - k + 1];
        int index = 0;
        for (int i = 0; i < k; i++) {
            queue.add(nums[i]);
        }
        res[index++] = queue.peek();

        for (int i = k; i < nums.length; i++) {
            queue.poll(nums[i-k]);
            queue.add(nums[i]);
            res[index++] = queue.peek();
        }


        return res;


    }
}
```


Leetcode 347 前 K 个高频元素

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        // 先记录元素频率 -> 大小堆找k

        Map<Integer, Integer> map = new HashMap<>();

        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        PriorityQueue<int[]> pq = new PriorityQueue<>((pair1, pair2) -> pair2[1] - pair1[1]);

        for (Map.Entry<Integer, Integer> pair : map.entrySet()) {
            pq.add(new int[]{pair.getKey(), pair.getValue()});
        }

        int[] res = new int[k];
        for (int i = 0; i < k; i++) {
            res[i] = pq.remove()[0];
        }

        return res;
    }
}
```
