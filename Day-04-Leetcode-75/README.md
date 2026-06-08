# 🌱 LeetCode 75 - Day 4

## 📌 Problem: 605. Can Place Flowers

🔗 Problem Link: https://leetcode.com/problems/can-place-flowers/

---

## 📝 Problem Statement

You have a long flowerbed in which some plots are planted and some are not. However, flowers cannot be planted in adjacent plots.

Given an integer array `flowerbed` containing `0`s and `1`s, where:

- `0` means the plot is empty.
- `1` means a flower is already planted.

And an integer `n`, return `true` if `n` new flowers can be planted in the flowerbed without violating the no-adjacent-flowers rule; otherwise, return `false`.

### Example 1

```text
Input: flowerbed = [1,0,0,0,1], n = 1
Output: true
```

### Example 2

```text
Input: flowerbed = [1,0,0,0,1], n = 2
Output: false
```

---

## 💡 Approach (Greedy)

We traverse the flowerbed array and check each plot.

A flower can be planted at the current position if:

1. The current plot is empty (`flowerbed[i] == 0`)
2. The left plot is empty or doesn't exist.
3. The right plot is empty or doesn't exist.

Whenever a valid position is found:

- Plant a flower by setting `flowerbed[i] = 1`
- Decrease `n` by 1
- If `n` becomes `0`, return `true` immediately.

If we finish traversing the array and still need more flowers, return `false`.

### Why Greedy?

Whenever a position is valid for planting, planting a flower immediately is always the best choice because it does not reduce the possibility of planting the maximum number of flowers later.

---

## 💻 Code (C++)

```cpp
class Solution {
public:
    bool canPlaceFlowers(vector<int>& flowerbed, int n) {

        if(n == 0) return true;

        for(int i = 0; i < flowerbed.size(); i++) {

            if(flowerbed[i] == 0) {

                if((i == 0 || flowerbed[i - 1] == 0) &&
                   (i == flowerbed.size() - 1 || flowerbed[i + 1] == 0)) {

                    flowerbed[i] = 1;
                    n--;

                    if(n == 0)
                        return true;
                }
            }
        }

        return false;
    }
};
```

---

## ⏱️ Time Complexity

- We traverse the flowerbed array only once.

**Time Complexity:** `O(n)`

where `n` is the size of the flowerbed array.

---

## 💾 Space Complexity

- No extra data structure is used.
- Only constant extra variables are required.

**Space Complexity:** `O(1)`

---

## 🚀 LeetCode 75 Progress

✅ Day 1: Merge Strings Alternately  
✅ Day 2: Greatest Common Divisor of Strings  
✅ Day 3: Kids With the Greatest Number of Candies  
✅ Day 4: Can Place Flowers
