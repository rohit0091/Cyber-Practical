# Day 01 - Two Sum

**Date**: 2026-01-01  
**Difficulty**: Easy  
**Topics**: Arrays, Hash Map, Hash Table

---

## 📝 Problem Statement

Given an array of integers `nums` and an integer `target`, return the **indices** of the two numbers such that they add up to `target`.

You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

You can return the answer in any order.

### Example 1:
```
Input: nums = [2, 7, 11, 15], target = 9
Output: [0, 1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

### Example 2:
```
Input: nums = [3, 2, 4], target = 6
Output: [1, 2]
Explanation: Because nums[1] + nums[2] == 6, we return [1, 2].
```

### Example 3:
```
Input: nums = [3, 3], target = 6
Output: [0, 1]
Explanation: Both elements are the same value, but different indices.
```

### Constraints:
- 2 <= nums.length <= 10^4
- -10^9 <= nums[i] <= 10^9
- -10^9 <= target <= 10^9
- Only one valid answer exists.

---

## 💡 Hints

<details>
<summary>Click to reveal Hint 1</summary>

Think about what you need to find for each number. If the current number is `x`, what value are you looking for?

</details>

<details>
<summary>Click to reveal Hint 2</summary>

For each number `x`, you need to find `target - x` in the array. Is there a data structure that allows fast lookups?

</details>

<details>
<summary>Click to reveal Hint 3</summary>

Use a hash map to store numbers you've seen along with their indices. For each new number, check if `target - current_number` exists in the hash map.

</details>

---

## ✅ Solution

### Approach 1: Hash Map (Optimal)

**Intuition:**
The brute force approach would be to check every pair of numbers, which takes O(n²) time. We can optimize this by using a hash map to store the numbers we've seen. For each number, we check if its complement (`target - current_number`) exists in the hash map.

**Algorithm:**
1. Create an empty hash map to store numbers and their indices
2. Iterate through the array
3. For each number, calculate its complement: `complement = target - current_number`
4. Check if the complement exists in the hash map
5. If yes, return the current index and the complement's index
6. If no, add the current number and its index to the hash map
7. Continue until the pair is found

**Implementation (Python):**
```python
def twoSum(nums, target):
    """
    Find two numbers that add up to target.
    
    Args:
        nums: List of integers
        target: Target sum
    
    Returns:
        List of two indices
    """
    seen = {}  # Hash map to store {number: index}
    
    for i, num in enumerate(nums):
        complement = target - num
        
        if complement in seen:
            return [seen[complement], i]
        
        seen[num] = i
    
    return []  # No solution found (shouldn't happen per problem statement)
```

**Implementation (Java):**
```java
import java.util.HashMap;
import java.util.Map;

public class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> seen = new HashMap<>();
        
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            
            if (seen.containsKey(complement)) {
                return new int[] { seen.get(complement), i };
            }
            
            seen.put(nums[i], i);
        }
        
        return new int[] {}; // No solution found
    }
}
```

**Implementation (C++):**
```cpp
#include <vector>
#include <unordered_map>

class Solution {
public:
    std::vector<int> twoSum(std::vector<int>& nums, int target) {
        std::unordered_map<int, int> seen;
        
        for (int i = 0; i < nums.size(); i++) {
            int complement = target - nums[i];
            
            if (seen.find(complement) != seen.end()) {
                return {seen[complement], i};
            }
            
            seen[nums[i]] = i;
        }
        
        return {}; // No solution found
    }
};
```

**Time Complexity**: O(n) - We traverse the array once  
**Space Complexity**: O(n) - Hash map can store up to n elements

---

### Approach 2: Brute Force (Not Recommended)

**Intuition:**
Check every possible pair of numbers to see if they sum to the target.

**Implementation (Python):**
```python
def twoSum_bruteforce(nums, target):
    """Brute force approach - O(n²) time"""
    n = len(nums)
    
    for i in range(n):
        for j in range(i + 1, n):
            if nums[i] + nums[j] == target:
                return [i, j]
    
    return []
```

**Time Complexity**: O(n²) - Nested loops  
**Space Complexity**: O(1) - No extra space needed

---

## 🧪 Test Cases

```python
# Test Case 1
assert twoSum([2, 7, 11, 15], 9) == [0, 1]

# Test Case 2
assert twoSum([3, 2, 4], 6) == [1, 2]

# Test Case 3 - Same values
assert twoSum([3, 3], 6) == [0, 1]

# Edge Case - Negative numbers
assert twoSum([-1, -2, -3, -4, -5], -8) == [2, 4]

# Edge Case - Zero in array
assert twoSum([0, 4, 3, 0], 0) == [0, 3]
```

---

## 📚 Key Takeaways

- **Hash maps are excellent for O(1) lookups** - Converting a two-loop problem into a single loop
- **Store complementary information** - Instead of searching for the target directly, store what you've seen and check for complements
- **Trade space for time** - Using O(n) extra space to achieve O(n) time instead of O(n²)
- **One-pass hash map** - We can build the hash map while searching, no need for two passes

---

## 🔗 Related Problems

- [Three Sum](https://leetcode.com/problems/3sum/) - Extension with three numbers
- [Four Sum](https://leetcode.com/problems/4sum/) - Extension with four numbers
- [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) - Optimized version for sorted arrays

---

## 📝 Personal Notes

This is a classic problem that introduces the concept of using hash maps to optimize search operations. The key insight is recognizing that for each number, we only need to check if its complement exists, rather than checking all pairs.
