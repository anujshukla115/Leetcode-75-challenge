# 724. Find Pivot Index

## Problem Link

https://leetcode.com/problems/find-pivot-index/

---

## Problem Statement

Given an array of integers `nums`, calculate the **pivot index** of this array.

The **pivot index** is the index where the sum of all the numbers strictly to the left of the index is equal to the sum of all the numbers strictly to the right of the index.

* If the pivot index exists, return the leftmost pivot index.
* If no such index exists, return `-1`.

---

## Approach (Optimal - Prefix Sum)

### Intuition

For every index, we need:

* `leftSum` → Sum of elements on the left side.
* `rightSum` → Sum of elements on the right side.

Instead of calculating left and right sums repeatedly for every index, we first compute the total sum of the array.

For each index:

```cpp
rightSum = totalSum - leftSum - nums[i]
```

If:

```cpp
leftSum == rightSum
```

then the current index is the pivot index.

After checking the current index, update:

```cpp
leftSum += nums[i];
```

---

## Dry Run

### Input

```cpp
nums = [1,7,3,6,5,6]
```

### Total Sum

```cpp
totalSum = 28
```

| Index | nums[i] | leftSum | rightSum | Pivot? |
| ----- | ------- | ------- | -------- | ------ |
| 0     | 1       | 0       | 27       | ❌      |
| 1     | 7       | 1       | 20       | ❌      |
| 2     | 3       | 8       | 17       | ❌      |
| 3     | 6       | 11      | 11       | ✅      |

Therefore:

```cpp
Answer = 3
```

---

## Code

```cpp
class Solution {
public:
    int pivotIndex(vector<int>& nums) {

        int leftsum = 0;
        int totalsum = 0;

        for(int i = 0; i < nums.size(); i++)
        {
            totalsum += nums[i];
        }

        for(int i = 0; i < nums.size(); i++)
        {
            int rightsum = totalsum - leftsum - nums[i];

            if(leftsum == rightsum)
            {
                return i;
            }

            leftsum += nums[i];
        }

        return -1;
    }
};
```

---

## Complexity Analysis

### Time Complexity

```cpp
O(n)
```

* First traversal to calculate `totalSum` → `O(n)`
* Second traversal to find pivot index → `O(n)`

Overall:

```cpp
O(n)
```

### Space Complexity

```cpp
O(1)
```

Only a few extra variables (`leftsum`, `rightsum`, `totalsum`) are used.

---

## Key Learning

* Prefix Sum helps in avoiding repeated calculations.
* Maintaining a running `leftSum` allows us to find the pivot index efficiently.
* Always look for ways to reuse previously computed information to optimize brute-force solutions.
