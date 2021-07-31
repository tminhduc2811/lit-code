# Map Sum Pairs
Implement your data structure
- `MapSum()` Initializes the `MapSum` object.
- `void insert(String key, int val)` Inserts the key-val pair into the map. If the key already existed, the original key-value pair will be overridden to the new one.
- `int sum(string prefix)` Returns the sum of all the pairs' value whose `key` starts with the `prefix`.

## Example
```go
["MapSum", "insert", "sum", "insert", "sum"]
[[], ["apple", 3], ["ap"], ["app", 2], ["ap"]]
Output
[null, null, 3, null, 5]
```
### Explanation
```go
MapSum mapSum = new MapSum();
mapSum.insert("apple", 3);  
mapSum.sum("ap");           // return 3 (apple = 3)
mapSum.insert("app", 2);    
mapSum.sum("ap");           // return 5 (apple + app = 3 + 2 = 5)
```

## Solution
It is straightforward

```go
type MapSum struct {
    mapValue map[string]int
}


/** Initialize your data structure here. */
func Constructor() MapSum {
    return MapSum{
        mapValue: make(map[string]int),
    }
}


func (this *MapSum) Insert(key string, val int)  {
    this.mapValue[key] = val
}


func (this *MapSum) Sum(prefix string) int {
    sum := 0
    for k, v := range this.mapValue {
        if strings.HasPrefix(k, prefix) {
            sum += v
        }
    }
    return sum
}
```
