# Day 12 - LeetCode 11: Container With Most Water

## Problem Link

https://leetcode.com/problems/container-with-most-water/

---

## Problem Statement

You are given an integer array `height` of length `n`.

There are `n` vertical lines drawn such that the two endpoints of the `i-th` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container that holds the maximum amount of water.

Return the maximum amount of water a container can store.

---

## Approach

### Brute Force

Try every possible pair of lines.

For every pair:

```cpp
area = min(height[i], height[j]) * (j - i)
```

Store the maximum area.

Time Complexity:

```text
O(n²)
```

---

### Optimal Approach (Two Pointers)

Start with:

```cpp
left = 0
right = n - 1
```

This gives the maximum possible width.

For every iteration:

```cpp
width = right - left
height = min(height[left], height[right])
area = width * height
```

Update the maximum area.

Move the pointer pointing to the shorter line because the shorter line limits the water level.

---

## Dry Run

### Input

```cpp
height = [1,8,6,2,5,4,8,3,7]
```

Initial:

```cpp
left = 0
right = 8
```

Area:

```cpp
width = 8
height = min(1,7) = 1

area = 8
```

Move:

```cpp
left++
```

Now:

```cpp
left = 1
right = 8
```

Area:

```cpp
width = 7
height = min(8,7) = 7

area = 49
```

Maximum area becomes:

```cpp
49
```

---

## Code

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {

        int left = 0;
        int right = height.size() - 1;
        int maxi = 0;

        while(left < right)
        {
            int width = right - left;
            int h = min(height[left], height[right]);
            int area = h * width;

            maxi = max(maxi, area);

            if(height[left] < height[right])
            {
                left++;
            }
            else
            {
                right--;
            }
        }

        return maxi;
    }
};
```

---

## Complexity Analysis

### Time Complexity

```text
O(n)
```

Each pointer moves at most once across the array.

### Space Complexity

```text
O(1)
```

---

## Key Learning

* Choosing the two tallest lines does not always give the maximum area.
* Area depends on both height and width.
* Start with maximum width and gradually improve the limiting height.
* The shorter wall determines the amount of water the container can hold.
