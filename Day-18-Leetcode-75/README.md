# 1732. Find the Highest Altitude

## Problem Link

https://leetcode.com/problems/find-the-highest-altitude/

---

## Problem Statement

There is a biker going on a road trip. The trip consists of `n + 1` points at different altitudes.

You are given an integer array `gain` of length `n` where:

* `gain[i]` is the net gain in altitude between points `i` and `i + 1`.

The biker starts the trip at altitude `0`.

Return the **highest altitude** of a point reached during the trip.

---

## Approach (Optimal - Running Sum)

### Intuition

The biker starts at altitude `0`.

As we traverse the `gain` array:

* Maintain a variable `currAlt` to store the current altitude.
* Update the altitude after every gain/loss.
* Maintain another variable `maxAlt` to keep track of the highest altitude reached so far.

At every step:

```cpp
currAlt += gain[i];
maxAlt = max(maxAlt, currAlt);
```

The final value of `maxAlt` will be the answer.

---

## Dry Run

### Input

```cpp
gain = [-5,1,5,0,-7]
```

| Step  | Gain | Current Altitude | Maximum Altitude |
| ----- | ---- | ---------------- | ---------------- |
| Start | -    | 0                | 0                |
| 1     | -5   | -5               | 0                |
| 2     | 1    | -4               | 0                |
| 3     | 5    | 1                | 1                |
| 4     | 0    | 1                | 1                |
| 5     | -7   | -6               | 1                |

Therefore:

```cpp
Answer = 1
```

---

## Code

```cpp
class Solution {
public:
    int largestAltitude(vector<int>& gain) {

        int currAlt = 0;
        int maxAlt = 0;

        for(int i = 0; i < gain.size(); i++)
        {
            currAlt += gain[i];
            maxAlt = max(maxAlt, currAlt);
        }

        return maxAlt;
    }
};
```

### Alternative (Range-Based Loop)

```cpp
class Solution {
public:
    int largestAltitude(vector<int>& gain) {
        int altitude = 0, maxAlt = 0;

        for (int g : gain) {
            altitude += g;
            maxAlt = max(maxAlt, altitude);
        }

        return maxAlt;
    }
};
```

---

## Complexity Analysis

### Time Complexity

```cpp
O(n)
```

* We traverse the `gain` array only once.
* Each element is processed exactly one time.

Overall:

```cpp
O(n)
```

### Space Complexity

```cpp
O(1)
```

Only two extra variables (`currAlt` and `maxAlt`) are used.

---

## Key Learning

* Running Sum is a powerful technique for tracking cumulative values efficiently.
* Maintaining only the necessary state can eliminate the need for extra space.
* Always consider whether intermediate values need to be stored or can be computed on the fly.
