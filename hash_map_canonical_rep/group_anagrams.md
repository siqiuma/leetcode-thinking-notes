# Group Anagrams (LeetCode 49)

## Problem Summary
Given an array of strings `strs`, group the anagrams together.  
You may return the answer in any order.

---

## Pattern
Hash Map + Canonical Representation  
(Frequency Encoding)

---

## Key Insight
All anagrams share the same **canonical representation**.

Two strings are anagrams if and only if they have the same frequency count for each character.  
By encoding character frequencies into a unique string key, we can group all anagrams using a hash map.

---

## Algorithm
1. Create a hash map where:
   - key = canonical representation of a string
   - value = list of strings belonging to that representation
2. For each string:
   - Count the frequency of each character (26 letters)
   - Convert the frequency array into a string key (with separators)
   - Add the string to the corresponding list in the map
3. Return all values of the map as the result

---

## Why This Works
Anagrams form an **equivalence class** where all strings share the same character frequency distribution.

The frequency encoding acts as a unique and collision-free identifier for each anagram group.  
Using a hash map ensures that all strings with the same representation are grouped together.

---

## Complexity
Let:
- `n` = number of strings
- `k` = maximum length of a string

- Time: `O(n * k)`
- Space: `O(n * k)`

---

## Common Mistakes
- Using character counts without separators (e.g., `11` vs `1#1`)
- Using nested loops and comparing strings pairwise (`O(n² * k)`)
- Forgetting that input strings may be empty

---

## Code (Java)
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap<>();

        for (String str : strs) {
            int[] count = new int[26];
            for (char c : str.toCharArray()) {
                count[c - 'a']++;
            }

            StringBuilder sb = new StringBuilder();
            for (int num : count) {
                sb.append(num).append('#');
            }
            String key = sb.toString();

            map.computeIfAbsent(key, k -> new ArrayList<>()).add(str);
        }

        return new ArrayList<>(map.values());
    }
}
