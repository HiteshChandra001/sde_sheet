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

# Remove Duplicates from Sorted Array

## 📌 Problem Statement

Given a **sorted integer array `nums`**, remove the duplicates **in-place** such that each unique element appears only once.
The relative order of the elements should be kept the same.

Return the number of unique elements (`k`).
The first `k` elements of `nums` should contain the final result.

> Extra space is not allowed (O(1) space).

---

## 💡 Approach

Since the array is already **sorted**, all duplicate elements are adjacent.

We use:

* A **pointer `i`** to iterate through the array
* A **counter `c`** to track the position where the next unique element should be placed

Whenever two adjacent elements are different, we store the current element at index `c` and increment `c`.

At the end, we add the last element and return `c + 1` as the count of unique elements.

---

## 🧠 Algorithm

1. Initialize:

   * `c = 0` (index for unique elements)
   * `i = 0` (iterator)
2. Traverse the array while `i < n - 1`
3. If `nums[i] != nums[i + 1]`:

   * Assign `nums[c] = nums[i]`
   * Increment `c`
4. After the loop, store the last element
5. Return `c + 1`

---

## ✅ Java Implementation

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int n = nums.length;
        int c = 0;
        int i = 0;

        while (i < n - 1) {
            if (nums[i] != nums[i + 1]) {
                nums[c] = nums[i];
                c++;
            }
            i++;
        }
        nums[c] = nums[i];
        return c + 1;
    }
}
```

---

## 📊 Example

**Input**

```
nums = [1,1,2,2,3]
```

**Output**

```
k = 3
nums = [1,2,3,_ ,_]
```

---

## ⏱️ Complexity Analysis

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)` (in-place modification)

---

# Find Max Consecutive Ones

## 📌 Problem Description

Given a binary array `nums`, return the **maximum number of consecutive 1s** in the array.

### Example

```
Input:  [1,1,0,1,1,1]
Output: 3
Explanation: The longest run of consecutive 1s is [1,1,1].
```

---

## 🧠 Approach

The solution uses a **single pass** through the array while keeping track of:

* `c` → current count of consecutive `1`s
* `max` → maximum count found so far

### Logic

* If the current element is `1`, increment the counter.
* Update the maximum value whenever the counter increases.
* If the element is `0`, reset the counter to `0`.

This ensures optimal performance with minimal space usage.

---

## 💻 Code Implementation (Java)

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int c = 0;
        int max = 0;
        for (int i : nums) {
            if (i == 1) {
                c++;
                max = Math.max(max, c);
            } else {
                c = 0;
            }
        }
        return max;
    }
}
```

---

## ⏱️ Time & Space Complexity

* **Time Complexity:** `O(n)` — traverses the array once
* **Space Complexity:** `O(1)` — uses constant extra space

---
