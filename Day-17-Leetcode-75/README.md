# Day 17 - Longest Subarray of 1's After Deleting One Element

## Problem Link

🔗 https://leetcode.com/problems/longest-subarray-of-1s-after-deleting-one-element/

---

## Problem Statement

Given a binary array `nums`, you should delete exactly one element from it.

Return the size of the longest non-empty subarray containing only `1`s in the resulting array.

---

## Approach: Sliding Window (Optimal)

### Intuition

Since we are allowed to delete exactly one element, our sliding window can contain **at most one `0`**.

* Expand the window using the `right` pointer.
* If a `0` is encountered, increment the zero count.
* If the window contains more than one `0`, shrink the window from the left until it becomes valid again.
* Since one element must always be deleted, the effective length of the current window becomes:

```cpp
right - left
```

instead of:

```cpp
right - left + 1
```

---

## Algorithm

1. Initialize:

   * `left = 0`
   * `maxlen = 0`
   * `zeros = 0`

2. Traverse the array using the `right` pointer.

3. If `nums[right]` is `0`, increment `zeros`.

4. While `zeros > 1`:

   * If `nums[left]` is `0`, decrement `zeros`.
   * Move `left` forward.

5. Update:

```cpp
maxlen = max(maxlen, right - left);
```

6. Return `maxlen`.

---

## Dry Run

### Input

```cpp
nums = [1,1,0,1]
```

| right | nums[right] | zeros | left | maxlen |
| ----- | ----------- | ----- | ---- | ------ |
| 0     | 1           | 0     | 0    | 0      |
| 1     | 1           | 0     | 0    | 1      |
| 2     | 0           | 1     | 0    | 2      |
| 3     | 1           | 1     | 0    | 3      |

### Output

```cpp
3
```

---

## C++ Solution

```cpp
class Solution {
public:
    int longestSubarray(vector<int>& nums) {

        int left = 0;
        int maxlen = 0;
        int zeros = 0;

        for(int right = 0; right < nums.size(); right++)
        {
            if(nums[right] == 0)
            {
                zeros++;
            }

            while(zeros > 1)
            {
                if(nums[left] == 0)
                {
                    zeros--;
                }

                left++;
            }

            maxlen = max(maxlen, right - left);
        }

        return maxlen;
    }
};
```

---

## Complexity Analysis

### Time Complexity: `O(n)`

* The `right` pointer traverses the array once.
* The `left` pointer also moves forward at most once.
* Each element is processed at most twice.

Overall Time Complexity:

```cpp
O(n + n) = O(2n) ≈ O(n)
```

### Space Complexity: `O(1)`

Only a few variables are used:

```cpp
left, right, zeros, maxlen
```

No extra data structure is required.

---

## Key Learning

* Sliding Window is useful for problems involving contiguous subarrays.
* When a problem allows deleting or replacing a limited number of elements, maintain a window satisfying that constraint.
* Always carefully interpret conditions like **"delete exactly one element"**.
