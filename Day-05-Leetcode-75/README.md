# LeetCode 75 - Day 5

# 345. Reverse Vowels of a String

🔗 Problem Link: https://leetcode.com/problems/reverse-vowels-of-a-string/

## Problem Statement

Given a string `s`, reverse only all the vowels in the string and return it.

The vowels are:

```text
a, e, i, o, u
A, E, I, O, U
```

### Example 1

```text
Input: s = "hello"
Output: "holle"
```

### Example 2

```text
Input: s = "leetcode"
Output: "leotcede"
```

---

## Approach (Two Pointers)

We use the Two Pointer technique to efficiently reverse only the vowels in the string.

### Steps

1. Store all vowels in an `unordered_set` for quick lookup.
2. Initialize two pointers:
   - `i` at the beginning of the string.
   - `j` at the end of the string.
3. Move `i` forward until a vowel is found.
4. Move `j` backward until a vowel is found.
5. Swap the vowels at positions `i` and `j`.
6. Move both pointers inward.
7. Repeat until `i >= j`.
8. Return the modified string.

### Why This Works

- The first vowel should be swapped with the last vowel.
- The second vowel should be swapped with the second last vowel.
- Two pointers allow us to find and swap these vowels efficiently in a single traversal.

---

## C++ Solution

```cpp
class Solution {
public:
    string reverseVowels(string s) {

        unordered_set<char> vowel = {
            'a','e','i','o','u',
            'A','E','I','O','U'
        };

        int i = 0;
        int j = s.size() - 1;

        while(i < j)
        {
            while(i < j && vowel.find(s[i]) == vowel.end())
            {
                i++;
            }

            while(i < j && vowel.find(s[j]) == vowel.end())
            {
                j--;
            }

            swap(s[i], s[j]);

            i++;
            j--;
        }

        return s;
    }
};
```

---

## Dry Run

### Input

```text
hello
```

### Process

```text
h e l l o
  ^     ^

Swap e and o

h o l l e
```

### Output

```text
holle
```

---

## Complexity Analysis

### Time Complexity

```text
O(n)
```

Each character is visited at most once by either pointer.

### Space Complexity

```text
O(1)
```

The vowel set contains only 10 fixed characters, so the extra space is constant.

---

## Key Concepts Learned

- Two Pointers
- String Manipulation
- Hash Set (`unordered_set`)
- Efficient In-Place Swapping

---

⭐ LeetCode 75 Challenge - Day 5 Complete
