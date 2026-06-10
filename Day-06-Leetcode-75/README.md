# LeetCode 75 - Day 6
# 151. Reverse Words in a String

🔗 Problem Link: https://leetcode.com/problems/reverse-words-in-a-string/

---

## Problem Statement

Given an input string `s`, reverse the order of the words.

A word is defined as a sequence of non-space characters. The returned string should:

- Contain the words in reverse order.
- Have only a single space separating words.
- Not contain leading or trailing spaces.

### Example 1

```text
Input: s = "the sky is blue"
Output: "blue is sky the"
```

### Example 2

```text
Input: s = "  hello world  "
Output: "world hello"
```

### Example 3

```text
Input: s = "a good   example"
Output: "example good a"
```

---

## Approach

### Step 1: Remove Extra Spaces

Traverse the string and:

- Skip leading spaces.
- Copy characters of each word.
- Skip multiple spaces between words.
- Add only one space between consecutive words.

This creates a cleaned string without extra spaces.

### Step 2: Reverse the Entire String

Reverse the cleaned string.

Example:

```text
hello world
↓
dlrow olleh
```

The word order becomes reversed, but each word itself is also reversed.

### Step 3: Reverse Each Word

Traverse the reversed string and reverse every individual word.

Example:

```text
dlrow olleh
↓
world hello
```

This restores each word while keeping the word order reversed.

---

## Code

```cpp
class Solution {
public:
    string reverseWords(string s) {
        int n = s.size();
        int i = 0;
        string temp;

        while(i < n)
        {
            while(i < n && s[i] == ' ')
                i++;

            while(i < n && s[i] != ' ')
            {
                temp += s[i];
                i++;
            }

            while(i < n && s[i] == ' ')
                i++;

            if(i < n)
                temp += ' ';
        }

        reverse(temp.begin(), temp.end());

        int start = 0;

        for(int end = 0; end <= temp.size(); end++)
        {
            if(end == temp.size() || temp[end] == ' ')
            {
                reverse(temp.begin() + start,
                        temp.begin() + end);

                start = end + 1;
            }
        }

        return temp;
    }
};
```

---

## Dry Run

### Input

```text
"  a good   example  "
```

### After Removing Extra Spaces

```text
"a good example"
```

### After Reversing Entire String

```text
"elpmaxe doog a"
```

### After Reversing Each Word

```text
"example good a"
```

### Output

```text
"example good a"
```

---

## Time Complexity

### Removing Extra Spaces

```text
O(n)
```

### Reversing Entire String

```text
O(n)
```

### Reversing Each Word

```text
O(n)
```

### Total Time Complexity

```text
O(n)
```

---

## Space Complexity

A temporary string `temp` is used to store the cleaned string.

```text
O(n)
```

---

## Key Learning

- Handling leading, trailing, and multiple spaces is the main challenge.
- Reversing the entire string first reverses the word order.
- Reversing each word restores the original characters.
- Efficient solution with linear time complexity.

---
⭐ Day 6 of my LeetCode 75 Challenge
