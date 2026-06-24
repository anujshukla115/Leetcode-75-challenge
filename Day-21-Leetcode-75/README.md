# Day 21 - LeetCode 1207: Unique Number of Occurrences

## Problem Link

🔗 https://leetcode.com/problems/unique-number-of-occurrences/

---

## Problem Statement

Given an array of integers `arr`, return `true` if the number of occurrences of each value in the array is unique, or `false` otherwise.

---

## Approach (Optimal - Hash Map + Hash Set)

### Intuition

* First, count the frequency of every element in the array.
* Then, check whether these frequencies are unique or not.
* If any frequency appears more than once, return `false`.
* Otherwise, return `true`.

### Algorithm

1. Create an `unordered_map<int, int>` to store the frequency of each element.
2. Traverse the array and update frequencies in the map.
3. Create an `unordered_set<int>` to store frequencies.
4. Traverse the frequency map:

   * If a frequency already exists in the set, return `false`.
   * Otherwise, insert the frequency into the set.
5. If all frequencies are unique, return `true`.

---

## Dry Run

### Input

```cpp
arr = [1,2,2,1,1,3]
```

### Step 1: Build Frequency Map

```text
1 -> 3
2 -> 2
3 -> 1
```

### Step 2: Check Unique Frequencies

Initially:

```text
st = {}
```

Process frequencies:

```text
3 -> not present -> insert
st = {3}

2 -> not present -> insert
st = {3,2}

1 -> not present -> insert
st = {3,2,1}
```

No duplicate frequencies found.

### Output

```cpp
true
```

---

## C++ Solution

```cpp
class Solution {
public:
    bool uniqueOccurrences(vector<int>& arr) {

        unordered_map<int, int> mp;
        unordered_set<int> st;

        for(auto x : arr)
        {
            mp[x]++;
        }

        for(auto x : mp)
        {
            if(st.find(x.second) != st.end())
            {
                return false;
            }

            st.insert(x.second);
        }

        return true;
    }
};
```

---

## Complexity Analysis

### Time Complexity

* Traversing the array to build the frequency map: **O(n)**
* Traversing the map and checking frequencies in the set: **O(n)** (in the worst case)

**Overall Time Complexity:**

```text
O(n)
```

where `n` is the size of the array.

### Space Complexity

* `unordered_map` stores frequencies of elements.
* `unordered_set` stores frequencies.

**Overall Space Complexity:**

```text
O(n)
```

---

## Key Learning

* Use `unordered_map` when frequency counting is required.
* Use `unordered_set` to efficiently detect duplicates.
* Hash-based data structures provide average **O(1)** insertion and lookup.
* Always analyze whether you need element uniqueness or frequency uniqueness.
