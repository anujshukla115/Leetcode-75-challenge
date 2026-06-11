# 📌 Product of Array Except Self

🔗 **Problem Link:** https://leetcode.com/problems/product-of-array-except-self/

## 📝 Problem Statement

Given an integer array `nums`, return an array `answer` such that:

```text
answer[i] is equal to the product of all the elements of nums except nums[i].
```

### Example

```cpp
Input: nums = [1,2,3,4]

Output: [24,12,8,6]
```

---

## 💡 Approach (Division with Zero Handling)

The idea is to first calculate the product of all non-zero elements and count how many zeros are present in the array.

### Case 1: No Zero Present

If there are no zeros in the array:

```text
answer[i] = totalProduct / nums[i]
```

Example:

```cpp
nums = [1,2,3,4]

totalProduct = 24

answer = [24,12,8,6]
```

---

### Case 2: Exactly One Zero

Example:

```cpp
nums = [1,2,0,4]
```

Product of non-zero elements:

```cpp
1 × 2 × 4 = 8
```

Output:

```cpp
[0,0,8,0]
```

Only the position containing zero gets the product of all non-zero elements.

---

### Case 3: More Than One Zero

Example:

```cpp
nums = [1,0,2,0,4]
```

Output:

```cpp
[0,0,0,0,0]
```

Since every product will contain at least one zero.

---

## 🔍 Algorithm

1. Count the number of zeros in the array.
2. Calculate the product of all non-zero elements.
3. Traverse the array again:
   - If `zero == 0`, use division.
   - If `zero == 1`, place the product only at the zero index.
   - If `zero > 1`, all answers remain zero.

---

## ✅ C++ Solution

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {

        int n = nums.size();
        int zero = 0;
        int prod = 1;

        vector<int> ans(n,0);

        for(int i=0;i<n;i++)
        {
            if(nums[i] == 0)
                zero++;
            else
                prod *= nums[i];
        }

        for(int i=0;i<n;i++)
        {
            if(zero == 0)
            {
                ans[i] = prod / nums[i];
            }
            else if(zero == 1)
            {
                if(nums[i] == 0)
                    ans[i] = prod;
            }
        }

        return ans;
    }
};
```

---

## ⏱️ Time Complexity

- First traversal to count zeros and calculate product → **O(n)**
- Second traversal to build answer array → **O(n)**

```text
Time Complexity = O(n)
```

---

## 📦 Space Complexity

Only a few extra variables are used:

```text
zero
prod
```

Therefore:

```text
Space Complexity = O(1)
```

*(Output array is not counted as extra space.)*

---

## 🚀 Key Learnings

- Handling edge cases involving zeros
- Product calculation without nested loops
- Optimizing from O(n²) to O(n)
- Array traversal techniques

---

### 🌟 LeetCode 75 Challenge - Day 7
Problem #238 - Product of Array Except Self
