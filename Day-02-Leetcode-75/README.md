# 1071. Greatest Common Divisor of Strings

🔗 **Problem Link:** https://leetcode.com/problems/greatest-common-divisor-of-strings/

## Problem Statement

For two strings `str1` and `str2`, we say that a string `x` divides a string `s` if `s` can be formed by concatenating `x` with itself one or more times.

Given two strings `str1` and `str2`, return the largest string `x` such that `x` divides both `str1` and `str2`.

---

## Approach (Optimal)

### Key Observation

If two strings are formed by repeating the same base pattern, then:

```text
str1 + str2 == str2 + str1
```

If this condition is false, then no common divisor string exists.

If it is true, then the length of the largest common divisor string will be:

```text
gcd(str1.length(), str2.length())
```

We can simply return the prefix of `str1` having this GCD length.

### Example

```text
str1 = "ABCABC"
str2 = "ABC"
```

Check:

```text
str1 + str2 = "ABCABCABC"
str2 + str1 = "ABCABCABC"
```

Both are equal ✅

Lengths:

```text
6 and 3
```

GCD:

```text
gcd(6, 3) = 3
```

Take first 3 characters of `str1`:

```text
"ABC"
```

Answer = `"ABC"`

---

## C++ Solution

```cpp
class Solution {
public:
    string gcdOfStrings(string str1, string str2) {
        if(str1+str2==str2+str1)
        {
            return str1.substr(0,gcd(str1.size(),str2.size()));
        }

        return "";
        
    }
};
```

---

## Time Complexity

| Operation | Complexity |
|------------|------------|
| String Concatenation & Comparison | O(n + m) |
| GCD Calculation | O(log(min(n, m))) |
| Substring Extraction | O(gcdLength) |

### Overall Time Complexity

```text
O(n + m)
```

where:

- n = str1.length()
- m = str2.length()

---

## Space Complexity

```text
O(n + m)
```

Extra space is used while creating the concatenated strings:

```cpp
str1 + str2
str2 + str1
```

---

## Tags

- String
- Math
- Greatest Common Divisor (GCD)
- LeetCode 75
