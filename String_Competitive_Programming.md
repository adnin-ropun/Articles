# std::string: for Competitive Programming

In Competitive Programming, a string is a dynamic array of characters. It's **faster** than a `vector<char>` for text tasks and **much safer** than C-style `char[]`.

---

## 1. Essential Operations Table

| What You Want | How to Do It | Complexity |
|---------------|-------------|-----------|
| Create | `string s = "text";` | $O(N)$ |
| Length | `s.size()` or `s.length()` | $O(1)$ |
| First char | `s.front()` or `s[0]` | $O(1)$ |
| Last char | `s.back()` or `s[s.size()-1]` | $O(1)$ |
| Add char | `s += 'a';` or `s.push_back('a');` | $O(1)$ amortized |
| Remove last | `s.pop_back();` | $O(1)$ |
| Find text | `s.find("abc")` | $O(N \cdot M)$ |
| Get substring | `s.substr(pos, len)` | $O(\text{len})$ |
| Sort | `sort(s.begin(), s.end());` | $O(N \log N)$ |
| Reverse | `reverse(s.begin(), s.end());` | $O(N)$ |
| To number | `stoi(s)` or `stoll(s)` | $O(N)$ |
| To string | `to_string(num)` | $O(\log_{10} V)$ |
| Read line | `getline(cin, s);` | $O(N)$ |
| Empty? | `s.empty()` | $O(1)$ |
| Clear | `s.clear();` | $O(1)$ |

---

### String as Array (Raw Access)

Sometimes you need to interface with C-style functions or use pointers.

```cpp
string s = "Hello";
char* cstr = s.data(); // Get raw pointer (C++11)
cout << cstr[1];       // Prints 'e'
```

### Check if String is Numeric

A very common task in parsing problems.

```cpp
bool allDigits = all_of(s.begin(), s.end(), ::isdigit);
```

### String Comparison (Lexicographical)

Strings are compared based on ASCII values, character by character.

```cpp
string a = "apple", b = "apply";
if (a < b) // true, because 'e' < 'y'
    cout << "apple comes first";
```

---

### Rule 1: Avoid Concatenating with `+` in Loops

**Don't do this:**
```cpp
for (int i = 0; i < n; i++) {
    s = s + char(i); // O(N) - Creates new copy each time!
}
```

**Do this instead:**
```cpp
for (int i = 0; i < n; i++) {
    s += char(i); // O(1) amortized
}
```

---

### Rule 2: Use safe find()

When using `s.find()`, always check against `string::npos`.

```cpp
if (s.find("target") != string::npos) {
    // Found it!
    int pos = s.find("target");
} else {
    // Not found
}
```

---

### Rule 3: Avoid Copying

When passing a string to a function, use `const string&` to avoid a slow $O(N)$ copy.

```cpp
// Bad: Copies entire string
void process(string s) { /* ... */ }

// Good: References the original
void process(const string& s) { /* ... */ }
```

---

### Rule 4: Use `getline()` Correctly

If you use `cin >> x` before `getline()`, the newline character stays in the buffer. Clear it with `cin.ignore()` first.

```cpp
int n;
cin >> n;
cin.ignore();  // Clear the newline from input buffer
string line;
getline(cin, line);  // Now reads correctly
```

---

## 4.Cheat Sheet

```cpp
#include <string>
#include <algorithm>

string s = "hello";

// Navigation
s[0];              // 'h'
s.front();         // 'h'
s.back();          // 'o'
s.at(1);           // 'e' (with bounds checking)

// Modification
s += 'x';          // "helloo"
s.push_back('x');  // "helloox"
s.pop_back();      // "helloo"
s.clear();         // ""

// Searching
s.find("lo");      // finds at position 3
s.rfind("l");      // reverse find
s.find_first_of("aeiou"); // first vowel

// Substring operations
s.substr(1, 3);    // "ell"
s.insert(2, "XX"); // "heXXllo"
s.erase(2, 2);     // "helo"
s.replace(0, 5, "goodbye"); // "goodbye"

// Comparison
s == "hello";      // true/false
s < "world";       // lexicographical
s.compare("hello"); // returns 0 if equal

// Converting
stoi("123");       // to int
stoll("123456789"); // to long long
stof("3.14");      // to float
to_string(42);     // "42"

// Sorting & reversing
sort(s.begin(), s.end());
reverse(s.begin(), s.end());
```

---

## 5. CP Patterns

### Pattern 1: Building a String Character by Character
```cpp
string result = "";
for (char c : input) {
    if (isvalid(c)) {
        result += c;  // Always use += not +
    }
}
```

### Pattern 2: Frequency Counting
```cpp
string s = "aabbcc";
map<char, int> freq;
for (char c : s) freq[c]++;
```

### Pattern 3: Palindrome Check
```cpp
bool isPalindrome(string s) {
    return s == string(s.rbegin(), s.rend());
}
```

### Pattern 4: Anagram Check
```cpp
bool isAnagram(string a, string b) {
    sort(a.begin(), a.end());
    sort(b.begin(), b.end());
    return a == b;
}
```
