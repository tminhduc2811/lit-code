# Group Anagrams
Given an array of strings `strs`, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Example 1

```go
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

## Example 2

```go
Input: strs = [""]
Output: [[""]]
```

## Example 3

```go
Input: strs = ["a"]
Output: [["a"]]
```

## Constraints

- `1 <= strs.length <= 104`
- `0 <= strs[i].length <= 100`
- `strs[i]` consists of lower-case English letters.

## Solution
- Use an array to store the frequency of characters in a string as a map key. Because from `a` to `z`, there are 26 characters => we only need an array at maximum 26 length.
- The result will be all values in the map

```go
func groupAnagrams(strs []string) [][]string {
    strMap := map[[26]int][]string{}
    for _, str := range strs {
        key := [26]int{}
        for i:=0; i < len(str); i++ {
            key[str[i] - 'a'] += 1
        }
        strMap[key] = append(strMap[key], str)
    }
    result := [][]string{}
    for _, v := range strMap {
        result = append(result, v)
    }
    return result
}

```
