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





# Four Sum (4Sum) Problem

This repository contains a Java implementation of the **4Sum** problem, a classic array + two-pointer problem commonly asked in coding interviews and featured on platforms like LeetCode.

---

## 🧩 Problem Statement

Given an integer array `nums` and an integer `target`, return **all unique quadruplets** `[nums[a], nums[b], nums[c], nums[d]]` such that:

* `a`, `b`, `c`, and `d` are **distinct indices**
* `nums[a] + nums[b] + nums[c] + nums[d] == target`
* The solution set must **not contain duplicate quadruplets**

---

## 💡 Approach

This solution uses a **sorting + two pointers** strategy:

1. **Sort the array** to make duplicate handling and pointer movement easier.
2. Fix the **first two numbers** using two nested loops (`i` and `j`).
3. Use **two pointers** (`l` and `r`) to find the remaining two numbers.
4. Skip duplicate values at every step to ensure uniqueness.
5. Use `long` for sum calculation to avoid integer overflow.

---

## ✅ Key Features

* Handles duplicate values correctly
* Prevents integer overflow
* Efficient compared to brute force

---

## 🧠 Algorithm Steps

1. Sort the input array
2. Loop `i` from `0` to `n-1`

   * Skip duplicates for `i`
3. Loop `j` from `i+1` to `n-1`

   * Skip duplicates for `j`
4. Initialize two pointers:

   * `l = j + 1`
   * `r = n - 1`
5. While `l < r`:

   * Compute the sum of four elements
   * If sum equals target → store result and move both pointers
   * If sum < target → move `l` forward
   * If sum > target → move `r` backward

---

## ⏱️ Time & Space Complexity

* **Time Complexity:** `O(n^3)`
* **Space Complexity:** `O(1)` (excluding output list)

---

## 🧪 Example

```text
Input:
nums = [1, 0, -1, 0, -2, 2]
target = 0

Output:
[
  [-2, -1, 1, 2],
  [-2, 0, 0, 2],
  [-1, 0, 0, 1]
]
```

---

## 🧑‍💻 Java Implementation

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        if (nums == null || nums.length < 4) return ans;

        Arrays.sort(nums);
        int n = nums.length;

        for (int i = 0; i < n; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            for (int j = i + 1; j < n; j++) {
                if (j > i + 1 && nums[j] == nums[j - 1]) continue;

                int l = j + 1, r = n - 1;
                while (l < r) {
                    long sum = (long) nums[i] + nums[j] + nums[l] + nums[r];

                    if (sum == target) {
                        ans.add(Arrays.asList(nums[i], nums[j], nums[l], nums[r]));
                        l++;
                        r--;
                        while (l < r && nums[l] == nums[l - 1]) l++;
                        while (l < r && nums[r] == nums[r + 1]) r--;
                    } else if (sum < target) {
                        l++;
                    } else {
                        r--;
                    }
                }
            }
        }
        return ans;
    }
}
```



