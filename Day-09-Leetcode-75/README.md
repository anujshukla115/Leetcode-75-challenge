# LeetCode 75 - Day 09

# 443. String Compression

🔗 Problem Link: https://leetcode.com/problems/string-compression/

---

## Problem Statement

Given an array of characters `chars`, compress it using the following algorithm:

* Begin with an empty string `s`.
* For each group of consecutive repeating characters in `chars`:

  * Append the character to `s`.
  * If the group's length is greater than 1, append the length of the group.
* The compressed string should be stored back into the input character array `chars`.
* Return the new length of the compressed array.

The algorithm must use only constant extra space.

---

## Example 1

```cpp
Input: chars = ['a','a','b','b','c','c','c']

Output: 6

Compressed Array:
['a','2','b','2','c','3']
```

---

## Example 2

```cpp
Input: chars = ['a']

Output: 1

Compressed Array:
['a']
```

---

## Example 3

```cpp
Input: chars = ['a','b','b','b','b','b','b','b','b','b','b','b','b']

Output: 4

Compressed Array:
['a','b','1','2']
```

---

## Approach (Two Pointers)

We use two pointers:

### Read Pointer (`read`)

* Traverses the array.
* Counts the frequency of consecutive identical characters.

### Write Pointer (`write`)

* Writes the compressed result back into the original array.

### Steps

1. Initialize `read` and `write` to 0.
2. For each group of consecutive characters:

   * Store the current character.
   * Count how many times it appears consecutively.
3. Write the character at the `write` position.
4. If the count is greater than 1:

   * Convert the count to a string using `to_string()`.
   * Write each digit individually into the array.
5. Continue until all groups are processed.
6. Return `write`, which represents the compressed array length.

---

## Dry Run

### Input

```cpp
chars = ['a','a','b','b','c','c','c']
```

### Processing

| Group | Count | Written |
| ----- | ----- | ------- |
| aa    | 2     | a2      |
| bb    | 2     | b2      |
| ccc   | 3     | c3      |

### Final Array

```cpp
['a','2','b','2','c','3']
```

### Returned Length

```cpp
6
```

---

## My Solution (C++)

```cpp
class Solution {
public:
    int compress(vector<char>& chars) {
        int write = 0;
        int read = 0;
        int n = chars.size();

        while(read < n)
        {
            char current = chars[read];
            int count = 0;

            while(read < n && chars[read] == current)
            {
                count++;
                read++;
            }

            chars[write] = current;
            write++;

            if(count > 1)
            {
                string s = to_string(count);

                for(char ch : s)
                {
                    chars[write] = ch;
                    write++;
                }
            }
        }

        return write;
    }
};
```

---

## Complexity Analysis

### Time Complexity

```text
O(n)
```

Each character is processed exactly once.

### Space Complexity

```text
O(1)
```

Only constant extra space is used. The compression is performed in-place.

---

## Key Learning

* Learned how to use the Two Pointer technique for in-place array modification.
* Used `read` pointer for traversing groups and `write` pointer for storing compressed results.
* Learned how to handle multi-digit frequencies using `to_string()`.
* Understood how to solve compression problems with constant extra space.

---

### LeetCode 75 Progress

✅ Day 09 Completed

**Problem:** 443. String Compression
**Approach:** Two Pointers (Read & Write)
**Time Complexity:** O(n)
**Space Complexity:** O(1)
