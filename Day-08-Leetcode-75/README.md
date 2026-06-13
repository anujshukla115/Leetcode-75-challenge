# LeetCode 75 - Day 08

# 334. Increasing Triplet Subsequence

🔗 Problem Link: https://leetcode.com/problems/increasing-triplet-subsequence/

---

## Problem Statement

Given an integer array `nums`, return `true` if there exists a triple of indices `(i, j, k)` such that:

```text
i < j < k
```

and

```text
nums[i] < nums[j] < nums[k]
```

If no such triplet exists, return `false`.

### Example 1

```cpp
Input: nums = [1,2,3,4,5]
Output: true
```

### Example 2

```cpp
Input: nums = [5,4,3,2,1]
Output: false
```

### Example 3

```cpp
Input: nums = [2,1,5,0,4,6]
Output: true
```

---

## Approach (optimal)

We maintain two variables:

* `first` → Smallest element found so far.
* `second` → Smallest element greater than `first`.

### Steps

1. Initialize `first` and `second` with `INT_MAX`.
2. Traverse the array.
3. If the current element is smaller than or equal to `first`, update `first`.
4. Otherwise, if the current element is smaller than or equal to `second`, update `second`.
5. If the current element is greater than both `first` and `second`, an increasing triplet has been found.
6. Return `true`.
7. If traversal finishes without finding a triplet, return `false`.

### Dry Run

```cpp
nums = [2,1,5,0,4,6]
```

| Current | First | Second |
| ------- | ----- | ------ |
| 2       | 2     | INF    |
| 1       | 1     | INF    |
| 5       | 1     | 5      |
| 0       | 0     | 5      |
| 4       | 0     | 4      |
| 6       | 0     | 4      |

Since:

```text
0 < 4 < 6
```

An increasing triplet exists, so return `true`.

---

## My Solution (C++)

```cpp
class Solution {
public:
    bool increasingTriplet(vector<int>& nums) {
        
        int first = INT_MAX;
        int second = INT_MAX;

        for(int i = 0; i < nums.size(); i++)
        {
            if(nums[i] <= first)
            {
                first = nums[i];
            }
            else if(nums[i] <= second)
            {
                second = nums[i];
            }
            else
            {
                return true;
            }
        }

        return false;
    }
};
```

---

## Complexity Analysis

### Time Complexity

```text
O(n)
```

We traverse the array only once.

### Space Complexity

```text
O(1)
```

Only two extra variables (`first` and `second`) are used.

---

## Key Learning

* Greedy algorithms often work by maintaining the best possible candidates.
* Keeping the smallest possible `first` and `second` maximizes the chance of finding a valid third element.
* This problem can be solved in linear time and constant space without using extra arrays.
