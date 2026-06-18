# Day 14 - Maximum Average Subarray I (LeetCode 643)

## Problem Link

https://leetcode.com/problems/maximum-average-subarray-i/

---

## Problem Statement

Given an integer array `nums` consisting of `n` elements and an integer `k`, find a contiguous subarray whose length is equal to `k` and has the maximum average value. Return this value.

---

## Approach: Sliding Window

Since the size of the subarray is fixed (`k`), we can use the Sliding Window technique.

### Steps

1. Calculate the sum of the first `k` elements.
2. Store it as the current maximum sum.
3. Slide the window one element at a time:

   * Remove the element leaving the window.
   * Add the new element entering the window.
4. Update the maximum sum whenever a larger sum is found.
5. Return `maxSum / k` as the maximum average.

This avoids recalculating the sum of every subarray and reduces the time complexity significantly.

---

## Dry Run

### Input

```text
nums = [1,12,-5,-6,50,3]
k = 4
```

### First Window

```text
[1,12,-5,-6]
```

Sum:

```text
1 + 12 - 5 - 6 = 2
```

```text
maxSum = 2
```

### Slide Window

Remove `1`, Add `50`

```text
New Sum = 2 - 1 + 50 = 51
maxSum = 51
```

### Slide Again

Remove `12`, Add `3`

```text
New Sum = 51 - 12 + 3 = 42
maxSum = 51
```

### Result

```text
Maximum Average = 51 / 4 = 12.75
```

---

## Code (C++)

```cpp
class Solution {
public:
    double findMaxAverage(vector<int>& nums, int k) {

        int n = nums.size();
        int sum = 0;

        for(int i = 0; i < k; i++)
        {
            sum += nums[i];
        }

        int maxsum = sum;

        for(int i = k; i < n; i++)
        {
            sum = sum - nums[i-k] + nums[i];
            maxsum = max(maxsum, sum);
        }

        return (double)maxsum / k;
    }
};
```

---

## Complexity Analysis

### Time Complexity

* First window calculation: `O(k)`
* Sliding the window: `O(n-k)`

Total:

```text
O(k) + O(n-k) = O(n)
```

### Space Complexity

Only a few extra variables are used.

```text
O(1)
```

---

## Key Learning

* When the subarray size is fixed, Sliding Window is often the optimal approach.
* Instead of recalculating the sum for every subarray, reuse the previous window sum.
* Sliding Window can reduce the complexity from `O(n*k)` to `O(n)`.

### LeetCode 75 Challenge

✅ Day 14 Completed

Problem: Maximum Average Subarray I (LeetCode 643)

Technique Learned: Sliding Window
