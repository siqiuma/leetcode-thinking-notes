# Subarray Sum Equals K (LeetCode 560)

## Problem Summary
Given an integer array `nums` and an integer `k`, return the total number of contiguous subarrays whose sum equals `k`.

---

## Pattern
Prefix Sum + Hash Map (frequency counting)

---

## Key Insight
Let `prefixSum[i]` be the sum of `nums[0..i]`.

A subarray `nums[j+1..i]` sums to `k` if:
prefixSum[i] - prefixSum[j] = k
=> prefixSum[j] = prefixSum[i] - k

So at each index `i`, if we have seen `prefixSum[i] - k` before, then all those occurrences represent valid subarrays ending at `i`.

---

## Algorithm
1. Use a hash map `map` storing `<prefixSum, frequency>` for prefix sums seen so far  
   Initialize `map[0] = 1` to count subarrays starting from index 0.
2. Traverse the array:
   - Update running sum: `sum += nums[i]`
   - If `map` contains `sum - k`, add its frequency to `count`
   - Update `map[sum]++`
3. Return `count`

---

## Why This Works
At index `i`, the map contains frequencies of all prefix sums from earlier indices.

If `sum - k` appears `f` times, then there are `f` different starting points that form subarrays ending at `i` with sum `k`.  
This is why we must store **frequency**, not just existence.

---

## Complexity
- Time: `O(n)`
- Space: `O(n)`

---

## Common Mistakes
- Using nested loops (`O(n²)`)
- Forgetting `map[0] = 1` (misses subarrays starting at index 0)
- Storing only existence instead of frequency (under-counts)
- Trying sliding window when negatives exist (does not work)

---

## Code (Java)
```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);

        int sum = 0;
        int count = 0;

        for (int num : nums) {
            sum += num;
            count += map.getOrDefault(sum - k, 0);
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }

        return count;
    }
}
