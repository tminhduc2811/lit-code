# My Pow
Implement `pow(x, n)`, which calculates `x` raised to the power `n` (i.e., xn).

## Example
```go
Input: x = 2.00000, n = 10
Output: 1024.00000
```

```go
Input: x = 2.10000, n = 3
Output: 9.26100
```

```go
Input: x = 2.00000, n = -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25
```

## Constraints
```
-100.0 < x < 100.0
-231 <= n <= 231-1
-104 <= xn <= 104
```

## Solution
The questions seems straightforward though the idea behind it is to use multiply as many time as we can.

Given we can evaluate `x^24` by a for loop 24 times. But this is not sufficient, we can also calculate it by 

`x^24 = x^12 * x^12`, `x^12 = x^6 * x^6`, and so on.
This gives us `Olog(n)` complexity

- How about the odd cases: `x^25 = x * x^12 * x^12`
- How about the negative pow: `x^-24 = (1/x)^24`

```go
func myPow(x float64, n int) float64 {
    // if the number is the smallest of float32 (1.175494 × 10-38) return 0 directly
    if math.Abs(x) < 1e-40 {
        return 0
    }
    // if n is 1, return x
    if n == 1 {
        return x
    }
    // if n is 0, return 1
    if n == 0 {
        return 1
    }
    // if n is negative, we can turn devide => multiple
    if n < 0 {
        return myPow(1/x, -n)
    }
    lower := myPow(x, n/2)
    if n%2 == 0 {
        return lower * lower
    }
    return x * lower * lower
}

```
