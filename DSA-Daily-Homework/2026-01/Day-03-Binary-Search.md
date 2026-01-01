# Day 03 - Binary Search

**Date**: 2026-01-03  
**Difficulty**: Medium  
**Topics**: Arrays, Binary Search, Divide and Conquer

---

## 📝 Problem Statement

Given a **sorted** array of integers `nums` and an integer `target`, write a function to search for `target` in `nums`. If `target` exists, return its index. Otherwise, return `-1`.

You must write an algorithm with **O(log n)** runtime complexity.

### Example 1:
```
Input: nums = [-1, 0, 3, 5, 9, 12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```

### Example 2:
```
Input: nums = [-1, 0, 3, 5, 9, 12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```

### Example 3:
```
Input: nums = [5], target = 5
Output: 0
Explanation: Single element array
```

### Constraints:
- 1 <= nums.length <= 10^4
- -10^4 < nums[i], target < 10^4
- All integers in `nums` are **unique**
- `nums` is sorted in **ascending order**

---

## 💡 Hints

<details>
<summary>Click to reveal Hint 1</summary>

Since the array is sorted, you can eliminate half of the remaining elements with each comparison. What algorithm does this?

</details>

<details>
<summary>Click to reveal Hint 2</summary>

Compare the target with the middle element. If they match, you found it! If target is smaller, search the left half. If target is larger, search the right half.

</details>

<details>
<summary>Click to reveal Hint 3</summary>

Use two pointers (left and right) to track the search range. Calculate mid = (left + right) // 2, but be careful of integer overflow in some languages!

</details>

---

## ✅ Solution

### Approach 1: Binary Search (Iterative)

**Intuition:**
Binary search works on sorted arrays by repeatedly dividing the search space in half. We compare the target with the middle element and eliminate half of the array based on the comparison. This gives us O(log n) time complexity.

**Algorithm:**
1. Initialize two pointers: `left = 0` and `right = len(nums) - 1`
2. While `left <= right`:
   - Calculate middle index: `mid = left + (right - left) // 2` (avoids overflow)
   - If `nums[mid] == target`, return `mid`
   - If `nums[mid] < target`, search right half: `left = mid + 1`
   - If `nums[mid] > target`, search left half: `right = mid - 1`
3. If target not found, return `-1`

**Implementation (Python):**
```python
def search(nums, target):
    """
    Binary search in sorted array.
    
    Args:
        nums: Sorted array of integers
        target: Target value to find
    
    Returns:
        Index of target, or -1 if not found
    """
    left, right = 0, len(nums) - 1
    
    while left <= right:
        # Calculate mid (avoids overflow in other languages)
        mid = left + (right - left) // 2
        
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1  # Search right half
        else:
            right = mid - 1  # Search left half
    
    return -1  # Target not found
```

**Implementation (Java):**
```java
public class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        
        while (left <= right) {
            // Prevents integer overflow
            int mid = left + (right - left) / 2;
            
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return -1;
    }
}
```

**Implementation (C++):**
```cpp
#include <vector>

class Solution {
public:
    int search(std::vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        return -1;
    }
};
```

**Time Complexity**: O(log n) - We halve the search space with each iteration  
**Space Complexity**: O(1) - Only using a constant amount of variables

---

### Approach 2: Binary Search (Recursive)

**Intuition:**
Binary search can also be implemented recursively, which some find more intuitive. Each recursive call searches a smaller portion of the array.

**Implementation (Python):**
```python
def search_recursive(nums, target):
    """Binary search using recursion"""
    
    def binary_search(left, right):
        if left > right:
            return -1
        
        mid = left + (right - left) // 2
        
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            return binary_search(mid + 1, right)
        else:
            return binary_search(left, mid - 1)
    
    return binary_search(0, len(nums) - 1)
```

**Time Complexity**: O(log n) - Same as iterative  
**Space Complexity**: O(log n) - Recursive call stack depth

---

## 🧪 Test Cases

```python
# Test Case 1 - Target exists in middle
assert search([-1, 0, 3, 5, 9, 12], 9) == 4

# Test Case 2 - Target doesn't exist
assert search([-1, 0, 3, 5, 9, 12], 2) == -1

# Test Case 3 - Single element (found)
assert search([5], 5) == 0

# Test Case 4 - Single element (not found)
assert search([5], 3) == -1

# Test Case 5 - Target at beginning
assert search([1, 2, 3, 4, 5], 1) == 0

# Test Case 6 - Target at end
assert search([1, 2, 3, 4, 5], 5) == 4

# Test Case 7 - Two elements
assert search([1, 3], 3) == 1

# Test Case 8 - Large array
assert search(list(range(0, 10000, 2)), 5000) == 2500
```

---

## 📚 Key Takeaways

- **Binary search requires sorted data** - The algorithm depends on the ordering property
- **O(log n) is very efficient** - Even for a billion elements, binary search needs only ~30 comparisons
- **Avoid integer overflow** - Use `mid = left + (right - left) // 2` instead of `mid = (left + right) // 2`
- **Edge conditions matter** - Pay attention to `left <= right` vs `left < right` based on your implementation
- **Iterative vs Recursive** - Iterative saves space (no call stack), recursive is often more readable

### Common Binary Search Patterns:
1. **Finding exact value** (this problem)
2. **Finding insert position** (leftmost/rightmost position)
3. **Finding peak element** (in mountain arrays)
4. **Search in rotated sorted arrays**
5. **Finding minimum/maximum** that satisfies a condition

---

## 🔗 Related Problems

- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Find position to insert target
- [First Bad Version](https://leetcode.com/problems/first-bad-version/) - Binary search variant
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Modified binary search
- [Find Peak Element](https://leetcode.com/problems/find-peak-element/) - Binary search application

---

## 📝 Personal Notes

Binary search is one of the most fundamental algorithms in computer science. While the concept is simple (divide and conquer), getting the implementation details right (boundary conditions, when to use `<=` vs `<`, how to update pointers) requires practice. The key insight is that we can eliminate half of the search space with each comparison because the array is sorted.

**Common Pitfalls:**
- Infinite loops due to incorrect pointer updates
- Off-by-one errors in boundary conditions
- Integer overflow when calculating mid (in languages like Java/C++)
