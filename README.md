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

# Longest Substring Without Repeating Characters

This repository contains a Java solution for the **Longest Substring Without Repeating Characters** problem, a classic **sliding window** problem frequently asked in coding interviews and competitive programming platforms like LeetCode.

---

## 🧩 Problem Statement

Given a string `s`, find the length of the **longest substring** without repeating characters.

---

## 💡 Approach (Sliding Window + HashMap)

The solution uses the **sliding window technique** combined with a `HashMap` to efficiently track characters and their most recent positions.

### Key Ideas:

* Maintain a window `[st, i]` that always contains unique characters
* Use a `HashMap<Character, Integer>` to store the **last seen index + 1** of each character
* When a duplicate character is found, move the start of the window (`st`) forward
* Keep updating the maximum window length

This approach avoids unnecessary re-checking and runs in linear time.

---

## 🧠 Algorithm Steps

1. Initialize:

   * `st` → start index of the sliding window
   * `res` → maximum length found so far
   * `map` → stores last seen position of characters

2. Iterate through the string using index `i`:

   * If the current character already exists in the map:

     * Update `st` to `max(st, map.get(character))`
   * Calculate the current window length: `i - st + 1`
   * Update `res`
   * Store the character with value `i + 1` in the map

3. Return `res`

---

## ⏱️ Time & Space Complexity

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(min(n, charset))`

Where `n` is the length of the string.

---

## 🧪 Example

```text
Input:
"abcabcbb"

Output:
3

Explanation:
The answer is "abc", with the length of 3.
```

---

## 🧑‍💻 Java Implementation

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int st = 0;
        int res = 0;

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);

            if (map.containsKey(c)) {
                st = Math.max(st, map.get(c));
            }

            res = Math.max(res, i - st + 1);
            map.put(c, i + 1);
        }

        return res;
    }
}
```



# Subarray Sum Equals K

## 📌 Problem Statement

Given an integer array `nums` and an integer `k`, return the **total number of continuous subarrays whose sum equals `k`**.

A subarray is a contiguous part of the array.

---

## 💡 Approach (Prefix Sum + HashMap)

This solution uses the **prefix sum** technique combined with a **hash map** to efficiently count valid subarrays in **O(n)** time.

### Key Idea

* Let `sum` be the cumulative sum of elements up to the current index.
* If at any point `sum - k` has appeared before, it means there exists a subarray ending at the current index whose sum is `k`.
* Store how many times each prefix sum has occurred using a hash map.

### Why It Works

If:

```
currentSum - previousSum = k
```

Then:

```
previousSum = currentSum - k
```

So we just need to count how many times `currentSum - k` has appeared so far.

---

## 🧠 Algorithm

1. Initialize:

   * `sum = 0` (running prefix sum)
   * `res = 0` (result count)
   * HashMap with `{0 → 1}` to handle subarrays starting at index 0
2. Traverse the array:

   * Add current number to `sum`
   * If `(sum - k)` exists in the map, add its count to `res`
   * Update the count of `sum` in the map
3. Return `res`

---

## ✅ Java Implementation

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int res = 0;
        int sum = 0;

        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1); // Base case

        for (int num : nums) {
            sum += num;

            if (map.containsKey(sum - k)) {
                res += map.get(sum - k);
            }

            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }

        return res;
    }
}
```

---

## ⏱️ Complexity Analysis

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(n)` (for the hash map)

---

## 🧪 Example

**Input**

```
nums = [1, 1, 1]
k = 2
```

**Output**

```
2
```

**Explanation**
Subarrays with sum `2`:

* `[1, 1]` (indices 0–1)
* `[1, 1]` (indices 1–2)


---

# Longest Subarray with Sum K (Java)

## 📌 Problem Statement

Given an integer array `arr[]` and an integer `k`, find the **length of the longest subarray** whose sum is equal to `k`.

This solution works for arrays containing **positive, negative, and zero values**.

---

## 💡 Approach: Prefix Sum + HashMap

### Key Idea

* Maintain a running **prefix sum** while iterating through the array.
* If `prefixSum == k`, then the subarray from index `0` to `i` has sum `k`.
* If `(prefixSum - k)` has appeared before, then the subarray between the previous index and current index has sum `k`.
* Store **only the first occurrence** of each prefix sum to maximize subarray length.

---

## 🧠 Algorithm

1. Initialize:

   * `HashMap<Integer, Integer>` to store prefix sum and its first index
   * `prefixSum = 0`
   * `maxLen = 0`
2. Traverse the array:

   * Add current element to `prefixSum`
   * Check if `prefixSum == k`
   * Check if `(prefixSum - k)` exists in the map
   * Update `maxLen` accordingly
   * Store prefix sum if not already present
3. Return `maxLen`

---

## ✅ Java Implementation

```java
import java.util.HashMap;

class Solution {
    public int longestSubarray(int[] arr, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int prefixSum = 0;
        int maxLen = 0;

        for (int i = 0; i < arr.length; i++) {
            prefixSum += arr[i];

            // Case 1: Subarray from 0 to i
            if (prefixSum == k) {
                maxLen = i + 1;
            }

            // Case 2: Subarray ending at i
            if (map.containsKey(prefixSum - k)) {
                maxLen = Math.max(maxLen, i - map.get(prefixSum - k));
            }

            // Store first occurrence only
            if (!map.containsKey(prefixSum)) {
                map.put(prefixSum, i);
            }
        }

        return maxLen;
    }
}
```

---

## 📊 Example

**Input**

```
arr = [10, 5, 2, 7, 1, 9]
k = 15
```

**Output**

```
4
```

**Explanation**
The longest subarray with sum `15` is `[5, 2, 7, 1]`.

---

## ⏱ Complexity Analysis

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(n)`

---

## 🚀 Notes

* This approach handles **negative numbers**, unlike the sliding window technique.
* Efficient and suitable for large inputs.

---

---

## 1. Reverse a Singly Linked List

### 📌 Problem Description

Given the head of a singly linked list, reverse the list and return the new head.

### 🧠 Approach

This solution uses an **iterative approach** with three pointers:

* `prev` – keeps track of the previous node
* `cur` – current node being processed
* `next` – temporarily stores the next node

By reversing the `next` pointer of each node, the list is reversed in-place.

### ✅ Algorithm Steps

1. Initialize `prev` as `null` and `cur` as `head`
2. Iterate through the list:

   * Save `cur.next` in `next`
   * Point `cur.next` to `prev`
   * Move `prev` and `cur` one step forward
3. Return `prev` as the new head

### ⏱️ Complexity

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)`

### 💻 Code

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode cur = head;
        ListNode prev = null;

        while (cur != null) {
            ListNode next = cur.next;
            cur.next = prev;
            prev = cur;
            cur = next;
        }
        return prev;
    }
}
```

---

## 2. Find the Middle of a Singly Linked List

### 📌 Problem Description

Given the head of a singly linked list, return the **middle node**.

* If the list has an even number of nodes, return the **second middle node**.

### 🧠 Approach

This solution uses the **two-pointer technique**:

* `slow` pointer moves one step at a time
* `fast` pointer moves two steps at a time

When `fast` reaches the end, `slow` will be at the middle.

### ✅ Algorithm Steps

1. Initialize both `slow` and `fast` to `head`
2. Move `slow` by one step and `fast` by two steps
3. When `fast` reaches the end, return `slow`

### ⏱️ Complexity

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)`

### 💻 Code

```java
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        return slow;
    }
}
```

---

## 📦 ListNode Definition

Both solutions use the following `ListNode` structure:

```java
public class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) {
        this.val = val;
        this.next = next;
    }
}
```


## 1. Merge Two Sorted Lists

### Problem

Given two sorted linked lists `list1` and `list2`, merge them into a single sorted linked list and return its head.

### Approach

* Use a **dummy node** to simplify list construction.
* Maintain a pointer (`res`) to build the merged list.
* Compare values from both lists and append the smaller node.
* Once one list is exhausted, attach the remaining nodes from the other list.

### Key Concepts

* Dummy node pattern
* Iterative merging
* Pointer manipulation

### Time & Space Complexity

* **Time:** `O(m + n)` where `m` and `n` are lengths of the lists
* **Space:** `O(1)` (in-place merge)

---



## 2. Remove Nth Node From End of List

### Problem

Given the head of a linked list, remove the `n`th node from the end of the list and return the head.

### Approach

* Use a **dummy node** to handle edge cases (e.g., removing the head).
* Use two pointers (`fast` and `slow`).
* Move `fast` ahead by `n + 1` steps.
* Move both pointers until `fast` reaches the end.
* `slow.next` will be the node to remove.

### Key Concepts

* Two-pointer (fast & slow) technique
* Dummy node to simplify edge cases
* Single-pass traversal

### Time & Space Complexity

* **Time:** `O(n)`
* **Space:** `O(1)`

---

## Why Use a Dummy Node?

* Avoids special handling for head removal
* Simplifies pointer logic
* Makes code cleaner and safer

---


## 🧮 1. Add Two Numbers

**Problem Link:**
[https://leetcode.com/problems/add-two-numbers/](https://leetcode.com/problems/add-two-numbers/)

### 🔍 Problem Summary

You are given two non-empty linked lists representing two non-negative integers.
The digits are stored in **reverse order**, and each node contains a single digit.

Add the two numbers and return the sum as a linked list.

---

### 💡 Approach

* Use a **dummy node** to simplify list construction
* Traverse both lists simultaneously
* Keep track of a **carry**
* Add remaining carry at the end if needed

---

### ✅ Java Solution

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode temp = dummy;
        int carry = 0;

        while (l1 != null || l2 != null) {
            int x = (l1 != null) ? l1.val : 0;
            int y = (l2 != null) ? l2.val : 0;

            int sum = x + y + carry;
            carry = sum / 10;

            temp.next = new ListNode(sum % 10);
            temp = temp.next;

            if (l1 != null) l1 = l1.next;
            if (l2 != null) l2 = l2.next;
        }

        if (carry != 0) {
            temp.next = new ListNode(carry);
        }

        return dummy.next;
    }
}
```

---

### ⏱ Complexity

* **Time:** `O(max(n, m))`
* **Space:** `O(max(n, m))`

---



## 🗑️ 2. Delete Node in a Linked List

**Problem Link:**
[https://leetcode.com/problems/delete-node-in-a-linked-list/](https://leetcode.com/problems/delete-node-in-a-linked-list/)

---

### 🔍 Problem Summary

You are given a node (not the tail) in a singly linked list.
Delete the given node **without access to the head** of the list.

---

### 💡 Key Insight

Since we cannot access the previous node:

* Copy the value from the **next node**
* Skip the next node by adjusting pointers

---

### ✅ Java Solution

```java
class Solution {
    public void deleteNode(ListNode node) {
        if (node == null) return;

        node.val = node.next.val;
        node.next = node.next.next;
    }
}
```

---

### ⏱ Complexity

* **Time:** `O(1)`
* **Space:** `O(1)`

---
