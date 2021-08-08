# Palindrome Partitioning II

Given a string `s`, partition `s` such that every substring of the partition is a palindrome.

Return the minimum cuts needed for a palindrome partitioning of `s`.

## Example 1:

```go
Input: s = "aab"
Output: 1
Explanation: The palindrome partitioning ["aa","b"] could be produced using 1 cut.
```

## Example 2

```go
Input: s = "a"
Output: 0
```

## Example 3

```go
Input: s = "ab"
Output: 1
```

## Constraints

- `1 <= s.length <= 2000`
- `s` consists of lower-case English letters only.

## Solution

Using DP with 2 states:
- isPalindrome `[len(s)][len(s)]bool`: Whether the string from i to j is a valid palindrome.
- minCut `[]int`: minCut[i] means the minimum number of cuts from 0 to i

Interate through the string with `left` and `right` pointers

If two chars are equal `(s[left] == s[right)` , there can be two cases:
- Even: `right > left <= 1`, means `right = left` or `right` next to `left`, eg: `aa`
- Odd: the middle can be different, eg: `acbca`, then we need to check if `left + 1` and `right - 1` make a valid palindrome

When we're able to determine the palindrome
- if `left == 0` then `0` to `right` is a palindrome, we dont need to cut => minCut = 0
- else `minCut = min(minCut[left - 1] + 1, minCut[right])`

The result will be `minCut[len(s) - 1]`

### Code

```go
func minCut(s string) int {
    if s == "" {
        return 0
    }
    
    length := len(s)
    
    // Minimum number of cuts for s[0:j]
    minCut := make([]int, length)
    
    // isPalindrome[i][j] = true means s[i]...s[j] is a palindrome
    isPalindrome := make([][]bool, length)
    for i := 0; i < length; i++ {
        isPalindrome[i] = make([]bool, length)
    }
    
    for right := 0; right < len(s); right++ {
        // a single char is always palindrome itself
        minCut[right] = right
        isPalindrome[right][right] = true
        
        for left:=0; left <= right; left++ {
            // s[left]...s[right] is a palindrome
            // right - left <= 1 other OR isPalindrome[left + 1][right - 1] = TRUE, which means odd cases
            if s[left] == s[right] && (right - left <= 1 || isPalindrome[left + 1][right - 1]) {
                // if left is 0, then s[0:right] is a palindrome, we dont need to cut
                if left == 0 {
                    minCut[right] = 0
                } else {
                    isPalindrome[left][right] = true
                    // from left to right we're gonna need 1 cut, so minCut at right will be min of minCut[left - 1] + 1 OR minCut[right]
                    minCut[right] = min(minCut[left - 1] + 1, minCut[right])
                }
            }
        }
    }
    
    return minCut[length - 1]
}

func min(a int, b int) int {
    if a > b {
        return b
    }
    return a
}
```

