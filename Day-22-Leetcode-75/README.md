# 1657. Determine if Two Strings Are Close

🔗 **Problem Link:** https://leetcode.com/problems/determine-if-two-strings-are-close/

---

## Problem Statement

Two strings are considered **close** if you can attain one string from the other using the following operations any number of times:

1. Swap any two existing characters.
2. Transform every occurrence of one existing character into another existing character, and do the same with the other character.

Return `true` if `word1` and `word2` are close, otherwise return `false`.

---

## Approach (Hash Map + Sorting)

### Key Observations

To make two strings close:

1. Both strings must contain the **same set of unique characters** because we cannot create new characters.
2. The **frequency distribution** of characters must be the same because frequencies can be swapped among existing characters.

### Steps

1. If the lengths of both strings are different, return `false`.
2. Store character frequencies of both strings using two hash maps.
3. Check whether both strings contain the same unique characters.
4. Store all frequencies from both maps into two vectors.
5. Sort both vectors.
6. If the sorted frequency vectors are equal, return `true`; otherwise, return `false`.

---

## Dry Run

### Example

```text
word1 = "cabbba"
word2 = "abbccc"
```

### Frequency Maps

```text
word1:
a → 1
b → 3
c → 2

word2:
a → 1
b → 2
c → 3
```

### Unique Characters

```text
word1 = {a, b, c}
word2 = {a, b, c}
```

Both contain the same characters ✅

### Frequency Vectors

```text
freq1 = {1, 3, 2}
freq2 = {1, 2, 3}
```

After sorting:

```text
freq1 = {1, 2, 3}
freq2 = {1, 2, 3}
```

Vectors are equal, so return:

```text
true
```

---

## Code

```cpp
class Solution {
public:
    bool closeStrings(string word1, string word2) {

        if(word1.size() != word2.size())
        {
            return false;
        }

        unordered_map<char, int> mp1;
        unordered_map<char, int> mp2;

        for(auto ch : word1)
        {
            mp1[ch]++;
        }

        for(auto ch : word2)
        {
            mp2[ch]++;
        }

        for(auto x : mp1)
        {
            if(mp2.find(x.first) == mp2.end())
            {
                return false;
            }
        }

        vector<int> freq1;
        vector<int> freq2;

        for(auto x : mp1)
        {
            freq1.push_back(x.second);
        }

        for(auto x : mp2)
        {
            freq2.push_back(x.second);
        }

        sort(freq1.begin(), freq1.end());
        sort(freq2.begin(), freq2.end());

        return freq1 == freq2;
    }
};
```

---

## Complexity Analysis

### Time Complexity: **O(n)**

* Building frequency maps: **O(n)**
* Checking character existence: **O(26)**
* Storing frequencies: **O(26)**
* Sorting frequency vectors: **O(26 log 26)**

Overall:

```text
O(n)
```

---

### Space Complexity: **O(1)**

* Two hash maps and two vectors store at most 26 lowercase English characters.

Overall:

```text
O(1)
```

---

## Key Learning

* Hash maps are useful for frequency counting.
* Two strings can be transformed only if they contain the same unique characters.
* Frequency distributions can be compared efficiently by sorting frequency values.
