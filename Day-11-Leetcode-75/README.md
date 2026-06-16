# Day 11 - LeetCode 392: Is Subsequence

## Problem Link

https://leetcode.com/problems/is-subsequence/

---

## Problem Statement

Given two strings `s` and `t`, return `true` if `s` is a subsequence of `t`, or `false` otherwise.

A subsequence of a string is a new string formed from the original string by deleting some (or no) characters without changing the relative order of the remaining characters.

---

## Approach

### Intuition

To determine whether `s` is a subsequence of `t`, we need to check if all characters of `s` appear in `t` in the same order.

Using two pointers:

* Pointer `i` traverses string `s`
* Pointer `j` traverses string `t`

If characters match, move both pointers.

If characters do not match, move only the pointer of `t` and continue searching.

If all characters of `s` are matched, then `s` is a subsequence of `t`.

---

## Dry Run

### Input

```cpp
s = "abc"
t = "ahbgdc"
```

| i | j | s[i] | t[j] | Action           |
| - | - | ---- | ---- | ---------------- |
| 0 | 0 | a    | a    | Match → i++, j++ |
| 1 | 1 | b    | h    | Move j           |
| 1 | 2 | b    | b    | Match → i++, j++ |
| 2 | 3 | c    | g    | Move j           |
| 2 | 4 | c    | d    | Move j           |
| 2 | 5 | c    | c    | Match → i++, j++ |

Now:

```cpp
i == s.size()
```

Return:

```cpp
true
```

---

## Code

```cpp
class Solution {
public:
    bool isSubsequence(string s, string t) {

        int i = 0;
        int j = 0;

        while(i < s.size() && j < t.size())
        {
            if(s[i] == t[j])
            {
                i++;
                j++;
            }
            else
            {
                j++;
            }
        }

        return i == s.size();
    }
};
```

---

## Complexity Analysis

### Time Complexity

```text
O(n)
```

where `n` is the length of `t`.

### Space Complexity

```text
O(1)
```

---

## Key Learning

* Subsequence is different from substring.
* Two pointers help efficiently compare ordered sequences.
* When characters don't match, continue searching in the larger string instead of returning false immediately.
