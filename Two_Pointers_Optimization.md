# Two Pointers: The $O(N)$ Optimization Guide

This documentation covers the three primary "Two Pointer" strategies used in Competitive Programming to reduce $O(N^2)$ brute-force solutions to $O(N)$ efficiency.

## 1. Converging Pointers (The "Opposite Ends" Search)

Used primarily on sorted arrays to find pairs or triplets that satisfy a specific sum or condition.

**Mechanism:** L starts at $0$, R starts at $n-1$. They move toward each other.

**The Logic:** Since the array is sorted, we take the best choice at each step. If the current pair fails the condition, we can mathematically prove that an entire set of other pairs involving that point also fails, allowing us to skip them entirely.

**Example:** If nums[L] + nums[R] is too small, nums[L] added to any other number to the left of R will also be too small. We discard nums[L] forever.

### Shortest CP Code (Two Sum)

```cpp
while (L < R) {
    int sum = nums[L] + nums[R];
    if (sum == target) return {L, R};
    (sum < target) ? L++ : R--; // Take the best next choice
}
```

## 2. Sliding Window (The "Caterpillar" Method)

Used to find a contiguous subarray or substring that satisfies a property (e.g., sum, unique characters).

**Mechanism:** Both pointers start at $0$. This functions exactly like a Caterpillar:

- **Extend:** The "Head" ($j$) stretches forward to expand the window until the condition is met.
- **Shrink:** The "Tail" ($i$) pulls forward to shrink the window and find the best answer (shortest/longest) until the condition fails.
- **Repeat:** Once the condition fails, the head stretches forward again.

### Shortest CP Code (Smallest Subarray Sum $\ge S$)

```cpp
for (int j = 0; j < n; j++) {
    sum += nums[j]; // Head extends
    while (sum >= S) { // Condition met
        minLen = min(minLen, j - i + 1); // Record best answer
        sum -= nums[i++]; // Tail shrinks
    }
}
```

## 3. The Runner (The "Fast and Slow" Cycle Finder)

Used for detecting cycles in Linked Lists or Arrays (where values act as indices).

**Mechanism:** slow moves 1 step; fast moves 2 steps.

**The Logic:** In a cycle, the relative speed difference of 1 ensures the fast pointer will eventually "lap" the slow pointer, meeting them at the same node.

### Shortest CP Code (Cycle Detection)

```cpp
while (fast && fast->next) {
    slow = slow->next;
    fast = fast->next->next;
    if (slow == fast) return true; // Cycle detected
}
```
