# 1456. Maximum Number of Vowels in a Substring of Given Length K

## Problem Link

https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length-k/

---

## Problem Statement

Given a string `s` and an integer `k`, return the maximum number of vowel letters in any substring of `s` with length `k`.

Vowels are:

* a
* e
* i
* o
* u

---

## Approach

This problem can be solved using the **Fixed Size Sliding Window** technique.

### Idea

* Count vowels in the first window of size `k`.
* Store this count as the current maximum.
* Slide the window one character at a time.
* Remove the contribution of the outgoing character.
* Add the contribution of the incoming character.
* Update the maximum vowel count.

This avoids recalculating vowels for every substring.

---

## Dry Run

Input:

s = "abciiidef"
k = 3

First window:

abc → vowels = 1

maxVowel = 1

Slide window:

bci → vowels = 1

cii → vowels = 2

maxVowel = 2

iii → vowels = 3

maxVowel = 3

iid → vowels = 2

ide → vowels = 2

def → vowels = 1

Answer = 3

---

## Code

```cpp
class Solution {
public:
    int maxVowels(string s, int k) {

        unordered_set<char> vowels={'a','e','i','o','u'};

        int n = s.size();
        int currentVowelCount = 0;

        for(int i=0; i<k; i++)
        {
            if(vowels.count(s[i]))
            {
                currentVowelCount++;
            }
        }

        int maxvowel = currentVowelCount;

        for(int i = k; i < n; i++)
        {
            if(vowels.count(s[i-k]))
            {
                currentVowelCount--;
            }

            if(vowels.count(s[i]))
            {
                currentVowelCount++;
            }

            maxvowel=max(maxvowel,currentVowelCount);
        }

        return maxvowel;
    }
};
```

---

## Time Complexity

O(n)

* First window: O(k)
* Sliding window traversal: O(n-k)

Overall:

O(n)

---

## Space Complexity

O(1)

The vowel set contains only 5 fixed characters, so extra space remains constant.

---

## Key Learning

* Fixed Size Sliding Window
* Efficient window updates
* Avoiding repeated calculations
* Character frequency tracking
