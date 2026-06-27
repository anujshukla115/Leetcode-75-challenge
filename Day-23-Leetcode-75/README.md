# 2352. Equal Row and Column Pairs

🔗 **Problem Link:** https://leetcode.com/problems/equal-row-and-column-pairs/

---

## Problem Statement

Given a **0-indexed** `n x n` integer matrix `grid`, return the number of pairs `(Ri, Cj)` such that row `Ri` and column `Cj` are equal.

A row and column pair is considered equal if they contain the same elements in the same order.

---

## Approach (Map + Matrix Traversal)

### Key Idea

* Store every row of the matrix in a map along with its frequency.
* Build each column as a vector.
* Check whether the column exists in the map.
* If it exists, add its frequency to the answer.

This works because multiple identical rows can exist, and each matching row contributes to the final count.

---

## Algorithm

1. Create a map to store each row and its frequency.
2. Traverse all rows and insert them into the map.
3. For each column:

   * Build a vector representing the column.
   * Check if this column vector exists in the map.
   * If yes, add its frequency to the answer.
4. Return the final count.

---

## Dry Run

### Example

```text
grid =
[
 [3,1,2,2],
 [1,4,4,5],
 [2,4,2,2],
 [2,4,2,2]
]
```

### Step 1: Store Rows in Map

```text
[3,1,2,2] -> 1
[1,4,4,5] -> 1
[2,4,2,2] -> 2
```

---

### Step 2: Build Columns

#### Column 0

```text
[3,1,2,2]
```

Found in map.

```text
count += 1
```

---

#### Column 1

```text
[1,4,4,4]
```

Not found.

```text
count += 0
```

---

#### Column 2

```text
[2,4,2,2]
```

Found in map with frequency 2.

```text
count += 2
```

---

#### Column 3

```text
[2,5,2,2]
```

Not found.

Final Answer:

```text
3
```

---

## Code

```cpp
class Solution {
public:
    int equalPairs(vector<vector<int>>& grid) {

        int n = grid.size();
        int count = 0;

        map<vector<int>, int> mp;

        // Store all rows in the map
        for(auto row : grid)
        {
            mp[row]++;
        }

        // Build each column and check in map
        for(int j = 0; j < n; j++)
        {
            vector<int> col;

            for(int i = 0; i < n; i++)
            {
                col.push_back(grid[i][j]);
            }

            if(mp.find(col) != mp.end())
            {
                count += mp[col];
            }
        }

        return count;
    }
};
```

---

## Complexity Analysis

### Time Complexity: **O(n² log n)**

* Storing rows in map: **O(n² log n)**
* Building all columns: **O(n²)**
* Searching columns in map: **O(n² log n)**

Overall:

```text
O(n² log n)
```

---

### Space Complexity: **O(n²)**

* The map stores all rows of the matrix.

Overall:

```text
O(n²)
```

---

## Key Learning

* A complete row can be used as a key in a `map`.
* Frequency maps are useful when duplicate rows exist.
* Matrix problems often become easier by converting rows/columns into vectors.
* Storing precomputed information helps avoid repeated comparisons.

---

**Topic Tags:** `Matrix` `Hash Map` `Map` `Simulation`
