# Binary Search: Where the Truth Flips

A monotonic sequence of boolean values changes exactly once. Binary search finds that flip point.

**False ... False ... True ... True**  
The flip is the first True.

---

## First True (Minimum)

```cpp
int L = 0, R = n;
while (L < R) {
    int mid = L + (R - L) / 2;
    if (check(mid)) R = mid;  // True → go left
    else L = mid + 1;         // False → go right
}
return L;  // First index where check() is true
```
Finds the first position where the condition becomes true by shrinking the right boundary when true.

---

## Last True (Maximum)

```cpp
int L = 0, R = n;
while (L < R) {
    int mid = L + (R - L) / 2;
    if (check(mid)) L = mid + 1;  // True → go right
    else R = mid;                 // False → go left
}
return L - 1;  // Last index where check() was true
```
Finds the last position where the condition is true by moving the left boundary past it.

---

## Lower Bound (First ≥ target)

```cpp
int L = 0, R = n;
while (L < R) {
    int mid = L + (R - L) / 2;
    if (arr[mid] >= target) R = mid;
    else L = mid + 1;
}
return L;
```
Finds the smallest index where the array element is greater than or equal to the target value.

---

## Upper Bound (First > target)

```cpp
int L = 0, R = n;
while (L < R) {
    int mid = L + (R - L) / 2;
    if (arr[mid] > target) R = mid;
    else L = mid + 1;
}
return L;
```
Finds the smallest index where the array element is strictly greater than the target value.

---

## Floating Point

```cpp
double L = 0, R = 1e9;
for (int i = 0; i < 80; i++) {
    double mid = (L + R) / 2;
    if (check(mid)) R = mid;
    else L = mid;
}
return L;
```
Uses fixed iterations to find a real-valued answer with exponential precision; 80 iterations guarantee 2⁻⁸⁰ precision.

---

## The Pattern

| Goal | Condition True | Return |
|------|----------------|--------|
| First true | `R = mid` | `L` |
| Last true | `L = mid + 1` | `L - 1` |
| Lower bound | `R = mid` | `L` |
| Upper bound | `R = mid` | `L` |
