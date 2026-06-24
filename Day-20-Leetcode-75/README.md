# Day 20 - LeetCode 2215: Find the Difference of Two Arrays

## Problem Link

🔗 https://leetcode.com/problems/find-the-difference-of-two-arrays/

---

## Problem Statement

Given two 0-indexed integer arrays `nums1` and `nums2`, return a list `answer` of size 2 where:

* `answer[0]` is a list of all distinct integers in `nums1` which are not present in `nums2`.
* `answer[1]` is a list of all distinct integers in `nums2` which are not present in `nums1`.

The integers in the lists may be returned in any order.

---

## Approach (Optimal - Using Unordered Set)

### Intuition

* We only need to know whether an element exists in the other array or not.
* Duplicate elements should not appear in the answer.
* `unordered_set` automatically removes duplicates and provides average **O(1)** lookup time.

### Algorithm

1. Store all elements of `nums1` in `unordered_set s1`.
2. Store all elements of `nums2` in `unordered_set s2`.
3. Traverse `s1`:

   * If an element is not present in `s2`, add it to `v1`.
4. Traverse `s2`:

   * If an element is not present in `s1`, add it to `v2`.
5. Push `v1` and `v2` into the final answer vector and return it.

---

## Dry Run

### Input

```cpp
nums1 = [1,2,3]
nums2 = [2,4,6]
```

### Step 1: Create Sets

```cpp
s1 = {1,2,3}
s2 = {2,4,6}
```

### Step 2: Traverse `s1`

* `1` → not present in `s2` → add to `v1`
* `2` → present in `s2` → skip
* `3` → not present in `s2` → add to `v1`

```cpp
v1 = [1,3]
```

### Step 3: Traverse `s2`

* `2` → present in `s1` → skip
* `4` → not present in `s1` → add to `v2`
* `6` → not present in `s1` → add to `v2`

```cpp
v2 = [4,6]
```

### Final Answer

```cpp
[[1,3],[4,6]]
```

---

## C++ Solution

```cpp
class Solution {
public:
    vector<vector<int>> findDifference(vector<int>& nums1, vector<int>& nums2) {

        unordered_set<int> s1(nums1.begin(), nums1.end());
        unordered_set<int> s2(nums2.begin(), nums2.end());

        vector<int> v1, v2;
        vector<vector<int>> ans;

        for (auto x : s1) {
            if (s2.find(x) == s2.end()) {
                v1.push_back(x);
            }
        }

        for (auto x : s2) {
            if (s1.find(x) == s1.end()) {
                v2.push_back(x);
            }
        }

        ans.push_back(v1);
        ans.push_back(v2);

        return ans;
    }
};
```

---

## Complexity Analysis

### Time Complexity

* Creating both sets: **O(n + m)**
* Traversing both sets: **O(n + m)**

**Overall Time Complexity:**

```cpp
O(n + m)
```

where:

* `n` = size of `nums1`
* `m` = size of `nums2`

### Space Complexity

* Two unordered sets store unique elements.
* Additional vectors store the answer.

**Overall Space Complexity:**

```cpp
O(n + m)
```

---

## Key Learning

* Use `unordered_set` when only presence/absence checking is required.
* `unordered_set` automatically removes duplicates.
* Average lookup time in `unordered_set` is **O(1)**.
* Always analyze whether frequency counting is actually needed before choosing `unordered_map`.
