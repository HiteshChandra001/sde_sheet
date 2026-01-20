# 3Sum – Java Solution

## Problem Statement

Given an integer array `nums`, return **all unique triplets** `[nums[a], nums[b], nums[c]]` such that:

* `a != b`, `b != c`, and `a != c`
* `nums[a] + nums[b] + nums[c] == 0`

The solution must not contain duplicate triplets.

---

## Approach

This solution uses the **two-pointer technique** combined with **sorting**.

### Key Steps

1. **Sort the array**

   * Sorting helps efficiently apply the two-pointer strategy and makes it easier to avoid duplicates.

2. **Fix the first element**

   * Iterate through the array and treat `nums[a]` as the first number of the triplet.

3. **Use two pointers**

   * Initialize two pointers:

     * `b = a + 1` (left pointer)
     * `c = n - 1` (right pointer)
   * Move pointers based on the sum:

     * If the sum is `0`, store the triplet.
     * If the sum is less than `0`, move the left pointer (`b++`).
     * If the sum is greater than `0`, move the right pointer (`c--`).

4. **Avoid duplicates**

   * A `HashSet<List<Integer>>` is used to ensure only unique triplets are stored.

---

## Code Explanation

```java
Arrays.sort(nums);
```

Sorts the array to enable two-pointer traversal.

```java
Set<List<Integer>> res = new HashSet<>();
```

Ensures duplicate triplets are not added.

```java
while (b < c) {
    int sum = nums[a] + nums[b] + nums[c];
```

Evaluates the sum of the current triplet and adjusts pointers accordingly.

---

## Time and Space Complexity

* **Time Complexity:** `O(n²)`

  * Sorting takes `O(n log n)`
  * Two-pointer traversal for each element takes `O(n)`

* **Space Complexity:** `O(k)`

  * Where `k` is the number of unique triplets stored in the result set

---

## Example

**Input**

```
nums = [-1, 0, 1, 2, -1, -4]
```

**Output**

```
[[-1, -1, 2], [-1, 0, 1]]
```

---
