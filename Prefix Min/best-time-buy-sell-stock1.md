# Best Time to Buy and Sell Stock (LeetCode 121)

## Problem Summary
Given an array `prices` where `prices[i]` is the stock price on day `i`, choose **one day to buy** and a **later day to sell** to maximize profit.  
Return the maximum profit; if no profit is possible, return `0`.

## Pattern
Greedy / One-pass  
Running Minimum (Prefix Min)

## Key Insight
If we sell on day `i`, the best buy day must be the day with the **minimum price in days [0..i]**.  
So the best profit for day `i` is:
`profit(i) = prices[i] - minPriceSoFar`  
Answer is the maximum of `profit(i)` over all days.

## Algorithm
1. Initialize `minPrice = +∞`, `maxProfit = 0`
2. Traverse `prices`:
   - Update `minPrice = min(minPrice, prices[i])`
   - Update `maxProfit = max(maxProfit, prices[i] - minPrice)`
3. Return `maxProfit`

## Why This Works (Invariant)
After processing day `i`:
- `minPrice` is the minimum price in `prices[0..i]`
- `prices[i] - minPrice` is the maximum profit for transactions that **sell on day i**
Taking the max over all `i` gives the optimal single-transaction profit.

## Complexity
- Time: `O(n)`
- Space: `O(1)`

## Common Mistakes
- Trying to sell before buying (not enforcing "buy before sell")
- Returning a negative profit instead of `0`
- Using nested loops (`O(n^2)`) and timing out

## Code (Java)
```java
class Solution {
    public int maxProfit(int[] prices) {
        int minPrice = Integer.MAX_VALUE;
        int maxProfit = 0;

        for (int price : prices) {
            minPrice = Math.min(minPrice, price);
            maxProfit = Math.max(maxProfit, price - minPrice);
        }
        return maxProfit;
    }
}
