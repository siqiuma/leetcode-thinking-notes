# Maximum Subarray (LeetCode 53)

## Problem Summary
Given an integer array `nums`, find the contiguous subarray with the largest sum and return that sum.

A subarray must be contiguous and contain at least one element.

---

## Pattern
Dynamic Programming (Kadane’s Algorithm)  
Can also be viewed as Greedy with a running prefix sum.

---

## Key Insight
Define `dp[i]` as the maximum subarray sum **ending at index i**.

At each position, we have two choices:
- Extend the previous subarray if it has positive contribution
- Start a new subarray at the current index

So the recurrence is:
dp[i] = max(nums[i], dp[i - 1] + nums[i])


The answer is the maximum value among all `dp[i]`.

---

## Algorithm
1. Initialize `currentSum = nums[0]` and `maxSum = nums[0]`
2. Traverse the array from index 1:
   - Update `currentSum = max(nums[i], currentSum + nums[i])`
   - Update `maxSum = max(maxSum, currentSum)`
3. Return `maxSum`

---

## Why This Works
At each index `i`, `currentSum` always represents the **maximum subarray sum ending at `i`**.

If the previous subarray sum is negative, extending it would only reduce the current sum, so it is optimal to discard it and start a new subarray at `i`.

By evaluating every possible subarray that ends at each index and keeping track of the maximum, we guarantee the optimal solution.

---

## Complexity
- Time: `O(n)`
- Space: `O(1)`

---

## Common Mistakes
- Treating the problem as sliding window (window size is not fixed or constrained)
- Returning 0 when all elements are negative
- Forgetting that the subarray must be contiguous

---

## Code (Java)
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int currentSum = nums[0];
        int maxSum = nums[0];

        for (int i = 1; i < nums.length; i++) {
            currentSum = Math.max(nums[i], currentSum + nums[i]);
            maxSum = Math.max(maxSum, currentSum);
        }

        return maxSum;
    }
}
