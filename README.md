# Complete STL Operations Guide for Competitive Programming 🚀

## Table of Contents
1. Vectors
2. Sets
3. Maps
4. Stacks
5. Queues
6. Priority Queue
7. Deque
8. Algorithms

---

## 1. Vectors

### 📊 Visual Representation
```
Memory Layout:
Index:    0    1    2    3    4
         ┌────┬────┬────┬────┬────┐
Vector:  │ 10 │ 20 │ 30 │ 40 │ 50 │
         └────┴────┴────┴────┴────┘
Capacity: 8 (actual memory allocated)
Size: 5 (elements present)
```

### 🔧 ALL Vector Operations

#### **1. Construction**
```cpp
// Empty vector
vector<int> v1;

// With size
vector<int> v2(5);           // [0, 0, 0, 0, 0]

// With size and value
vector<int> v3(5, 10);       // [10, 10, 10, 10, 10]

// From another vector
vector<int> v4(v3);          // Copy of v3

// From array
int arr[] = {1, 2, 3};
vector<int> v5(arr, arr + 3); // [1, 2, 3]

// From initializer list
vector<int> v6 = {1, 2, 3, 4}; // [1, 2, 3, 4]

// 2D vector
vector<vector<int>> v7(3, vector<int>(4, 0)); // 3x4 matrix with 0s
```

#### **2. Adding Elements**
```cpp
vector<int> v;

// At end
v.push_back(10);              // [10] - O(1) amortized
v.emplace_back(20);           // [10, 20] - faster, constructs in-place

// At specific position
v.insert(v.begin(), 5);       // [5, 10, 20] - O(n)
v.insert(v.begin() + 1, 7);   // [5, 7, 10, 20] - O(n)

// Multiple elements
v.insert(v.end(), 3, 100);    // [5, 7, 10, 20, 100, 100, 100] - O(n)

// Visual Transcript:
// push_back(10): [] → [10]
// push_back(20): [10] → [10, 20]
// insert(begin, 5): Shift all → [5, 10, 20]
```

#### **3. Removing Elements**
```cpp
vector<int> v = {1, 2, 3, 4, 5};

// From end
v.pop_back();                 // [1, 2, 3, 4] - O(1)

// From specific position
v.erase(v.begin());           // [2, 3, 4] - O(n)
v.erase(v.begin() + 1);       // [2, 4] - O(n)

// Range erase
v = {1, 2, 3, 4, 5};
v.erase(v.begin() + 1, v.begin() + 3); // [1, 4, 5] - removes [2,3]

// Remove all elements
v.clear();                    // [] - O(n)

// Visual:
// erase(begin+1): [1,2,3,4,5]
//                    ↓ remove
//                 [1,3,4,5] (shift left)
```

#### **4. Accessing Elements**
```cpp
vector<int> v = {10, 20, 30, 40, 50};

// By index
cout << v[2];                 // 30 - O(1), no bounds check
cout << v.at(2);              // 30 - O(1), with bounds check

// First and last
cout << v.front();            // 10 - O(1)
cout << v.back();             // 50 - O(1)

// Get pointer to data
int* ptr = v.data();          // Points to first element

// Visual:
// Index:  0   1   2   3   4
//       [10, 20, 30, 40, 50]
//        ↑           ↑       ↑
//     front()      [2]     back()
```

#### **5. Size and Capacity**
```cpp
vector<int> v = {1, 2, 3};

// Size operations
int sz = v.size();            // 3 - O(1)
bool empty = v.empty();       // false - O(1)

// Capacity operations
int cap = v.capacity();       // >=3 (implementation dependent)
v.reserve(100);               // Reserve space for 100 elements - O(n)
v.shrink_to_fit();           // Reduce capacity to size - O(n)

// Resize
v.resize(5);                  // [1, 2, 3, 0, 0] - O(n)
v.resize(7, 10);              // [1, 2, 3, 0, 0, 10, 10] - O(n)
v.resize(2);                  // [1, 2] - O(n)

// Visual Transcript:
// Initial: size=3, capacity=4
//          [1, 2, 3, _]
// 
// reserve(10): size=3, capacity=10
//              [1, 2, 3, _, _, _, _, _, _, _]
// 
// resize(5): size=5, capacity=10
//            [1, 2, 3, 0, 0, _, _, _, _, _]
```

#### **6. Modifying Operations**
```cpp
vector<int> v = {1, 2, 3, 4};

// Assign new content
v.assign(3, 100);             // [100, 100, 100] - replaces all
v.assign({5, 6, 7});          // [5, 6, 7]

// Swap with another vector
vector<int> v2 = {10, 20};
v.swap(v2);                   // v=[10,20], v2=[5,6,7] - O(1)

// Fill with value (C++11)
fill(v.begin(), v.end(), 0);  // [0, 0] - O(n)
```

#### **7. Iterators**
```cpp
vector<int> v = {1, 2, 3, 4, 5};

// Forward iteration
for(auto it = v.begin(); it != v.end(); ++it) {
    cout << *it << " ";       // 1 2 3 4 5
}

// Reverse iteration
for(auto it = v.rbegin(); it != v.rend(); ++it) {
    cout << *it << " ";       // 5 4 3 2 1
}

// Const iterators
for(auto it = v.cbegin(); it != v.cend(); ++it) {
    // *it = 10; // ERROR: can't modify
}

// Range-based loop (C++11)
for(int x : v) {
    cout << x << " ";
}

for(int& x : v) {             // Reference - can modify
    x *= 2;
}

// Visual:
// begin()          end()
//   ↓                ↓
// [1, 2, 3, 4, 5] (end points past last)
//   ↑
// rend()           rbegin()
```

#### **8. Comparison Operations**
```cpp
vector<int> v1 = {1, 2, 3};
vector<int> v2 = {1, 2, 3};
vector<int> v3 = {1, 2, 4};

// Equality
bool eq = (v1 == v2);         // true
bool neq = (v1 != v3);        // true

// Lexicographical comparison
bool less = (v1 < v3);        // true (3 < 4)
bool greater = (v3 > v1);     // true

// Visual Comparison:
// v1: [1, 2, 3]
// v3: [1, 2, 4]
//          ↑
//        3 < 4, so v1 < v3
```

### 🎯 Complete Operations Table

| Operation | Code | Time | Space | Use Case |
|-----------|------|------|-------|----------|
| **Construction** |
| Default | `vector<int> v;` | O(1) | O(1) | Empty vector |
| With size | `vector<int> v(n);` | O(n) | O(n) | Known size |
| With value | `vector<int> v(n, val);` | O(n) | O(n) | Initialize all |
| Copy | `vector<int> v2(v1);` | O(n) | O(n) | Duplicate |
| 2D | `vector<vector<int>> v(n, vector<int>(m));` | O(n*m) | O(n*m) | Matrix |
| **Adding** |
| End | `v.push_back(x)` | O(1)* | - | Most common |
| End (better) | `v.emplace_back(x)` | O(1)* | - | Faster construction |
| Position | `v.insert(it, x)` | O(n) | - | Rare in CP |
| Multiple | `v.insert(it, n, x)` | O(n) | - | Bulk insert |
| **Removing** |
| End | `v.pop_back()` | O(1) | - | Common |
| Position | `v.erase(it)` | O(n) | - | Shift needed |
| Range | `v.erase(it1, it2)` | O(n) | - | Remove multiple |
| All | `v.clear()` | O(n) | - | Reset vector |
| **Access** |
| Index | `v[i]` | O(1) | - | Fast, no check |
| Safe index | `v.at(i)` | O(1) | - | With bounds check |
| First | `v.front()` | O(1) | - | Get first |
| Last | `v.back()` | O(1) | - | Get last |
| Raw pointer | `v.data()` | O(1) | - | C-style array |
| **Size** |
| Get size | `v.size()` | O(1) | - | Element count |
| Check empty | `v.empty()` | O(1) | - | Is empty? |
| Get capacity | `v.capacity()` | O(1) | - | Allocated space |
| Reserve | `v.reserve(n)` | O(n) | - | Pre-allocate |
| Shrink | `v.shrink_to_fit()` | O(n) | - | Free extra space |
| Resize | `v.resize(n)` | O(n) | - | Change size |
| **Modify** |
| Assign | `v.assign(n, val)` | O(n) | - | Replace all |
| Swap | `v.swap(v2)` | O(1) | - | Exchange vectors |
| Fill | `fill(v.begin(), v.end(), val)` | O(n) | - | Set all to value |
| **Iterators** |
| Begin | `v.begin()` | O(1) | - | First element |
| End | `v.end()` | O(1) | - | Past last |
| Reverse begin | `v.rbegin()` | O(1) | - | Last element |
| Reverse end | `v.rend()` | O(1) | - | Before first |

*O(1) amortized

### 💡 Codeforces Example with All Operations
```cpp
// Problem: Array manipulations
void solve() {
    int n, q;
    cin >> n >> q;
    
    // 1. Construction with size
    vector<int> arr(n);
    
    // 2. Input using iterators
    for(auto it = arr.begin(); it != arr.end(); ++it) {
        cin >> *it;
    }
    
    // 3. Reserve space for queries
    vector<int> results;
    results.reserve(q);
    
    while(q--) {
        int type;
        cin >> type;
        
        if(type == 1) {
            // Insert element
            int pos, val;
            cin >> pos >> val;
            arr.insert(arr.begin() + pos, val);
        }
        else if(type == 2) {
            // Remove element
            int pos;
            cin >> pos;
            arr.erase(arr.begin() + pos);
        }
        else if(type == 3) {
            // Get element
            int pos;
            cin >> pos;
            results.push_back(arr.at(pos));
        }
        else if(type == 4) {
            // Reverse range
            int l, r;
            cin >> l >> r;
            reverse(arr.begin() + l, arr.begin() + r + 1);
        }
        else if(type == 5) {
            // Sort range
            int l, r;
            cin >> l >> r;
            sort(arr.begin() + l, arr.begin() + r + 1);
        }
    }
    
    // Output results
    for(int res : results) {
        cout << res << " ";
    }
}
```

---

## 2. Sets

### 📊 Visual: Set Internal Structure (Red-Black Tree)
```
         5(B)
        /    \
      3(R)   8(R)
      /      /  \
    1(B)   7(B) 10(B)

B = Black node
R = Red node

Properties:
1. All elements unique
2. Always sorted
3. Balanced tree (height = O(log n))
```

### 🔧 ALL Set Operations

#### **1. Construction**
```cpp
// Empty set
set<int> s1;

// From initializer list
set<int> s2 = {5, 2, 8, 1, 9};  // Automatically sorted: {1,2,5,8,9}

// From another set
set<int> s3(s2);                 // Copy

// From array
int arr[] = {3, 1, 4, 1, 5};
set<int> s4(arr, arr + 5);       // {1,3,4,5} - duplicates removed

// From vector
vector<int> v = {7, 2, 7, 3};
set<int> s5(v.begin(), v.end()); // {2,3,7}

// Custom comparator (descending order)
set<int, greater<int>> s6 = {1, 5, 3}; // {5,3,1}

// Visual:
// Input: {5, 2, 8, 1, 9}
// Set builds tree:
//       5
//      / \
//     2   8
//    /     \
//   1       9
// Iteration gives: 1, 2, 5, 8, 9
```

#### **2. Insertion Operations**
```cpp
set<int> s;

// Single element
auto result1 = s.insert(10);     // Returns pair<iterator, bool>
// result1.first = iterator to 10
// result1.second = true (inserted successfully)

auto result2 = s.insert(10);     // Duplicate
// result2.second = false (not inserted)

// With position hint (for optimization)
auto it = s.insert(s.begin(), 5); // Faster if hint is good

// Range insertion
vector<int> v = {1, 2, 3};
s.insert(v.begin(), v.end());

// Initializer list
s.insert({20, 30, 40});

// Emplace (construct in place)
s.emplace(50);                   // Slightly faster than insert

// Visual Transcript:
// Step 1: insert(10)
//         Tree: [10]
//         Result: (iterator→10, true)
//
// Step 2: insert(10) again
//         Tree: [10] (unchanged)
//         Result: (iterator→10, false)
//
// Step 3: insert(5)
//         Tree: [5, 10]
//              5
//               \
//               10
```

#### **3. Deletion Operations**
```cpp
set<int> s = {1, 2, 3, 4, 5};

// By value
size_t removed = s.erase(3);     // Returns count (1 if found, 0 if not)
// s = {1, 2, 4, 5}

// By iterator
auto it = s.find(2);
if(it != s.end()) {
    s.erase(it);                 // s = {1, 4, 5}
}

// Range erase
auto it1 = s.find(1);
auto it2 = s.find(5);
s.erase(it1, it2);               // Removes [1,5), s = {5}

// Clear all
s.clear();                       // s = {}

// Visual:
// Before: {1, 2, 3, 4, 5}
//           2
//          / \
//         1   4
//            / \
//           3   5
//
// After erase(3): {1, 2, 4, 5}
//           2
//          / \
//         1   4
//              \
//               5 (rebalanced)
```

#### **4. Search Operations**
```cpp
set<int> s = {1, 3, 5, 7, 9};

// Find exact element
auto it1 = s.find(5);
if(it1 != s.end()) {
    cout << "Found: " << *it1;   // Found: 5
}

// Count (always 0 or 1 for set)
int cnt = s.count(5);            // 1

// Lower bound (first >= value)
auto it2 = s.lower_bound(6);     // Points to 7
auto it3 = s.lower_bound(5);     // Points to 5

// Upper bound (first > value)
auto it4 = s.upper_bound(5);     // Points to 7
auto it5 = s.upper_bound(9);     // Points to s.end()

// Equal range (returns pair of iterators)
auto range = s.equal_range(5);   // [iterator to 5, iterator to 7]

// Visual Search:
// Set: {1, 3, 5, 7, 9}
//       ↑   ↑   ↑
//       |   |   |
// lower_bound(6): finds 7 (first >= 6)
// lower_bound(5): finds 5 (first >= 5)
// upper_bound(5): finds 7 (first > 5)
```

#### **5. Access Operations**
```cpp
set<int> s = {10, 20, 30, 40, 50};

// First element
int first = *s.begin();          // 10

// Last element
int last = *s.rbegin();          // 50
// OR
int last2 = *prev(s.end());      // 50

// Kth element (0-indexed)
auto it = s.begin();
advance(it, 2);                  // Move iterator 2 positions
int third = *it;                 // 30

// Next element
auto it2 = s.find(20);
auto next_it = next(it2);        // Points to 30

// Previous element
auto prev_it = prev(it2);        // Points to 10

// Visual:
// begin()                    end()
//   ↓                          ↓
// [10, 20, 30, 40, 50] nullptr
//   ↑              ↑
// first          last (via rbegin)
//
// advance(it, 2) from begin:
// 10 → 20 → 30
```

#### **6. Size and Capacity**
```cpp
set<int> s = {1, 2, 3};

// Size
size_t sz = s.size();            // 3 - O(1)

// Check if empty
bool empty = s.empty();          // false - O(1)

// Maximum possible size
size_t max_sz = s.max_size();    // Very large number (implementation dependent)
```

#### **7. Iterators**
```cpp
set<int> s = {1, 2, 3, 4, 5};

// Forward iteration
for(auto it = s.begin(); it != s.end(); ++it) {
    cout << *it << " ";          // 1 2 3 4 5
}

// Reverse iteration
for(auto it = s.rbegin(); it != s.rend(); ++it) {
    cout << *it << " ";          // 5 4 3 2 1
}

// Range-based loop
for(int x : s) {
    cout << x << " ";            // 1 2 3 4 5
}

// Const iterators
for(auto it = s.cbegin(); it != s.cend(); ++it) {
    // *it = 10; // ERROR: can't modify
}

// Visual Iterator Movement:
// begin()   →    →    →    →   end()
//   ↓                             ↓
//  [1]   [2]   [3]   [4]   [5]  null
//   ↑                             ↑
// rend()  ←    ←    ←    ←   rbegin()
```

#### **8. Set Operations (Mathematical)**
```cpp
set<int> s1 = {1, 2, 3, 4};
set<int> s2 = {3, 4, 5, 6};

// Union
set<int> result_union;
set_union(s1.begin(), s1.end(), 
          s2.begin(), s2.end(),
          inserter(result_union, result_union.begin()));
// result: {1, 2, 3, 4, 5, 6}

// Intersection
set<int> result_inter;
set_intersection(s1.begin(), s1.end(),
                 s2.begin(), s2.end(),
                 inserter(result_inter, result_inter.begin()));
// result: {3, 4}

// Difference (s1 - s2)
set<int> result_diff;
set_difference(s1.begin(), s1.end(),
               s2.begin(), s2.end(),
               inserter(result_diff, result_diff.begin()));
// result: {1, 2}

// Symmetric difference (elements in either but not both)
set<int> result_sym;
set_symmetric_difference(s1.begin(), s1.end(),
                         s2.begin(), s2.end(),
                         inserter(result_sym, result_sym.begin()));
// result: {1, 2, 5, 6}

// Visual:
// s1: {1, 2, 3, 4}
// s2: {3, 4, 5, 6}
//
// Union:        {1, 2, 3, 4, 5, 6}
// Intersection:       {3, 4}
// Difference:   {1, 2}
// Sym Diff:     {1, 2,       5, 6}
```

#### **9. Comparison Operations**
```cpp
set<int> s1 = {1, 2, 3};
set<int> s2 = {1, 2, 3};
set<int> s3 = {1, 2, 4};

// Equality
bool eq = (s1 == s2);            // true
bool neq = (s1 != s3);           // true

// Lexicographical comparison
bool less = (s1 < s3);           // true (3 < 4)
bool greater = (s3 > s1);        // true
```

#### **10. Swap Operation**
```cpp
set<int> s1 = {1, 2, 3};
set<int> s2 = {10, 20};

s1.swap(s2);
// s1 = {10, 20}
// s2 = {1, 2, 3}
// O(1) - just swaps internal pointers
```

### 🎯 Complete Set Operations Table

| Operation | Code | Time | Use Case |
|-----------|------|------|----------|
| **Construction** |
| Empty | `set<int> s;` | O(1) | Start fresh |
| From list | `set<int> s = {1,2,3};` | O(n log n) | Initialize |
| Copy | `set<int> s2(s1);` | O(n) | Duplicate |
| From range | `set<int> s(v.begin(), v.end());` | O(n log n) | From vector/array |
| Custom compare | `set<int, greater<int>> s;` | O(1) | Descending order |
| **Insertion** |
| Single | `s.insert(x)` | O(log n) | Add element |
| With hint | `s.insert(it, x)` | O(log n)* | Optimized insert |
| Range | `s.insert(v.begin(), v.end())` | O(k log n) | Bulk insert |
| Emplace | `s.emplace(x)` | O(log n) | Construct in-place |
| **Deletion** |
| By value | `s.erase(x)` | O(log n) | Remove element |
| By iterator | `s.erase(it)` | O(log n) | Remove at position |
| Range | `s.erase(it1, it2)` | O(k log n) | Remove multiple |
| Clear all | `s.clear()` | O(n) | Empty set |
| **Search** |
| Find | `s.find(x)` | O(log n) | Exact match |
| Count | `s.count(x)` | O(log n) | Check existence |
| Lower bound | `s.lower_bound(x)` | O(log n) | First >= x |
| Upper bound | `s.upper_bound(x)` | O(log n) | First > x |
| Equal range | `s.equal_range(x)` | O(log n) | Range of x |
| **Access** |
| First | `*s.begin()` | O(1) | Minimum |
| Last | `*s.rbegin()` | O(1) | Maximum |
| Kth element | `*next(s.begin(), k)` | O(k) | Access by position |
| Next | `next(it)` | O(1) | Iterator + 1 |
| Previous | `prev(it)` | O(1) | Iterator - 1 |
| **Size** |
| Get size | `s.size()` | O(1) | Element count |
| Check empty | `s.empty()` | O(1) | Is empty? |
| Max size | `s.max_size()` | O(1) | Theoretical max |
| **Set Ops** |
| Union | `set_union(...)` | O(n log n) | A ∪ B |
| Intersection | `set_intersection(...)` | O(n log n) | A ∩ B |
| Difference | `set_difference(...)` | O(n log n) | A - B |
| Sym difference | `set_symmetric_difference(...)` | O(n log n) | A △ B |
| **Other** |
| Swap | `s1.swap(s2)` | O(1) | Exchange sets |
| Compare | `s1 == s2` | O(n) | Equality check |

*O(1) if hint is correct

### 💡 Multiset (Allows Duplicates)

```cpp
multiset<int> ms;

// All set operations work
ms.insert(5);
ms.insert(5);                    // Allowed!
ms.insert(5);
// ms = {5, 5, 5}

// Count returns actual count
int cnt = ms.count(5);           // 3

// Erase removes ALL occurrences
ms.erase(5);                     // ms = {}

// Erase single occurrence
ms = {5, 5, 5};
auto it = ms.find(5);
ms.erase(it);                    // ms = {5, 5} (removes only one)

// Visual:
// multiset: [5, 5, 5, 7, 7, 9]
//            ↑     ↑
//         find(5) gets first
//         count(5) = 3
//         erase(5) removes all 3
```

### 💡 Unordered_set (Hash Table)

```cpp
unordered_set<int> us = {1, 5, 3, 9};

// Same operations as set
us.insert(7);
us.erase(3);
auto it = us.find(5);

// But:
// - No guaranteed order
// - O(1) average time for insert/erase/find
// - O(n) worst case (hash collisions)

// Iteration order is random
for(int x : us) {
    cout << x << " ";            // Random order: 9 1 5 7
}

// Visual:
// Hash Table:
// Bucket 0: []
// Bucket 1: [1]
// Bucket 2: []
// Bucket 3: [3] → [9] (collision chain)
// Bucket 4: []
// Bucket 5: [5]
```

### 💡 Codeforces Example: All Set Operations

```cpp
// Problem: Range queries on set
void solve() {
    set<int> s;
    int q;
    cin >> q;
    
    while(q--) {
        int type;
        cin >> type;
        
        if(type == 1) {
            // Insert
            int x;
            cin >> x;
            auto [it, inserted] = s.insert(x);
            cout << (inserted ? "Inserted" : "Already exists") << "\n";
        }
        else if(type == 2) {
            // Delete
            int x;
            cin >> x;
            size_t removed = s.erase(x);
            cout << (removed ? "Deleted" : "Not found") << "\n";
        }
        else if(type == 3) {
            // Find
            int x;
            cin >> x;
            bool found = (s.count(x) > 0);
            cout << (found ? "Found" : "Not found") << "\n";
        }
        else if(type == 4) {
            // Get minimum
            if(!s.empty()) {
                cout << *s.begin() << "\n";
            }
        }
        else if(type == 5) {
            // Get maximum
            if(!s.empty()) {
                cout << *s.rbegin() << "\n";
            }
        }
        else if(type == 6) {
            // First >= x
            int x;
            cin >> x;
            auto it = s.lower_bound(x);
            if(it != s.end()) {
                cout << *it << "\n";
            } else {
                cout << "None\n";
            }
        }
        else if(type == 7) {
            // First > x
            int x;
            cin >> x;
            auto it = s.upper_bound(x);
            if(it != s.end()) {
                cout << *it << "\n";
            } else {
                cout << "None\n";
            }
        }
        else if(type == 8) {
            // Print all in order
            for(int x : s) {
                cout << x << " ";
            }
            cout << "\n";
        }
        else if(type == 9) {
            // Print all in reverse
            for(auto it = s.rbegin(); it != s.rend(); ++it) {
                cout << *it << " ";
            }
            cout << "\n";
        }
    }
}
```

---

## 3. Maps

### 📊 Visual: Map Internal Structure
```
map<string, int> ages;

Key-Value Pairs (sorted by key):
       ("Bob", 25)
       /          \
  ("Alice", 30)   ("Charlie", 20)

Stored as Red-Black Tree:
Keys sorted: "Alice" < "Bob" < "Charlie"
```

### 🔧 ALL Map Operations

#### **1. Construction**
```cpp
// Empty map
map<int, string> m1;

// From initializer list
map<int, string> m2 = {
    {1, "one"},
    {2, "two"},
    {3, "three"}
};

// Copy constructor
map<int, string> m3(m2);

// Custom comparator (descending keys)
map<int, string, greater<int>> m4 = {
    {1, "one"},
    {2, "two"}
}; // Keys: 2, 1 (descending)

// Visual:
// m2 internal structure:
//        2:"two"
//       /       \
//   1:"one"   3:"three"
```

#### **2. Insertion Operations**
```cpp
map<int, string> m;

// Method 1: Using []
m[1] = "one";                    // Creates if not exists
m[1] = "ONE";                    // Updates if exists

// Method 2: Using insert
auto result1 = m.insert({2, "two"});
// result1 = pair<iterator, bool>
// result1.first = iterator to element
// result1.second = true if inserted

auto result2 = m.insert({2, "TWO"});
// result2.second = false (key exists, not inserted)

// Method 3: Using insert with pair
m.insert(make_pair(3, "three"));
m.insert(pair<int, string>(4, "four"));

// Method 4: Emplace (construct in-place)
m.emplace(5, "five");            // Slightly faster

// Method 5: Try_emplace (C++17)
m.try_emplace(6, "six");         // Only inserts if key doesn't exist
m.try_emplace(1, "wrong");       // Doesn't overwrite existing

// Range insertion
map<int, string> m2 = {{7, "seven"}, {8, "eight"}};
m.insert(m2.begin(), m2.end());

// Visual Transcript:
// m[1] = "one":
//   Empty → {1: "one"}
//
// insert({2, "two"}):
//        1:"one"
//            \
//           2:"two"
//
// insert({2, "TWO"}):
//   Already exists, returns false
//   Map unchanged
```

#### **3. Deletion Operations**
```cpp
map<int, string> m = {
    {1, "one"},
    {2, "two"},
    {3, "three"},
    {4, "four"}
};

// By key
size_t removed = m.erase(2);     // Returns 1 if found, 0 if not
// m = {{1,"one"}, {3,"three"}, {4,"four"}}

// By iterator
auto it = m.find(3);
if(it != m.end()) {
    m.erase(it);
}
// m = {{1,"one"}, {4,"four"}}

// Range erase
auto it1 = m.find(1);
auto it2 = m.find(4);
m.erase(it1, it2);               // Removes [1, 4), so only 1
// m = {{4,"four"}}

// Clear all
m.clear();                       // m = {}

// Visual:
// Before: {1:"one", 2:"two", 3:"three", 4:"four"}
//              2:"two"
//             /       \
//         1:"one"   3:"three"
//                       \
//                      4:"four"
//
// After erase(2): Tree rebalanced
//           3:"three"
//          /         \
//      1:"one"    4:"four"
```

#### **4. Access Operations**
```cpp
map<int, string> m = {
    {1, "one"},
    {2, "two"},
    {3, "three"}
};

// Using [] (creates if not exists!)
string s1 = m[1];                // "one"
string s2 = m[10];               // Creates {10, ""} and returns ""

// Using at() (throws exception if not exists)
string s3 = m.at(2);             // "two"
// string s4 = m.at(10);         // Throws std::out_of_range

// Check before access
if(m.count(3)) {
    cout << m[3];                // Safe
}

// Or use find
auto it = m.find(3);
if(it != m.end()) {
    cout << it->second;          // "three"
}

// Visual:
// m[10] when 10 doesn't exist:
// Before: {1, 2, 3}
// After:  {1, 2, 3, 10:""} ← Automatically created!
//
// m.at(10) throws exception:
// ❌ std::out_of_range
```

#### **5. Search Operations**
```cpp
map<int, string> m = {
    {10, "ten"},
    {20, "twenty"},
    {30, "thirty"},
    {40, "forty"}
};

// Find exact key
auto it1 = m.find(20);
if(it1 != m.end()) {
    cout << it1->first << ": " << it1->second; // 20: twenty
}

// Count (0 or 1 for map)
int cnt = m.count(30);           // 1

// Contains (C++20)
bool exists = m.contains(40);    // true

// Lower bound (first >= key)
auto it2 = m.lower_bound(25);    // Points to {30, "thirty"}
auto it3 = m.lower_bound(20);    // Points to {20, "twenty"}

// Upper bound (first > key)
auto it4 = m.upper_bound(20);    // Points to {30, "thirty"}

// Equal range
auto [it_lower, it_upper] = m.equal_range(20);
// it_lower → {20, "twenty"}
// it_upper → {30, "thirty"}

// Visual Search:
// Map: {10, 20, 30, 40}
//       ↑   ↑   ↑   ↑
//
// lower_bound(25): finds 30 (first >= 25)
// lower_bound(20): finds 20 (first >= 20)
// upper_bound(20): finds 30 (first > 20)
```

#### **6. Iterators and Traversal**
```cpp
map<int, string> m = {
    {1, "one"},
    {2, "two"},
    {3, "three"}
};

// Forward iteration (sorted by key)
for(auto it = m.begin(); it != m.end(); ++it) {
    cout << it->first << ": " << it->second << "\n";
    // 1: one
    // 2: two
    // 3: three
}

// Reverse iteration
for(auto it = m.rbegin(); it != m.rend(); ++it) {
    cout << it->first << ": " << it->second << "\n";
    // 3: three
    // 2: two
    // 1: one
}

// Range-based loop (C++11)
for(auto& p : m) {
    cout << p.first << ": " << p.second << "\n";
}

// Structured binding (C++17)
for(auto& [key, value] : m) {
    cout << key << ": " << value << "\n";
}

// Modify values during iteration
for(auto& [key, value] : m) {
    value = "modified";          // OK
    // key = 10;                 // ERROR: keys are const
}

// Visual:
// begin()            end()
//   ↓                  ↓
// [1:one → 2:two → 3:three] → null
//   ↑                  ↑
// rend()            rbegin()
```

#### **7. Size and Capacity**
```cpp
map<int, string> m = {
    {1, "one"},
    {2, "two"}
};

// Size
size_t sz = m.size();            // 2 - O(1)

// Check if empty
bool empty = m.empty();          // false - O(1)

// Maximum possible size
size_t max_sz = m.max_size();    // Very large number
```

#### **8. Swap Operation**
```cpp
map<int, string> m1 = {{1, "one"}, {2, "two"}};
map<int, string> m2 = {{10, "ten"}};

m1.swap(m2);
// m1 = {{10, "ten"}}
// m2 = {{1, "one"}, {2, "two"}}
// O(1) - just swaps internal pointers
```

#### **9. Comparison Operations**
```cpp
map<int, string> m1 = {{1, "a"}, {2, "b"}};
map<int, string> m2 = {{1, "a"}, {2, "b"}};
map<int, string> m3 = {{1, "a"}, {2, "c"}};

// Equality
bool eq = (m1 == m2);            // true
bool neq = (m1 != m3);           // true

// Lexicographical comparison
bool less = (m1 < m3);           // true ("b" < "c")
```

### 🎯 Complete Map Operations Table

| Operation | Code | Time | Use Case |
|-----------|------|------|----------|
| **Construction** |
| Empty | `map<K,V> m;` | O(1) | Start fresh |
| From list | `map<K,V> m = {{k1,v1}, {k2,v2}};` | O(n log n) | Initialize |
| Copy | `map<K,V> m2(m1);` | O(n) | Duplicate |
| Custom compare | `map<K,V,greater<K>> m;` | O(1) | Reverse order |
| **Insertion** |
| Bracket | `m[key] = value` | O(log n) | Add/update |
| Insert | `m.insert({key, value})` | O(log n) | Add only |
| Emplace | `m.emplace(key, value)` | O(log n) | Construct in-place |
| Try emplace | `m.try_emplace(key, value)` | O(log n) | Insert if new |
| Range | `m.insert(m2.begin(), m2.end())` | O(k log n) | Bulk insert |
| **Deletion** |
| By key | `m.erase(key)` | O(log n) | Remove pair |
| By iterator | `m.erase(it)` | O(log n) | Remove at position |
| Range | `m.erase(it1, it2)` | O(k log n) | Remove multiple |
| Clear all | `m.clear()` | O(n) | Empty map |
| **Access** |
| Bracket | `m[key]` | O(log n) | Get/create value |
| At | `m.at(key)` | O(log n) | Get (throws) |
| **Search** |
| Find | `m.find(key)` | O(log n) | Get iterator |
| Count | `m.count(key)` | O(log n) | Check existence |
| Contains | `m.contains(key)` | O(log n) | C++20 check |
| Lower bound | `m.lower_bound(key)` | O(log n) | First >= key |
| Upper bound | `m.upper_bound(key)` | O(log n) | First > key |
| Equal range | `m.equal_range(key)` | O(log n) | Range of key |
| **Iteration** |
| Forward | `for(auto it = m.begin(); ...)` | O(n) | Ascending order |
| Reverse | `for(auto it = m.rbegin(); ...)` | O(n) | Descending |
| Range-for | `for(auto& [k,v] : m)` | O(n) | Modern C++ |
| **Size** |
| Get size | `m.size()` | O(1) | Pair count |
| Check empty | `m.empty()` | O(1) | Is empty? |
| Max size | `m.max_size()` | O(1) | Theoretical max |
| **Other** |
| Swap | `m1.swap(m2)` | O(1) | Exchange maps |
| Compare | `m1 == m2` | O(n) | Equality check |

### 💡 Multimap (Allows Duplicate Keys)

```cpp
multimap<int, string> mm;

// Same key, different values
mm.insert({1, "one"});
mm.insert({1, "uno"});
mm.insert({1, "एक"});

// Count returns number of elements with key
int cnt = mm.count(1);           // 3

// Find returns iterator to first occurrence
auto it = mm.find(1);

// Get all values for a key
auto range = mm.equal_range(1);
for(auto it = range.first; it != range.second; ++it) {
    cout << it->second << " ";   // one uno एक
}

// Visual:
// multimap structure:
//      1:"one"
//      /     \
//   1:"uno"  1:"एक"
//
// All have key 1, stored together
```

### 💡 Unordered_map (Hash Table)

```cpp
unordered_map<string, int> um;

// Same operations as map
um["apple"] = 5;
um["banana"] = 3;
um.erase("apple");

// But:
// - No guaranteed order
// - O(1) average time
// - O(n) worst case
// - Cannot use lower_bound/upper_bound

// Iteration order is random
for(auto& [key, value] : um) {
    cout << key << ": " << value << "\n";
}

// Custom hash function for custom types
struct CustomHash {
    size_t operator()(const pair<int,int>& p) const {
        return hash<int>()(p.first) ^ hash<int>()(p.second);
    }
};

unordered_map<pair<int,int>, string, CustomHash> custom_um;

// Visual Hash Table:
// Bucket 0: []
// Bucket 1: ["apple":5]
// Bucket 2: ["banana":3]
// Bucket 3: []
// ...
```

### 💡 Codeforces Example: All Map Operations

```cpp
// Problem: String frequency and operations
void solve() {
    map<string, int> freq;
    int q;
    cin >> q;
    
    while(q--) {
        int type;
        cin >> type;
        
        if(type == 1) {
            // Add/Update
            string word;
            int count;
            cin >> word >> count;
            freq[word] += count;     // Auto-creates if not exists
        }
        else if(type == 2) {
            // Remove word
            string word;
            cin >> word;
            freq.erase(word);
        }
        else if(type == 3) {
            // Get frequency
            string word;
            cin >> word;
            cout << freq[word] << "\n"; // Returns 0 if not exists
        }
        else if(type == 4) {
            // Check if exists
            string word;
            cin >> word;
            cout << (freq.count(word) ? "YES" : "NO") << "\n";
        }
        else if(type == 5) {
            // Print all words in alphabetical order
            for(auto& [word, count] : freq) {
                cout << word << ": " << count << "\n";
            }
        }
        else if(type == 6) {
            // Find first word >= given word
            string word;
            cin >> word;
            auto it = freq.lower_bound(word);
            if(it != freq.end()) {
                cout << it->first << "\n";
            } else {
                cout << "None\n";
            }
        }
        else if(type == 7) {
            // Total unique words
            cout << freq.size() << "\n";
        }
        else if(type == 8) {
            // Word with max frequency
            int max_freq = 0;
            string max_word;
            for(auto& [word, count] : freq) {
                if(count > max_freq) {
                    max_freq = count;
                    max_word = word;
                }
            }
            cout << max_word << ": " << max_freq << "\n";
        }
        else if(type == 9) {
            // Increment all frequencies by 1
            for(auto& [word, count] : freq) {
                count++;
            }
        }
        else if(type == 10) {
            // Remove all with frequency < threshold
            int threshold;
            cin >> threshold;
            for(auto it = freq.begin(); it != freq.end(); ) {
                if(it->second < threshold) {
                    it = freq.erase(it); // erase returns next iterator
                } else {
                    ++it;
                }
            }
        }
    }
}
```

---

*Continuing with remaining containers...*

Would you like me to continue with **Stacks, Queues, Priority Queues, Deque, and Algorithms** with the same level of detail?
