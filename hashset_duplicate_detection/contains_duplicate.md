# Contains Duplicate (LeetCode 217)

## Problem Summary
Given an integer array `nums`, return `true` if any value appears at least twice in the array, and return `false` if every element is distinct.

---

## Pattern
Hash Set / Duplicate Detection

---

## Key Insight
While traversing the array, if a value has appeared before, then a duplicate exists.

A hash set allows constant-time checks for whether an element has already been seen.

---

## Algorithm
1. Create a hash set to store elements that have already appeared
2. Traverse the array from left to right:
   - If the current element exists in the set, return `true`
   - Otherwise, add the element to the set
3. If traversal completes without finding duplicates, return `false`

---

## Why This Works
At index `i`, the hash set contains all elements from indices `[0 .. i - 1]`.

If `nums[i]` is already in the set:
- A duplicate has been found
- Early return avoids unnecessary work

Every element is checked once, and no nested loops are needed.

---

## Complexity
- Time: `O(n)`
- Space: `O(n)`

---

## Common Mistakes
- Using nested loops and getting `O(n²)` time complexity
- Forgetting to return early after finding a duplicate
- Sorting the array and unintentionally modifying the input

---

## Code (Java)
```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> set = new HashSet<>();

        for (int num : nums) {
            if (set.contains(num)) {
                return true;
            }
            set.add(num);
        }
        return false;
    }
}
