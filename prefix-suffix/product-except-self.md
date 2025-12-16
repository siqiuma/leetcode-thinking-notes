# Product of Array Except Self

## Problem Summary
Given an array, return an array where each element is the product of all other elements.
Constraints:
- O(n) time
- No division

---

## Pattern
Prefix / Suffix Product

---

## Key Insight
For each index i:
result[i] = product of elements on the left of i × product of elements on the right of i

---

## Algorithm
1. First pass: store left products in result[]
2. Second pass: multiply right products into result[]
3. Use two variables (left, right) to achieve O(1) extra space

---

## Why This Works
- Avoids division
- Naturally handles zero
- Each element contributes exactly once to left or right

---

## Complexity
- Time: O(n)
- Space: O(1) (excluding output)

---

## Common Mistakes
- Using division
- Using extra arrays unnecessarily

---

## Code
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        
        // result[i] will store the product of all elements except nums[i]
        int[] result = new int[n];
        
        // left represents the product of all elements to the left of i
        int left = 1;
        for (int i = 0; i < n; i++) {
            // at index i, left is the product of nums[0..i-1]
            result[i] = left;
            left *= nums[i];
        }
        
        // right represents the product of all elements to the right of i
        int right = 1;
        for (int i = n - 1; i >= 0; i--) {
            // multiply left product with right product
            result[i] *= right;
            right *= nums[i];
        }
        
        return result;
    }
}

