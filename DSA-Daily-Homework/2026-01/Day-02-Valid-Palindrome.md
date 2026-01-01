# Day 02 - Valid Palindrome

**Date**: 2026-01-02  
**Difficulty**: Easy  
**Topics**: Strings, Two Pointers

---

## 📝 Problem Statement

A phrase is a **palindrome** if, after converting all uppercase letters to lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` if it is a palindrome, or `false` otherwise.

### Example 1:
```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

### Example 2:
```
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```

### Example 3:
```
Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
```

### Constraints:
- 1 <= s.length <= 2 * 10^5
- s consists only of printable ASCII characters.

---

## 💡 Hints

<details>
<summary>Click to reveal Hint 1</summary>

You need to compare characters from both ends of the string. What pointer technique allows you to do this efficiently?

</details>

<details>
<summary>Click to reveal Hint 2</summary>

Use two pointers - one starting from the beginning and one from the end. Move them towards each other, skipping non-alphanumeric characters.

</details>

<details>
<summary>Click to reveal Hint 3</summary>

Don't create a new string by filtering/cleaning the input. Instead, skip invalid characters on the fly using the two-pointer technique.

</details>

---

## ✅ Solution

### Approach 1: Two Pointers (Optimal)

**Intuition:**
We can use two pointers starting from both ends of the string and move them towards the center. For each position, we skip non-alphanumeric characters and compare the valid characters (converted to lowercase). If all comparisons match, it's a palindrome.

**Algorithm:**
1. Initialize two pointers: `left` at the start (0) and `right` at the end (len(s) - 1)
2. While `left < right`:
   - Skip non-alphanumeric characters from the left
   - Skip non-alphanumeric characters from the right
   - Compare characters at both pointers (case-insensitive)
   - If they don't match, return False
   - Move both pointers inward
3. If we complete the loop without finding mismatches, return True

**Implementation (Python):**
```python
def isPalindrome(s):
    """
    Check if string is a valid palindrome.
    
    Args:
        s: Input string
    
    Returns:
        Boolean indicating if s is a palindrome
    """
    left, right = 0, len(s) - 1
    
    while left < right:
        # Skip non-alphanumeric characters from left
        while left < right and not s[left].isalnum():
            left += 1
        
        # Skip non-alphanumeric characters from right
        while left < right and not s[right].isalnum():
            right -= 1
        
        # Compare characters (case-insensitive)
        if s[left].lower() != s[right].lower():
            return False
        
        left += 1
        right -= 1
    
    return True
```

**Implementation (Java):**
```java
public class Solution {
    public boolean isPalindrome(String s) {
        int left = 0;
        int right = s.length() - 1;
        
        while (left < right) {
            // Skip non-alphanumeric from left
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }
            
            // Skip non-alphanumeric from right
            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }
            
            // Compare characters
            if (Character.toLowerCase(s.charAt(left)) != 
                Character.toLowerCase(s.charAt(right))) {
                return false;
            }
            
            left++;
            right--;
        }
        
        return true;
    }
}
```

**Implementation (C++):**
```cpp
#include <string>
#include <cctype>

class Solution {
public:
    bool isPalindrome(std::string s) {
        int left = 0;
        int right = s.length() - 1;
        
        while (left < right) {
            // Skip non-alphanumeric from left
            while (left < right && !isalnum(s[left])) {
                left++;
            }
            
            // Skip non-alphanumeric from right
            while (left < right && !isalnum(s[right])) {
                right--;
            }
            
            // Compare characters
            if (tolower(s[left]) != tolower(s[right])) {
                return false;
            }
            
            left++;
            right--;
        }
        
        return true;
    }
};
```

**Time Complexity**: O(n) - We traverse the string once with two pointers  
**Space Complexity**: O(1) - Only using two pointer variables

---

### Approach 2: Filter and Compare (Alternative)

**Intuition:**
First clean the string by removing non-alphanumeric characters and converting to lowercase, then check if it equals its reverse.

**Implementation (Python):**
```python
def isPalindrome_filter(s):
    """Alternative approach using string filtering"""
    # Filter and clean the string
    cleaned = ''.join(char.lower() for char in s if char.isalnum())
    
    # Check if it equals its reverse
    return cleaned == cleaned[::-1]
```

**Time Complexity**: O(n) - Filtering and reversing both take O(n)  
**Space Complexity**: O(n) - Creating a new cleaned string

---

## 🧪 Test Cases

```python
# Test Case 1 - Classic palindrome with punctuation
assert isPalindrome("A man, a plan, a canal: Panama") == True

# Test Case 2 - Not a palindrome
assert isPalindrome("race a car") == False

# Test Case 3 - Empty/whitespace
assert isPalindrome(" ") == True

# Test Case 4 - Single character
assert isPalindrome("a") == True

# Test Case 5 - Numbers included
assert isPalindrome("0P") == False

# Test Case 6 - All non-alphanumeric
assert isPalindrome(".,") == True

# Test Case 7 - Mixed case palindrome
assert isPalindrome("RaceCar") == True
```

---

## 📚 Key Takeaways

- **Two-pointer technique** is efficient for palindrome checking - no need to reverse or create new strings
- **In-place processing** saves memory - skip invalid characters on the fly rather than preprocessing
- **Case-insensitive comparison** can be done during iteration - no need to create a lowercase copy
- **Edge cases matter** - empty strings, single characters, and all non-alphanumeric characters

---

## 🔗 Related Problems

- [Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/) - Palindrome with one character deletion allowed
- [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) - Check if linked list is palindrome
- [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/) - Find longest palindrome in string

---

## 📝 Personal Notes

This problem demonstrates the power of the two-pointer technique for in-place string processing. The key insight is that we don't need to create a cleaned version of the string - we can skip invalid characters as we go. This saves both time and space.
