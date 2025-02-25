# Reversing Words in a String: A Deep Dive into Optimized Solutions

When working with strings, one common problem is reversing the order of words in a given sentence. This question frequently appears in coding interviews, testing a candidate's ability to manipulate strings efficiently.

## Problem Statement

Given an input string `s`, reverse the order of words. A word is defined as a sequence of non-space characters. The words in `s` will be separated by at least one space.

The output string should:
- Have words in reverse order.
- Contain only a single space between words.
- Not have leading or trailing spaces.

### Examples:

#### Example 1:
**Input:**  
`s = "the sky is blue"`  
**Output:**  
`"blue is sky the"`

#### Example 2:
**Input:**  
`s = "  hello world  "`  
**Output:**  
`"world hello"`

#### Example 3:
**Input:**  
`s = "a good   example"`  
**Output:**  
`"example good a"`

## Understanding the Problem

The problem essentially requires us to:
1. Split the string into words.
2. Remove extra spaces (leading, trailing, and in-between multiple spaces).
3. Reverse the order of words.
4. Return the resulting string with only single spaces between words.

## Brute Force Approach

A straightforward way to solve this problem is:
1. Split the string by spaces (`split(" ")`).
2. Filter out empty strings to remove extra spaces.
3. Reverse the array of words.
4. Join the words with a single space.

### TypeScript Implementation:
```typescript
function reverseWords(s: string): string {
    return s.trim().split(/\s+/).reverse().join(" ");
}
```
### Explanation:
1. `trim()` removes leading and trailing spaces.
2. `split(/\s+/)` splits the string into words, handling multiple spaces.
3. `reverse()` reverses the word order.
4. `join(" ")` joins the words with a single space.

### Time and Space Complexity:
- **Time Complexity:** O(N) (trimming, splitting, reversing, and joining all take linear time).
- **Space Complexity:** O(N) (storing the words in an array takes extra space).

## Optimized Approach: In-Place String Manipulation

If the string is mutable (e.g., in languages like C++), we can perform the reversal in-place with O(1) extra space. Since TypeScript strings are immutable, we can use an efficient two-pointer approach that mimics in-place behavior:

### Optimized TypeScript Implementation:
```typescript
function reverseWordsOptimized(s: string): string {
    let result = "";
    let i = s.length - 1;
    
    while (i >= 0) {
        while (i >= 0 && s[i] === ' ') i--; // Skip trailing spaces
        if (i < 0) break;
        
        let j = i;
        while (j >= 0 && s[j] !== ' ') j--; // Find the word boundary
        
        result += (result.length === 0 ? "" : " ") + s.substring(j + 1, i + 1);
        i = j - 1; // Move to the next word
    }
    return result;
}
```

### Explanation:
1. Traverse the string from the end to find words.
2. Extract each word and append it to the result.
3. Use condition checks to avoid extra spaces.

### Time and Space Complexity:
- **Time Complexity:** O(N) (single pass to collect words).
- **Space Complexity:** O(1) (only extra space for the result string).

## Conclusion
- The brute force approach is simple but uses extra space.
- The optimized approach mimics in-place reversal and is more efficient in terms of space.
- In coding interviews, showcasing multiple solutions and optimizing them step-by-step can demonstrate problem-solving skills effectively.

**Would you use the optimized approach in real-world scenarios? Share your thoughts in the comments!**

