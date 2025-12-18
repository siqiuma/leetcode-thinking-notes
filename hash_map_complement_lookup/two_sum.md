# Two Sum (LeetCode 1)

## Problem Summary
Given an integer array `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`.

You may assume that each input has exactly one solution, and you may not use the same element twice.

---

## Pattern
Hash Map / Complement Lookup

---

## Key Insight
For each element `nums[i]`, if there exists a previous element equal to  
`target - nums[i]`, then the pair forms a valid solution.

A hash map allows us to check the existence of this complement in O(1) time while traversing the array only once.

---

## Algorithm
1. Create a hash map to store `<value, index>` for elements already seen
2. Traverse the array from left to right:
   - If `target - nums[i]` exists in the map, return the stored index and `i`
   - Otherwise, store `nums[i]` with its index in the map
3. Since exactly one solution exists, the answer will be found during traversal

---

## Why This Works
At index `i`, the hash map contains all elements from indices `[0 .. i-1]`.

If `target - nums[i]` is found in the map:
- It guarantees we are using two different elements
- Every possible pair is considered exactly once
- No nested loops are required

---

## Complexity
- Time: O(n)
- Space: O(n)

---

## Common Mistakes
- Returning values instead of indices
- Using the same element twice
- Using nested loops (O(n²)) instead of hashing

---

## Code (Java)
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[]{map.get(complement), i};
            }
            map.put(nums[i], i);
        }

        return new int[0];
    }
}
