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

---

# Trapping Rain Water – Two Pointer Solution

## Problem

Given an array `height` where each element represents the height of a bar, compute how much water can be trapped after raining.

This is the classic **Trapping Rain Water** problem (LeetCode #42).

---

## Approach

This solution uses a **two-pointer technique** to achieve optimal performance.

### Key Idea

* Use two pointers: `l` (left) and `r` (right).
* Track the maximum height seen so far from both sides:

  * `leftMax`
  * `rightMax`
* Water trapped at any index depends on the **minimum** of the maximum heights to its left and right.

### Algorithm

1. Initialize two pointers at both ends of the array.
2. Move the pointer with the smaller maximum height inward.
3. Accumulate trapped water as:

   ```
   trapped water = currentMax - currentHeight
   ```
4. Continue until both pointers meet.

---

## Code

```java
class Solution {
    public int trap(int[] height) {
        int l = 0, r = height.length - 1;
        int res = 0;
        int leftMax = 0, rightMax = 0;

        while (l < r) {
            leftMax = Math.max(leftMax, height[l]);
            rightMax = Math.max(rightMax, height[r]);

            if (leftMax < rightMax) {
                res += leftMax - height[l++];
            } else {
                res += rightMax - height[r--];
            }
        }
        return res;
    }
}
```

---

## Example

**Input**

```
height = [0,1,0,2,1,0,1,3,2,1,2,1]
```

**Output**

```
6
```

---

## Complexity Analysis

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)` (constant extra space)

---
