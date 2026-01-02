# sde_sheet
Striver SDE DSA Sheet

# Longest Consecutive Sequence

## Problem Statement

Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

The algorithm must run in **O(n)** time.

---

## Approach

* Store all elements in a `HashSet` for **constant time lookup**
* Iterate through the set and start counting **only if the current number has no predecessor**
* Expand the sequence by checking consecutive numbers
* Each number is processed **at most once**

This avoids sorting and ensures linear time complexity.

---

## Java Implementation

```java
import java.util.HashSet;
import java.util.Set;

class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for (int num : nums) {
            set.add(num);
        }

        int res = 0;

        for (Integer num : set) {
            int count = 1;

            // Check if it's the start of a sequence
            if (!set.contains(num - 1)) {
                while (set.contains(num + 1)) {
                    num++;
                    count++;
                }
                res = Math.max(res, count);
            }
        }

        return res;
    }
}
```

---

## Example

**Input:**

```
nums = [100, 4, 200, 1, 3, 2]
```

**Output:**

```
4
```

**Explanation:**
The longest consecutive sequence is `[1, 2, 3, 4]`.

---

## Complexity Analysis

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(n)`

---

## Key Insight

Only numbers that start a sequence (`num - 1` not present) are expanded, ensuring each element is visited once.


