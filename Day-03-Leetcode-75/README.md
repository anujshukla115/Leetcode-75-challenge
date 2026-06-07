# Day 3 - Kids With the Greatest Number of Candies

## 🔗 Problem Link

https://leetcode.com/problems/kids-with-the-greatest-number-of-candies/

## 📌 Problem Statement

There are `n` kids with candies. You are given an integer array `candies`, where each `candies[i]` represents the number of candies the `iᵗʰ` kid has, and an integer `extraCandies` representing the number of extra candies that you can give to a kid.

Return a boolean array `result` of length `n`, where `result[i]` is `true` if, after giving the `iᵗʰ` kid all the `extraCandies`, they will have the greatest number of candies among all the kids, or at least tie for the greatest number of candies. Otherwise, return `false`.

### Example

```cpp
Input:
candies = [2,3,5,1,3]
extraCandies = 3

Output:
[true,true,true,false,true]
```

## 💡 Approach

1. Find the maximum number of candies currently possessed by any kid.
2. Traverse the `candies` array.
3. For each kid, add `extraCandies` to their current candies.
4. Compare the result with the maximum candy count.
5. If the new count is greater than or equal to the maximum, store `true`; otherwise, store `false`.
6. Return the resulting boolean array.

## ✅ C++ Solution

```cpp
class Solution {
public:
    vector<bool> kidsWithCandies(vector<int>& candies, int extraCandies) {

        int maxCandy = *max_element(candies.begin(), candies.end());

        vector<bool> result;

        for (int candy : candies) {
            result.push_back(candy + extraCandies >= maxCandy);
        }

        return result;
    }
};
```

## ⏱️ Time Complexity

* Finding the maximum element: **O(n)**
* Traversing the array: **O(n)**

**Overall Time Complexity:** `O(n)`

## 💾 Space Complexity

* Result vector stores `n` boolean values.

**Space Complexity:** `O(n)`

## 🎯 Key Learning

This problem teaches the importance of **precomputing frequently used values**. By finding the maximum candy count once and reusing it, we avoid unnecessary repeated calculations and achieve an efficient `O(n)` solution.

---

### 🚀 LeetCode 75 Challenge

**Day 3 Completed ✅**
