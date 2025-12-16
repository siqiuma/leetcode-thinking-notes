# Best Time to Buy and Sell Stock II (LeetCode 122)

## Problem Summary
You are given an array `prices` where `prices[i]` is the stock price on day `i`.

You may complete as many transactions as you like (buy one and sell one share of the stock multiple times), but you may hold at most one share at a time.

Return the maximum profit.

---

## Pattern
Greedy  
(Sum of all positive price differences)

---

## Key Insight
Since unlimited transactions are allowed, every profitable price increase can be taken.

For any consecutive days `i` and `i + 1`:
- If `prices[i + 1] > prices[i]`, we can profit by buying on day `i` and selling on day `i + 1`.

Summing all such positive differences captures the profit of **every increasing segment**, which is equivalent to any optimal buy-sell strategy.

---

## Algorithm
1. Initialize `maxProfit = 0`
2. Traverse the array:
   - If `prices[i + 1] > prices[i]`, add `prices[i + 1] - prices[i]` to `maxProfit`
3. Return `maxProfit`

---

## Why This Works
Any increasing price sequence can be broken into daily gains without changing the total profit.

Example:
Buy at 1, sell at 5
profit = 5 - 1 = 4

Equivalent to:
(2 - 1) + (3 - 2) + (5 - 3) = 4

Since there is no limit on the number of transactions, taking every upward move is optimal.  
Downward moves are skipped because they would reduce profit.

---

## Complexity
- Time: O(n)
- Space: O(1)

---

## Common Mistakes
- Treating this problem as “only one transaction” (Stock I)
- Trying to find global min/max unnecessarily
- Overcomplicating with DP when greedy is sufficient

---

## Code (Java)
```java
class Solution {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        for (int i = 0; i < prices.length - 1; i++) {
            if (prices[i] < prices[i + 1]) {
                maxProfit += prices[i + 1] - prices[i];
            }
        }
        return maxProfit;
    }
}
