# Day 1 - Merge Strings Alternately

## Problem Statement

You are given two strings `word1` and `word2`.

Merge the strings by adding letters in alternating order, starting with `word1`. If a string is longer than the other, append the additional letters onto the end of the merged string.

### Example

**Input**

```cpp
word1 = "abc"
word2 = "pqr"
```

**Output**

```cpp
"apbqcr"
```

---

## Approach

### Two Pointer Approach

* Initialize two pointers `i` and `j` for `word1` and `word2`.
* Traverse both strings simultaneously.
* Add one character from `word1` and then one character from `word2` to the result string.
* Continue until one of the strings is exhausted.
* Append the remaining characters from the longer string using `substr()`.

---

## Algorithm

1. Create an empty string `ans`.
2. Initialize:

   ```cpp
   i = 0
   j = 0
   ```
3. While both strings have characters remaining:

   * Add `word1[i]`
   * Add `word2[j]`
   * Increment both pointers
4. Append the remaining part of `word1` (if any).
5. Append the remaining part of `word2` (if any).
6. Return the final merged string.

---

## C++ Solution

```cpp
class Solution {
public:
    string mergeAlternately(string word1, string word2) {
        string ans = "";

        int i = 0, j = 0;
        int n = word1.size();
        int m = word2.size();

        while(i < n && j < m) {
            ans += word1[i++];
            ans += word2[j++];
        }

        if(i < n) ans += word1.substr(i);
        if(j < m) ans += word2.substr(j);

        return ans;
    }
};
```

---

## Complexity Analysis

### Time Complexity

```text
O(n + m)
```

Where:

* `n` = length of `word1`
* `m` = length of `word2`

Each character is processed exactly once.

### Space Complexity

```text
O(n + m)
```

The result string stores all characters from both input strings.

---

## Key Learnings

* Introduction to the Two Pointer technique.
* String traversal using indices.
* Using `substr()` to extract remaining characters.
* Importance of handling strings with different lengths.
* Converting problem logic into code through step-by-step thinking.

---

## Status

✅ Solved

📅 Day 1 of LeetCode 75 Challenge
