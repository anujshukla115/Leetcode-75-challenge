# LeetCode 75 - Day 10

## Problem: Move Zeroes

**Problem Link:** https://leetcode.com/problems/move-zeroes/

---

## Problem Statement

Given an integer array `nums`, move all `0`s to the end of it while maintaining the relative order of the non-zero elements.

You must do this in-place without making a copy of the array.

---

## Approach

### My Approach

1. Find the index of the first zero in the array.
2. If no zero exists, the array is already in the correct form.
3. Use another pointer `j` to search for non-zero elements after the first zero.
4. Whenever a non-zero element is found, swap it with the zero pointed to by `i`.
5. Move `i` forward to the next zero position.
6. Continue until the end of the array.

This ensures:

* All non-zero elements remain in their original relative order.
* All zeroes are moved to the end.
* The operation is performed in-place.

---

## Dry Run

Input:

```cpp
[0,1,0,3,12]
```

Find first zero:

```cpp
i = 0
j = 1
```

Swap:

```cpp
[1,0,0,3,12]
```

Move `i` to next zero.

Swap with `3`:

```cpp
[1,3,0,0,12]
```

Move `i` to next zero.

Swap with `12`:

```cpp
[1,3,12,0,0]
```

Output achieved.

---

## Code

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int n = nums.size();
        int i = n;

        for(int k = 0; k < n; k++)
        {
            if(nums[k] == 0)
            {
                i = k;
                break;
            }
        }

        if(i == n)
        {
            return;
        }

        int j = i + 1;

        while(j < n)
        {
            if(nums[j] == 0)
            {
                j++;
            }
            else
            {
                swap(nums[i], nums[j]);

                while(i < n && nums[i] != 0)
                {
                    i++;
                }

                j++;
            }
        }
    }
};
```

---

## Complexity Analysis

### Time Complexity

O(n)

* Finding first zero: O(n)
* Traversing with pointers: O(n)
* Each pointer moves only forward.

### Space Complexity

O(1)

* No extra data structure is used.

---

## Key Learning

* Two Pointer Technique
* In-place Array Manipulation
* Difference between assignment (`=`) and comparison (`==`)
* Maintaining relative order while modifying an array
* Complexity analysis of multiple forward-moving pointers
