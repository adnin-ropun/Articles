# C++ Maps: Complete Guide for CP

## ⚡ Quick Selection Guide

| Need | Container |
|------|-----------|
| Sorted + Unique keys | `map` |
| Sorted + Duplicate keys | `multimap` |
| Fast lookup + Unique keys | `unordered_map` |
| Fast lookup + Duplicate keys | `unordered_multimap` |

---

## Summary

| Container | What It Is | Time | Best For |
|-----------|-----------|------|----------|
| **map** | Sorted (Red-Black Tree), unique keys | O(log n) | Phonebook: name→number, sorted by name |
| **unordered_map** | Hash table, unique keys | O(1) avg | Cache, frequency counter, quick lookup |
| **multimap** | Sorted, duplicate keys allowed | O(log n) | Dictionary: word→multiple meanings |
| **unordered_multimap** | Hash table, duplicate keys allowed | O(1) avg | Index: keyword→multiple page numbers |

---

## 🔧 Function Table

| Function | map | unordered_map | multimap | unordered_multimap | Purpose | Example |
|----------|-----|---------------|----------|-------------------|---------|---------|
| `insert()` | ✅ | ✅ | ✅ | ✅ | Add pair | `m.insert({1,"a"});` |
| `emplace()` | ✅ | ✅ | ✅ | ✅ | Construct in-place | `m.emplace(1,"a");` |
| `operator[]` | ✅ | ✅ | ❌ | ❌ | Access/insert | `m[1]="a";` |
| `at()` | ✅ | ✅ | ❌ | ❌ | Bounds-checked access | `auto s=m.at(1);` |
| `find(key)` | ✅ | ✅ | ✅ | ✅ | Find iterator | `auto it=m.find(1);` |
| `count(key)` | ✅ | ✅ | ✅ | ✅ | Count occurrences | `int c=m.count(1);` |
| `equal_range(key)` | ❌ | ❌ | ✅ | ✅ | Range of duplicates | `auto [l,r]=m.equal_range(1);` |
| `lower_bound(key)` | ✅ | ❌ | ✅ | ❌ | First key ≥ | `auto it=m.lower_bound(1);` |
| `upper_bound(key)` | ✅ | ❌ | ✅ | ❌ | First key > | `auto it=m.upper_bound(1);` |
| `erase(key)` | ✅ | ✅ | ✅ | ✅ | Remove by key | `m.erase(1);` |
| `erase(it)` | ✅ | ✅ | ✅ | ✅ | Remove by iterator | `m.erase(m.begin());` |
| `erase(lo, hi)` | ✅ | ✅ | ✅ | ✅ | Remove range | `m.erase(lo, hi);` |
| `size()` | ✅ | ✅ | ✅ | ✅ | Element count | `int n=m.size();` |
| `empty()` | ✅ | ✅ | ✅ | ✅ | Check empty | `if(m.empty())` |
| `clear()` | ✅ | ✅ | ✅ | ✅ | Delete all | `m.clear();` |
| `begin()/end()` | ✅ | ✅ | ✅ | ✅ | Iteration | `for(auto& [k,v]:m)` |
| `reserve()` | ❌ | ✅ | ❌ | ✅ | Pre-allocate buckets | `m.reserve(100000);` |
| `advance(it, n)` | ✅ | ✅ | ✅ | ✅ | Advance iterator (modifies) | `advance(it, 2);` |
| `it->first/second` | ✅ | ✅ | ✅ | ✅ | Access key/value from iterator | `auto k=it->first; auto v=it->second;` |

---