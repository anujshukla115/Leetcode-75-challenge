# LeetCode 75 - Day 13

## 1679. Max Number of K-Sum Pairs

### Problem Link

https://leetcode.com/problems/max-number-of-k-sum-pairs/

---

## Problem Statement

You are given an integer array `nums` and an integer `k`.

In one operation, you can pick two numbers from the array whose sum equals `k` and remove them from the array.

Return the maximum number of operations you can perform.

### Example

**Input:**

```text
nums = [1,2,3,4], k = 5
```

**Output:**

```text
2
```

**Explanation:**

* Remove (1,4)
* Remove (2,3)

Total operations = 2

---

## My Approach (HashMap / Frequency Map)

### Intuition

For every number `nums[i]`, we need another number:

```text
need = k - nums[i]
```

If the required number (`need`) has already appeared before, we can form a valid pair.

To efficiently check whether the required number exists, we use an `unordered_map` to store frequencies of previously seen numbers.

### Algorithm

1. Create a frequency map.
2. Traverse the array once.
3. For each element:

   * Calculate `need = k - nums[i]`.
   * If `need` exists in the map:

     * Form a pair.
     * Increment operation count.
     * Decrease frequency of `need`.
   * Otherwise:

     * Store current number in the map.
4. Return total operations.

---

## Dry Run

### Input

```text
nums = [1,2,3,4]
k = 5
```

| Current Number | Need | Action     | Count |
| -------------- | ---- | ---------- | ----- |
| 1              | 4    | Store 1    | 0     |
| 2              | 3    | Store 2    | 0     |
| 3              | 2    | Pair Found | 1     |
| 4              | 1    | Pair Found | 2     |

Final Answer:

```text
2
```

---

## C++ Solution

```cpp
class Solution {
public:
    int maxOperations(vector<int>& nums, int k) {

        unordered_map<int,int> mp;
        int count = 0;

        for(int i = 0; i < nums.size(); i++)
        {
            int need = k - nums[i];

            if(mp[need] > 0)
            {
                count++;
                mp[need]--;
            }
            else
            {
                mp[nums[i]]++;
            }
        }

        return count;
    }
};
```

---

## Complexity Analysis

### Time Complexity

```text
O(n)
```

* We traverse the array only once.
* HashMap operations take O(1) average time.

### Space Complexity

```text
O(n)
```

* In the worst case, all elements may be stored in the HashMap.

---

## What I Learned

* How to use the complement technique (`k - nums[i]`).
* Efficient pair finding using a HashMap.
* Difference between using an index (`i`) and an element value (`nums[i]`).
* Converting a brute-force O(n²) solution into an optimal O(n) solution.

### Day 13 Complete ✅

Problem: 1679. Max Number of K-Sum Pairs
Approach: HashMap + Complement Technique
Time Complexity: O(n)
Space Complexity: O(n)
