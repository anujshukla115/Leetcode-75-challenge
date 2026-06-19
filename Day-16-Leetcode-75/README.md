# 1004. Max Consecutive Ones III

## Problem Link

https://leetcode.com/problems/max-consecutive-ones-iii/

---

## Problem Statement

Given a binary array `nums` and an integer `k`, return the maximum number of consecutive 1's in the array if you can flip at most `k` zeros.

---

## Approach

This problem can be solved using a **Variable Size Sliding Window**.

### Idea

* Maintain a window containing at most `k` zeros.
* Expand the window using the right pointer.
* Count the number of zeros in the current window.
* If the number of zeros exceeds `k`, shrink the window from the left.
* Track the maximum valid window length.

The window always represents a subarray that can be converted entirely into 1s using at most `k` flips.

---

## Dry Run

Input:

nums = [1,1,1,0,0,0,1,1,1,1,0]
k = 2

Window expands:

[1,1,1,0,0]

zeros = 2

Valid window length = 5

Next:

[1,1,1,0,0,0]

zeros = 3

Invalid

Move left pointer until:

zeros ≤ 2

Continue updating maximum length.

Answer = 6

---

## Code

```cpp
class Solution {
public:
    int longestOnes(vector<int>& nums, int k) {
        int left = 0;
        int maxlen = 0;
        int zerocount = 0;

        for(int right = 0; right < nums.size(); right++)
        {
            if(nums[right] == 0)
            {
                zerocount++;
            }

            while(zerocount > k)
            {
                if(nums[left] == 0)
                {
                    zerocount--;
                }

                left++;
            }

            maxlen = max(maxlen, right - left + 1);
        }

        return maxlen;
    }
};
```

---

## Time Complexity

O(n)

Each element is visited at most twice:

* Once by right pointer
* Once by left pointer

Therefore:

O(n)

---

## Space Complexity

O(1)

Only a few variables are used.

---

## Key Learning

* Variable Size Sliding Window
* Expand and shrink window technique
* Maintaining valid window conditions
* Longest valid subarray problems
* Two Pointer optimization
