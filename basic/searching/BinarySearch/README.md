# Binary Search

The essence of binary search lies not in "monotoncity" but in "boundaries." As long as a property exists that allows the interval to be split into two, binary search can be used to pinpoint the boundary point.

The following templates assume `0 <= left <= right` and that both values fall within the range of a 32-bit `int`. The midpoint is calculated using the difference between the bounds to avoid overflow associated with `left+right`

## AlgorithM Templates

### Template 1

```java
boolean check(int x) {
}

int search(int left, int right) {
    while (left < right) {
        int mid = left + ((right - left) >> 1);
        if (check(mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    return left;
}
```

### Template 2

```java
boolean check(int x) {
}

int search(int left, int right) {
    while (left < right) {
        int mid = left + ((right - left) >> 1) + ((right - left) & 1);
        if (check(mid)) {
            left = mid;
        } else {
            right = mid - 1;
        }
    }
    return left;
}
```

When solving binary search problems you can follow this

1. Set the loop condition to $left<right$;
2. Inside the loop, start by writing $mid = left + \lfloor \frac{right - left}{2} \rfloor$;
3. Implement the $check()$ function based on the specific problem (for very simple logic, a separate $check$ function may not be necessary), and decide whether to use $right = mid$ (Template 1) or $left = mid$ (Template 2):
- If using $right = mid$, the corresponding `else` statement is $left = mid + 1$, and the calculation for $mid$ remains unchanged: $mid = left + \lfloor \frac{right - left}{2} \rfloor$;
- If using $left = mid$, the corresponding `else` statement is $right = mid - 1$, and you must account for the remainder when the range size is odd by adjusting the $mid$ calculation: $mid = left + \lfloor \frac{right - left}{2} \rfloor + ((right - left) \bmod 2)$;
4. Upon loop termination, $left$ and $right$ will be equal.

Note that the advantage of these two templates is that the answer is always maintained within the binary search interval, and the value at the termination point corresponds exactly to the answer's location. For cases where there might be no solution, simply check whether the final $left$ or $right$ value satisfies the problem's conditions.

## Example Problem
[Find First and Last Position of Element in Sorted Array](/solution/0000-0099/0034.Find%20First%20and%20Last%20Position%20of%20Element%20in%20Sorted%20Array/README.md)
- [Sqrt(x)](/solution/0000-0099/0069.Sqrt%28x%29/README.md)
- [Find Peak Element](/solution/0100-0199/0162.Find%20Peak%20Element/README.md)
- [First Bad Version](/solution/0200-0299/0278.First%20Bad%20Version/README.md)
- [Fixed Point](/solution/1000-1099/1064.Fixed%20Point/README.md)