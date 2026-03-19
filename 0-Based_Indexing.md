# Why 0-Based Indexing?

## The Distance Rule

**Calculate element count instantly**: Length = End - Start (excluded)

**Formula**: For a range from index $A$ to index $B$ (excluded), count = $B - A$

**Example**: String "PYTHON", substring from index 0 to 2:
- Length: $2 - 0 = 2$
- Characters: 'P', 'Y' (indices [0, 1])
- Code: `substr(0, 2)`

---

## Splitting and Merging

The end index of one slice is the start index of the next—no gaps or overlaps.

**Formula**: Array split at index $i$ gives: $[0, i)$ and $[i, n)$

- No index used twice
- No index skipped

---

## Offsets vs. Positions

**Index meaning**: Not a rank (1st, 2nd, 3rd), but a distance from the start.

**Formula**: `Address + Index = Element Location`

**Example**: Box of 8 cupcakes:
- Position: "the 1st cupcake"
- Offset: "0 steps from left edge" → `cake[0]`
---

## Practical Examples

### Example 1: The Distance Rule

**Problem**: Extract username from email "alex@example.com"

```cpp
#include <iostream>
#include <string>

int main() {
    std::string email = "alex@example.com";
    
    int end = email.find('@');    // end = 4
    int start = 0;
    int length = end - start;     // 4 - 0 = 4
    
    std::string username = email.substr(start, length);
    
    std::cout << "Username: " << username << std::endl;  // Output: alex
    return 0;
}
```

**Note**: No `+1` or `-1` needed. Length is exactly `end - start`.

---

### Example 2: Splitting and Merging

**Problem**: Split array [10, 20, 30, 40, 50, 60] in half, then recombine

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> original = {10, 20, 30, 40, 50, 60};
    int m = original.size() / 2;  // m = 3
    
    // Left: indices [0, 3)  →  {10, 20, 30}
    std::vector<int> left(original.begin(), original.begin() + m);
    
    // Right: indices [3, 6)  →  {40, 50, 60}
    std::vector<int> right(original.begin() + m, original.end());
    
    // Merge back
    std::vector<int> merged;
    merged.insert(merged.end(), left.begin(), left.end());
    merged.insert(merged.end(), right.begin(), right.end());
    
    return 0;
}
```

**Note**: Boundaries align perfectly—no overlap, no gaps.
