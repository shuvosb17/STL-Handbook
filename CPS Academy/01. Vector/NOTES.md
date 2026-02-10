# 📘 Ultimate STL Vector Notes — Part 1

> **Course**: C++ Standard Template Library (STL)
> **Topic**: Almost Everything About STL Vectors
> **Level**: Beginner-Friendly with In-Depth Visualizations

---

## 📌 Table of Contents

1. What is STL?
2. Why Do We Need Vectors?
3. Arrays vs Vectors — The Core Problem
4. What is a Vector?
5. Declaring a Vector
6. Push Back — Adding Elements
7. Accessing Elements
8. Size Function
9. Iterating Through a Vector
10. Taking Input from User
11. Initializing Vectors
12. Vector Internal Memory (Capacity & Resizing)

---

## 1. What is STL?

**STL** stands for **Standard Template Library**. It is a collection of **ready-made, pre-built** data structures and algorithms in C++ that you can directly use — like copy-pasting powerful tools into your code.

> 💡 Think of STL as a **toolbox** that C++ gives you for free. Instead of building a hammer from scratch, you just pick one up and use it.

### What does STL include?

| Component | Examples |
|-----------|---------|
| **Containers** (Data Structures) | `vector`, `list`, `map`, `set`, `stack`, `queue` |
| **Algorithms** | `sort()`, `find()`, `reverse()`, `max()`, `min()` |
| **Iterators** | Pointers that help traverse containers |

### How to use STL?

````cpp
#include <bits/stdc++.h>  // Includes ALL STL headers at once
using namespace std;
````

> This single header `<bits/stdc++.h>` is a shortcut in competitive programming that includes everything — vectors, maps, algorithms, etc.

---

## 2. Why Do We Need Vectors?

Before understanding vectors, let's first understand the **problem with regular arrays**.

### The Problem with Static Arrays

````cpp
int arr[5] = {1, 2, 3, 4, 5};
````

When you declare `arr[5]`:
- You get **exactly 5 slots** — no more, no less.
- The size is **fixed at compile time**.
- You **cannot add** a 6th element later.
- You **cannot shrink** it if you only need 3 elements.

### Visualization: Static Array

````
Memory Layout (Fixed Size = 5):
┌──────┬──────┬──────┬──────┬──────┐
│  1   │  2   │  3   │  4   │  5   │
├──────┼──────┼──────┼──────┼──────┤
│ [0]  │ [1]  │ [2]  │ [3]  │ [4]  │
└──────┴──────┴──────┴──────┴──────┘

❌ Want to add 6? IMPOSSIBLE! No room.
❌ Only using 2 slots? TOO BAD! Memory still allocated for 5.
````

### Real-World Analogy

> Imagine you book a table at a restaurant for **exactly 5 people**. If a 6th friend shows up — there's no chair. If only 2 friends come — you're wasting 3 chairs. That's a static array.
>
> A **vector** is like a **magic table** that automatically grows when more friends arrive and shrinks when they leave! 🪄

---

## 3. Arrays vs Vectors — The Core Problem

| Feature | Static Array | Dynamic Array (Vector) |
|---------|-------------|----------------------|
| Size | Fixed at declaration | Grows/shrinks dynamically |
| Declaration | `int arr[5];` | `vector<int> v;` |
| Adding elements | Not possible beyond size | `push_back()` adds at end |
| Memory | Can waste memory | Efficient memory management |
| Safety | No bounds checking | `.at()` provides bounds checking |
| Passing to functions | Need to pass size separately | Carries its own size `.size()` |

---

## 4. What is a Vector?

A **vector** is a **dynamic array** provided by the C++ STL. It can:
- ✅ **Grow** in size when you add elements
- ✅ **Shrink** when you remove elements
- ✅ Access elements by **index** (just like arrays)
- ✅ Automatically **manage memory** for you

### Visualization: Vector as a Dynamic Container

````
Initially: Empty vector
┌─────────────────────────────┐
│         (empty)             │
│     size = 0                │
└─────────────────────────────┘
          ↓
    push_back(10)
          ↓
┌──────┐
│  10  │
├──────┤
│ [0]  │    size = 1
└──────┘
          ↓
    push_back(20)
          ↓
┌──────┬──────┐
│  10  │  20  │
├──────┼──────┤
│ [0]  │ [1]  │    size = 2
└──────┴──────┘
          ↓
    push_back(30)
          ↓
┌──────┬──────┬──────┐
│  10  │  20  │  30  │
├──────┼──────┼──────┤
│ [0]  │ [1]  │ [2]  │    size = 3
└──────┴──────┴──────┘
````

---

## 5. Declaring a Vector

### Syntax

````cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    // Method 1: Empty vector
    vector<int> v;
    
    // Method 2: Vector with initial size (all elements = 0)
    vector<int> v2(5);       // [0, 0, 0, 0, 0]
    
    // Method 3: Vector with size AND default value
    vector<int> v3(5, 10);   // [10, 10, 10, 10, 10]
    
    // Method 4: Initialize with values directly
    vector<int> v4 = {1, 2, 3, 4, 5};
    
    return 0;
}
````

### Visualization of Each Declaration

````
Method 1: vector<int> v;
┌───────────────┐
│   (empty)     │   size = 0
└───────────────┘

Method 2: vector<int> v2(5);
┌─────┬─────┬─────┬─────┬─────┐
│  0  │  0  │  0  │  0  │  0  │   size = 5
├─────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │
└─────┴─────┴─────┴─────┴─────┘

Method 3: vector<int> v3(5, 10);
┌──────┬──────┬──────┬──────┬──────┐
│  10  │  10  │  10  │  10  │  10  │   size = 5
├──────┼──────┼──────┼──────┼──────┤
│ [0]  │ [1]  │ [2]  │ [3]  │ [4]  │
└──────┴──────┴──────┴──────┴──────┘

Method 4: vector<int> v4 = {1, 2, 3, 4, 5};
┌─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │  5  │   size = 5
├─────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │
└─────┴─────┴─────┴─────┴─────┘
````

---

## 6. Push Back — Adding Elements

`push_back()` adds an element **at the end** of the vector. The vector automatically grows to accommodate the new element.

### Code Example

````cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v;          // Empty vector
    
    v.push_back(10);        // v = [10]
    v.push_back(20);        // v = [10, 20]
    v.push_back(30);        // v = [10, 20, 30]
    
    // Print all elements
    for (int i = 0; i < v.size(); i++) {
        cout << v[i] << " ";
    }
    // Output: 10 20 30
    
    return 0;
}
````

### Step-by-Step Visualization

````
Step 0: vector<int> v;
┌─────────────┐
│  (empty)    │   size = 0
└─────────────┘

Step 1: v.push_back(10);
                    ← 10 enters from the back
┌──────┐
│  10  │              size = 1
├──────┤
│ [0]  │
└──────┘

Step 2: v.push_back(20);
                    ← 20 enters from the back
┌──────┬──────┐
│  10  │  20  │      size = 2
├──────┼──────┤
│ [0]  │ [1]  │
└──────┴──────┘

Step 3: v.push_back(30);
                    ← 30 enters from the back
┌──────┬──────┬──────┐
│  10  │  20  │  30  │    size = 3
├──────┼──────┼──────┤
│ [0]  │ [1]  │ [2]  │
└──────┴──────┴──────┘

🎯 Key Insight: Elements always get added at the END (back)
````

---

## 7. Accessing Elements

You can access vector elements just like array elements using the **index operator `[]`** or the **`.at()` function**.

### Code Example

````cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30, 40, 50};
    
    // Method 1: Using [] operator
    cout << v[0] << endl;    // 10
    cout << v[2] << endl;    // 30
    cout << v[4] << endl;    // 50
    
    // Method 2: Using .at()
    cout << v.at(1) << endl; // 20
    cout << v.at(3) << endl; // 40
    
    return 0;
}
````

### Visualization: How Indexing Works

````
Vector v = {10, 20, 30, 40, 50}

Index:    [0]    [1]    [2]    [3]    [4]
        ┌──────┬──────┬──────┬──────┬──────┐
Value:  │  10  │  20  │  30  │  40  │  50  │
        └──────┴──────┴──────┴──────┴──────┘

v[0]  → 10  ✅ (first element)
v[2]  → 30  ✅ (third element)
v[4]  → 50  ✅ (last element)

⚠️ v[5] → UNDEFINED BEHAVIOR! (Out of bounds)
   v.at(5) → Throws an exception (safer!)
````

### `[]` vs `.at()` — Which to use?

| Feature | `v[i]` | `v.at(i)` |
|---------|--------|-----------|
| Speed | Slightly faster | Slightly slower |
| Bounds checking | ❌ No | ✅ Yes |
| On invalid index | Undefined behavior (crash/garbage) | Throws `out_of_range` exception |
| Use when | You're sure index is valid | You want safety |

---

## 8. Size Function

The `.size()` function returns the **total number of elements** currently in the vector.

### Code Example

````cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v;
    
    cout << v.size() << endl;     // 0 (empty)
    
    v.push_back(10);
    v.push_back(20);
    v.push_back(30);
    
    cout << v.size() << endl;     // 3
    
    v.push_back(40);
    v.push_back(50);
    v.push_back(60);
    
    cout << v.size() << endl;     // 6
    
    return 0;
}
````

### Visualization

````
After declaration:       v.size() = 0
┌─────────┐
│ (empty) │
└─────────┘

After 3 push_backs:     v.size() = 3
┌──────┬──────┬──────┐
│  10  │  20  │  30  │
└──────┴──────┴──────┘

After 6 push_backs:     v.size() = 6
┌──────┬──────┬──────┬──────┬──────┬──────┐
│  10  │  20  │  30  │  40  │  50  │  60  │
└──────┴──────┴──────┴──────┴──────┴──────┘

💡 .size() always tells you the CURRENT number of elements
   (not the capacity — more on that later!)
````

---

## 9. Iterating Through a Vector

There are multiple ways to loop through all elements of a vector.

### Method 1: Index-Based For Loop (Most Common)

````cpp
vector<int> v = {2, 3, 5, 6};

for (int i = 0; i < v.size(); i++) {
    cout << v[i] << " ";
}
// Output: 2 3 5 6
````

### Visualization of the Loop

````
v = {2, 3, 5, 6}      v.size() = 4

Iteration 1: i = 0    i < 4? ✅    print v[0] → 2
Iteration 2: i = 1    i < 4? ✅    print v[1] → 3
Iteration 3: i = 2    i < 4? ✅    print v[2] → 5
Iteration 4: i = 3    i < 4? ✅    print v[3] → 6
Iteration 5: i = 4    i < 4? ❌    STOP

Output: 2 3 5 6
````

### Method 2: Range-Based For Loop (Modern C++)

````cpp
vector<int> v = {2, 3, 5, 6};

for (int x : v) {
    cout << x << " ";
}
// Output: 2 3 5 6
````

> 💡 Read this as: **"For each element x IN v, print x"**. It's cleaner and less error-prone.

### Method 3: Using Iterators

````cpp
vector<int> v = {2, 3, 5, 6};

for (auto it = v.begin(); it != v.end(); it++) {
    cout << *it << " ";
}
// Output: 2 3 5 6
````

### Visualization: How Iterators Work

````
v = {2, 3, 5, 6}

       v.begin()                            v.end()
          ↓                                    ↓
        ┌──────┬──────┬──────┬──────┐     ┌────────┐
        │  2   │  3   │  5   │  6   │     │ (past  │
        │      │      │      │      │     │  end)  │
        └──────┴──────┴──────┴──────┘     └────────┘
          it→     it→    it→    it→     it == v.end() → STOP!

*it dereferences the iterator to get the VALUE at that position
````

---

## 10. Taking Input from User

### Pattern 1: Known Size — Input N elements

````cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;                    // User tells us how many elements
    
    vector<int> v;
    
    for (int i = 0; i < n; i++) {
        int x;
        cin >> x;
        v.push_back(x);         // Add each element to the vector
    }
    
    // Print all elements
    for (int i = 0; i < v.size(); i++) {
        cout << v[i] << " ";
    }
    
    return 0;
}
````

### Alternative: Pre-sized vector with direct input

````cpp
int n;
cin >> n;

vector<int> v(n);               // Create vector of size n (all zeros)

for (int i = 0; i < n; i++) {
    cin >> v[i];                 // Input directly into position
}
````

### Visualization: Input Flow

````
User types: 5
             2 3 4 5 6

Step 1: n = 5
Step 2: vector<int> v;   →  (empty)

Step 3: Loop reads elements one by one:
  cin >> 2  →  push_back(2)  →  v = [2]
  cin >> 3  →  push_back(3)  →  v = [2, 3]
  cin >> 4  →  push_back(4)  →  v = [2, 3, 4]
  cin >> 5  →  push_back(5)  →  v = [2, 3, 4, 5]
  cin >> 6  →  push_back(6)  →  v = [2, 3, 4, 5, 6]

Final:
┌─────┬─────┬─────┬─────┬─────┐
│  2  │  3  │  4  │  5  │  6  │   size = 5
├─────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │
└─────┴─────┴─────┴─────┴─────┘
````

---

## 11. Initializing Vectors

Here's a summary of **all the ways** to create and initialize vectors:

````cpp
// 1. Empty vector
vector<int> v1;

// 2. With specific size (default value = 0 for int)
vector<int> v2(5);              // [0, 0, 0, 0, 0]

// 3. With size and custom default value
vector<int> v3(5, 7);           // [7, 7, 7, 7, 7]

// 4. Using initializer list
vector<int> v4 = {1, 2, 3, 4, 5};

// 5. Copy from another vector
vector<int> v5(v4);             // [1, 2, 3, 4, 5]  (copy of v4)

// 6. From array
int arr[] = {10, 20, 30};
vector<int> v6(arr, arr + 3);   // [10, 20, 30]
````

### Visualization: All Initialization Methods

````
v1 (empty):           []                    size = 0

v2 (size 5):          [0, 0, 0, 0, 0]      size = 5

v3 (size 5, val 7):   [7, 7, 7, 7, 7]      size = 5

v4 (init list):       [1, 2, 3, 4, 5]      size = 5

v5 (copy of v4):      [1, 2, 3, 4, 5]      size = 5
                       ↑ separate copy in memory

v6 (from array):      [10, 20, 30]          size = 3
````

---

## 12. Vector Internal Memory (Capacity & Resizing)

This is one of the **most important** concepts for understanding how vectors truly work under the hood.

### The Problem: How Does a Vector Grow?

When you `push_back()`, the vector needs more memory. But memory is allocated in **contiguous blocks** (one after another). So what happens when there's no room next to the existing elements?

### The Answer: **Doubling Strategy**

When a vector runs out of space, it:
1. **Allocates a NEW block** of memory (usually **2x** the current capacity)
2. **Copies** all existing elements to the new block
3. **Frees** the old memory
4. **Adds** the new element

### Visualization: Capacity vs Size

````
Size     = Number of elements actually stored
Capacity = Total memory slots available

Example: push_back sequence

═══════════════════════════════════════════════════════════
push_back(1):
  Size = 1, Capacity = 1
  ┌─────┐
  │  1  │
  └─────┘
  
═══════════════════════════════════════════════════════════
push_back(2):  ← No room! Capacity doubles: 1 → 2
  Size = 2, Capacity = 2
  ┌─────┬─────┐
  │  1  │  2  │
  └─────┴─────┘
  
═══════════════════════════════════════════════════════════
push_back(3):  ← No room! Capacity doubles: 2 → 4
  Size = 3, Capacity = 4
  ┌─────┬─────┬─────┬─────┐
  │  1  │  2  │  3  │     │  ← 1 empty slot reserved
  └─────┴─────┴─────┴─────┘
  
═══════════════════════════════════════════════════════════
push_back(4):  ← Room exists! No reallocation needed
  Size = 4, Capacity = 4
  ┌─────┬─────┬─────┬─────┐
  │  1  │  2  │  3  │  4  │
  └─────┴─────┴─────┴─────┘
  
═══════════════════════════════════════════════════════════
push_back(5):  ← No room! Capacity doubles: 4 → 8
  Size = 5, Capacity = 8
  ┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
  │  1  │  2  │  3  │  4  │  5  │     │     │     │
  └─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
                                    ↑ 3 empty slots reserved
````

### Code to Observe Capacity

````cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v;
    
    for (int i = 1; i <= 10; i++) {
        v.push_back(i);
        cout << "Size: " << v.size() 
             << "  Capacity: " << v.capacity() << endl;
    }
    
    return 0;
}
````

### Output

````
Size: 1   Capacity: 1
Size: 2   Capacity: 2
Size: 3   Capacity: 4    ← doubled!
Size: 4   Capacity: 4
Size: 5   Capacity: 8    ← doubled!
Size: 6   Capacity: 8
Size: 7   Capacity: 8
Size: 8   Capacity: 8
Size: 9   Capacity: 16   ← doubled!
Size: 10  Capacity: 16
````

### Why Doubling?

| Strategy | Number of reallocations for N elements | Time Complexity |
|----------|---------------------------------------|-----------------|
| Grow by 1 each time | N reallocations | O(N²) total |
| **Double each time** | **log₂(N) reallocations** | **O(N) amortized** |

> 💡 **Amortized O(1)**: Even though individual `push_back` calls *occasionally* take O(N) time (when reallocation happens), on average across many calls, each `push_back` is effectively **O(1)** — constant time!

### Memory Visualization: The Copy Process

````
Before push_back(3) — capacity is full:

Old Memory Block (capacity = 2):
┌─────┬─────┐
│  1  │  2  │  ← FULL! No room for 3
└─────┴─────┘

Step 1: Allocate NEW block (capacity = 4):
┌─────┬─────┬─────┬─────┐
│     │     │     │     │  ← Empty new block
└─────┴─────┴─────┴─────┘

Step 2: COPY old elements to new block:
┌─────┬─────┐         ┌─────┬─────┬─────┬─────┐
│  1  │  2  │ ══════> │  1  │  2  │     │     │
└─────┴─────┘  copy   └─────┴─────┴─────┴─────┘

Step 3: Add new element:
                       ┌─────┬─────┬─────┬─────┐
                       │  1  │  2  │  3  │     │
                       └─────┴─────┴─────┴─────┘

Step 4: FREE old memory block:
┌─────┬─────┐
│ 💀  │ 💀  │ ← Deleted / freed
└─────┴─────┘

Final result:
┌─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │     │   size=3, capacity=4
└─────┴─────┴─────┴─────┘
````

---

## 🧠 Quick Reference Cheat Sheet

````cpp
// ═══════════════════════════════════════════
//         VECTOR CHEAT SHEET (Part 1)
// ═══════════════════════════════════════════

#include <bits/stdc++.h>
using namespace std;

int main() {
    // --- DECLARATION ---
    vector<int> v;                    // empty
    vector<int> v2(5);                // [0,0,0,0,0]
    vector<int> v3(5, 10);            // [10,10,10,10,10]
    vector<int> v4 = {1, 2, 3, 4};    // [1,2,3,4]

    // --- ADDING ELEMENTS ---
    v.push_back(100);                 // adds 100 at end

    // --- ACCESSING ---
    cout << v[0];                     // first element
    cout << v.at(0);                  // safer access

    // --- SIZE ---
    cout << v.size();                 // number of elements
    cout << v.capacity();             // allocated slots

    // --- LOOPING ---
    for (int i = 0; i < v.size(); i++)     // index loop
        cout << v[i];
    
    for (int x : v)                        // range-based
        cout << x;
    
    for (auto it = v.begin(); it != v.end(); it++)  // iterator
        cout << *it;

    // --- INPUT ---
    int n; cin >> n;
    vector<int> inp(n);
    for (int i = 0; i < n; i++) cin >> inp[i];

    return 0;
}
````

---

## 🎯 Key Takeaways from Part 1

| Concept | Key Point |
|---------|-----------|
| **STL** | Pre-built library of data structures & algorithms in C++ |
| **Vector** | Dynamic array that grows/shrinks automatically |
| **push_back()** | Adds element at the END of vector |
| **v[i] / v.at(i)** | Access element at index i (`.at()` is safer) |
| **v.size()** | Returns current number of elements |
| **Capacity** | Internal allocated memory (≥ size), doubles when full |
| **Amortized O(1)** | push_back is effectively constant time on average |
| **Contiguous memory** | Vector elements sit next to each other in memory |

---






# 📘 Ultimate STL Vector Notes — Part 2

> **Course**: C++ Standard Template Library (STL)
> **Topic**: Vector Operations Deep Dive — Functions, Sorting, Reversing, Iterators & More
> **Level**: Beginner-Friendly with In-Depth Visualizations

---

## 📌 Table of Contents (Part 2)

13. Pop Back — Removing Last Element
14. Front and Back — Accessing First & Last Elements
15. Insert — Adding Elements at Any Position
16. Erase / Delete — Removing Elements at Any Position
17. Clear — Removing All Elements
18. Sorting a Vector
19. Reverse a Vector
20. Iterators — begin() and end() Deep Dive
21. Passing Vectors to Functions
22. 2D Vectors (Vector of Vectors)
23. Practice Problems & Tips
24. Complete Cheat Sheet

---

## 13. Pop Back — Removing Last Element

`pop_back()` removes the **last element** from the vector. The vector shrinks by 1.

### Code Example

````cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30, 40, 50};
    
    cout << "Before pop_back: ";
    for (int x : v) cout << x << " ";   // 10 20 30 40 50
    cout << endl;
    
    v.pop_back();   // Removes 50
    
    cout << "After pop_back: ";
    for (int x : v) cout << x << " ";   // 10 20 30 40
    cout << endl;
    
    v.pop_back();   // Removes 40
    
    cout << "After 2nd pop_back: ";
    for (int x : v) cout << x << " ";   // 10 20 30
    cout << endl;
    
    return 0;
}
````

### Step-by-Step Visualization

````
Initial: v = {10, 20, 30, 40, 50}
┌──────┬──────┬──────┬──────┬──────┐
│  10  │  20  │  30  │  40  │  50  │   size = 5
├──────┼──────┼──────┼──────┼──────┤
│ [0]  │ [1]  │ [2]  │ [3]  │ [4]  │
└──────┴──────┴──────┴──────┴──────┘

═══════════════════════════════════════
v.pop_back();       ← 50 removed from the back
                                    💥
┌──────┬──────┬──────┬──────┐
│  10  │  20  │  30  │  40  │          size = 4
├──────┼──────┼──────┼──────┤
│ [0]  │ [1]  │ [2]  │ [3]  │
└──────┴──────┴──────┴──────┘

═══════════════════════════════════════
v.pop_back();       ← 40 removed from the back
                              💥
┌──────┬──────┬──────┐
│  10  │  20  │  30  │                 size = 3
├──────┼──────┼──────┤
│ [0]  │ [1]  │ [2]  │
└──────┴──────┴──────┘

⚠️ pop_back() does NOT return the removed element!
   It just removes it. If you need the value first, read it with .back()
````

### push_back vs pop_back — The Perfect Pair

````
push_back(x)  →  Adds x at the END     →  size increases by 1
pop_back()    →  Removes from the END   →  size decreases by 1

Think of it like a stack of plates:
   push_back = put a plate on top
   pop_back  = take the top plate off

    ┌───────┐ ← pop_back() removes this
    │  50   │
    ├───────┤
    │  40   │
    ├───────┤
    │  30   │
    ├───────┤
    │  20   │
    ├───────┤
    │  10   │
    └───────┘
    ↑ push_back() adds here (on top)
````

---

## 14. Front and Back — Accessing First & Last Elements

`.front()` returns the **first** element, `.back()` returns the **last** element.

### Code Example

````cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30, 40, 50};
    
    cout << "First element: " << v.front() << endl;   // 10
    cout << "Last element: "  << v.back()  << endl;   // 50
    
    // Same as:
    cout << "First (v[0]): "              << v[0]            << endl;   // 10
    cout << "Last (v[size-1]): "          << v[v.size()-1]   << endl;   // 50
    
    return 0;
}
````

### Visualization

````
v = {10, 20, 30, 40, 50}

  v.front()                              v.back()
     ↓                                      ↓
┌──────┬──────┬──────┬──────┬──────┐
│  10  │  20  │  30  │  40  │  50  │
├──────┼──────┼──────┼──────┼──────┤
│ [0]  │ [1]  │ [2]  │ [3]  │ [4]  │
└──────┴──────┴──────┴──────┴──────┘

v.front() ≡ v[0]           → Always the FIRST element
v.back()  ≡ v[v.size()-1]  → Always the LAST element

💡 .back() is especially useful before pop_back()
   to READ the value before removing it:
   
   int lastVal = v.back();    // Save it: 50
   v.pop_back();              // Now remove it
````

---

## 15. Insert — Adding Elements at Any Position

`insert()` lets you add elements at **any position** in the vector, not just the end.

### Code Example

````cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 4, 5};
    
    // Insert 99 at index 2 (before element at position 2)
    v.insert(v.begin() + 2, 99);
    // v = {1, 2, 99, 3, 4, 5}
    
    for (int x : v) cout << x << " ";
    // Output: 1 2 99 3 4 5
    
    return 0;
}
````

### How Insert Works — Deep Visualization

````
v = {1, 2, 3, 4, 5}        v.begin() points to index 0

We want: v.insert(v.begin() + 2, 99)
         ───────────────────────────
         Position = begin + 2 = index 2
         Value = 99

Step 1: Current state
┌─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │  5  │
├─────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │
└─────┴─────┴─────┴─────┴─────┘
               ↑
          Insert 99 HERE

Step 2: Shift elements [2], [3], [4] to the RIGHT by 1
┌─────┬─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │     │  3  │  4  │  5  │
├─────┼─────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │ [5] │
└─────┴─────┴─────┴─────┴─────┴─────┘
               ↑
          Empty slot created

Step 3: Place 99 in the empty slot
┌─────┬─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │ 99  │  3  │  4  │  5  │   size = 6
├─────┼─────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │ [5] │
└─────┴─────┴─────┴─────┴─────┴─────┘

⚠️ Time Complexity: O(N) — because elements need to be shifted!
````

### Insert at Different Positions

````cpp
vector<int> v = {1, 2, 3, 4, 5};

// Insert at the BEGINNING
v.insert(v.begin(), 99);              // {99, 1, 2, 3, 4, 5}

// Insert at index 3
v.insert(v.begin() + 3, 77);          // {99, 1, 2, 77, 3, 4, 5}

// Insert at the END (same as push_back)
v.insert(v.end(), 88);                // {99, 1, 2, 77, 3, 4, 5, 88}
````

### Understanding `begin() + n` — The Pointer Arithmetic

````
v = {1, 2, 3, 4, 5}

v.begin()       → points to index 0 → value 1
v.begin() + 1   → points to index 1 → value 2
v.begin() + 2   → points to index 2 → value 3
v.begin() + 3   → points to index 3 → value 4
v.begin() + 4   → points to index 4 → value 5
v.end()         → points PAST the last element (index 5)

   v.begin()                                    v.end()
      ↓                                            ↓
   ┌─────┬─────┬─────┬─────┬─────┐          ┌──────────┐
   │  1  │  2  │  3  │  4  │  5  │          │ (beyond) │
   └─────┴─────┴─────┴─────┴─────┘          └──────────┘
   +0     +1    +2    +3    +4               

💡 v.begin() + i  =  "point to index i"
````

---

## 16. Erase / Delete — Removing Elements at Any Position

`erase()` removes elements at a **specific position** or a **range of positions**.

### Erase a Single Element

````cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 4, 5};
    
    // Erase element at index 2 (which is value 3)
    v.erase(v.begin() + 2);
    // v = {1, 2, 4, 5}
    
    for (int x : v) cout << x << " ";
    // Output: 1 2 4 5
    
    return 0;
}
````

### Visualization: Erase Single Element

````
v = {1, 2, 3, 4, 5}

v.erase(v.begin() + 2);    ← Delete element at index 2

Step 1: Identify the element to delete
┌─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │  5  │
├─────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │
└─────┴─────┴─────┴─────┴─────┘
               ↑
           DELETE THIS (value = 3)

Step 2: Shift elements LEFT to fill the gap
┌─────┬─────┬─────┬─────┐
│  1  │  2  │  4  │  5  │       size = 4
├─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │
└─────┴─────┴─────┴─────┘

Result: 3 is gone, 4 and 5 shifted left
````

### Erase a Range of Elements

````cpp
vector<int> v = {1, 2, 3, 4, 5};

// Erase from index 1 to index 3 (inclusive of 1, exclusive of 3)
v.erase(v.begin() + 1, v.begin() + 3);
// Removes elements at index 1 and 2 (values 2 and 3)
// v = {1, 4, 5}
````

### Visualization: Erase a Range

````
v = {1, 2, 3, 4, 5}

v.erase(v.begin() + 1, v.begin() + 3);
        ─────────────  ─────────────── 
        start (incl.)  end (exclusive)

Which elements are deleted?
┌─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │  5  │
├─────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │
└─────┴─────┴─────┴─────┴─────┘
        ╚═══════╝
        DELETE THESE (index 1 and 2)
        range: [begin+1, begin+3)

Result:
┌─────┬─────┬─────┐
│  1  │  4  │  5  │   size = 3
├─────┼─────┼─────┤
│ [0] │ [1] │ [2] │
└─────┴─────┴─────┘

💡 Range is [start, end) — start is INCLUDED, end is EXCLUDED
   This is a common pattern in C++ STL!
````

### Erase All Occurrences Example

````
Before erase(begin+1, begin+3):

  begin    begin+1  begin+2  begin+3  begin+4
    ↓        ↓        ↓        ↓        ↓
  ┌────┐  ┌────┐  ┌────┐  ┌────┐  ┌────┐
  │ 1  │  │ 2  │  │ 3  │  │ 4  │  │ 5  │
  └────┘  └────┘  └────┘  └────┘  └────┘
          │←── ERASE ──→│
          [begin+1, begin+3)
          includes 1, excludes 3

After:
  ┌────┐  ┌────┐  ┌────┐
  │ 1  │  │ 4  │  │ 5  │
  └────┘  └────┘  └────┘
````

---

## 17. Clear — Removing All Elements

`.clear()` removes **all elements** from the vector, making it empty.

### Code Example

````cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 4, 5};
    
    cout << "Size before clear: " << v.size() << endl;    // 5
    
    v.clear();
    
    cout << "Size after clear: " << v.size() << endl;     // 0
    cout << "Is empty? " << v.empty() << endl;            // 1 (true)
    
    return 0;
}
````

### Visualization

````
Before v.clear():
┌─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │  5  │   size = 5
└─────┴─────┴─────┴─────┴─────┘

v.clear();   💥💥💥💥💥

After v.clear():
┌───────────────────────────────┐
│          (empty)              │   size = 0
└───────────────────────────────┘

⚠️ Note: clear() sets size to 0, but CAPACITY may remain unchanged!
   The memory is still allocated, just not in use.

   v.size()     → 0
   v.capacity() → might still be 8 (or whatever it was)
````

---

## 18. Sorting a Vector

The `sort()` function from STL sorts a vector. By default it sorts in **ascending (non-decreasing) order**.

### Basic Sorting (Ascending)

````cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v = {5, 3, 1, 4, 2};
    
    sort(v.begin(), v.end());    // Ascending order
    
    for (int x : v) cout << x << " ";
    // Output: 1 2 3 4 5
    
    return 0;
}
````

### Visualization: How Sort Works

````
Before sort:
┌─────┬─────┬─────┬─────┬─────┐
│  5  │  3  │  1  │  4  │  2  │
├─────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │
└─────┴─────┴─────┴─────┴─────┘

sort(v.begin(), v.end());  ← Sort entire vector

After sort (ascending / non-decreasing):
┌─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │  5  │
├─────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │
└─────┴─────┴─────┴─────┴─────┘
  ↑                          ↑
smallest                  largest

⏱️ Time Complexity: O(N log N) — very efficient!
````

### Sorting in Descending Order

````cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v = {5, 3, 1, 4, 2};
    
    // Method 1: Using greater<int>()
    sort(v.begin(), v.end(), greater<int>());
    
    for (int x : v) cout << x << " ";
    // Output: 5 4 3 2 1
    
    return 0;
}
````

### Visualization: Descending Sort

````
Before:  {5, 3, 1, 4, 2}

sort(v.begin(), v.end(), greater<int>());

After (descending / non-increasing):
┌─────┬─────┬─────┬─────┬─────┐
│  5  │  4  │  3  │  2  │  1  │
├─────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │
└─────┴─────┴─────┴─────┴─────┘
  ↑                          ↑
largest                  smallest
````

### Sorting a Partial Range

You can sort only a **portion** of the vector!

````cpp
vector<int> v = {5, 3, 1, 4, 2};

// Sort only from index 1 to index 3 (exclusive of 4)
sort(v.begin() + 1, v.begin() + 4);
// v = {5, 1, 3, 4, 2}
//       ↑  sorted ↑  
````

### Visualization: Partial Sort

````
v = {5, 3, 1, 4, 2}

sort(v.begin() + 1, v.begin() + 4);
     ──────────────  ──────────────
     start = index 1  end = index 4 (exclusive)

Before:
┌─────┬─────┬─────┬─────┬─────┐
│  5  │  3  │  1  │  4  │  2  │
├─────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │
└─────┴─────┴─────┴─────┴─────┘
        ╚══════════════╝
        Only THIS part gets sorted

After:
┌─────┬─────┬─────┬─────┬─────┐
│  5  │  1  │  3  │  4  │  2  │
├─────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │
└─────┴─────┴─────┴─────┴─────┘
  ↑     ╚══════════════╝   ↑
 unchanged  SORTED part  unchanged
````

### Understanding Non-Decreasing vs Non-Increasing

This is a common point of confusion:

````
NON-DECREASING ORDER (default sort — ascending):
  Each element ≥ previous element
  Equal elements are allowed next to each other
  
  Example: 1 2 2 3 4 4 5
           ↑ ↑ ↑ ↑ ↑ ↑ ↑
           ≤ = ≤ ≤ = ≤    ← never goes DOWN
  
  This is what sort(begin, end) gives you.

═══════════════════════════════════════════════

NON-INCREASING ORDER (descending):
  Each element ≤ previous element
  Equal elements are allowed next to each other
  
  Example: 5 4 4 3 2 2 1
           ↑ ↑ ↑ ↑ ↑ ↑ ↑
           ≥ = ≥ ≥ = ≥    ← never goes UP
  
  This is what sort(begin, end, greater<int>()) gives you.

═══════════════════════════════════════════════

STRICTLY INCREASING: 1 2 3 4 5 (NO duplicates allowed)
STRICTLY DECREASING: 5 4 3 2 1 (NO duplicates allowed)
````

---

## 19. Reverse a Vector

`reverse()` reverses the order of elements in a vector.

### Code Example

````cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 4, 5};
    
    reverse(v.begin(), v.end());
    
    for (int x : v) cout << x << " ";
    // Output: 5 4 3 2 1
    
    return 0;
}
````

### Visualization: How Reverse Works

````
v = {1, 2, 3, 4, 5}

reverse(v.begin(), v.end());

Step-by-step (elements swap from outside inward):

Step 1: Swap v[0] and v[4]
┌─────┬─────┬─────┬─────┬─────┐
│  5  │  2  │  3  │  4  │  1  │
└─────┴─────┴─────┴─────┴─────┘
  ↑←──────── SWAP ────────→↑

Step 2: Swap v[1] and v[3]
┌─────┬─────┬─────┬─────┬─────┐
│  5  │  4  │  3  │  2  │  1  │
└─────┴─────┴─────┴─────┴─────┘
        ↑←── SWAP ──→↑

Step 3: Middle element stays (odd-length)
┌─────┬─────┬─────┬─────┬─────┐
│  5  │  4  │  3  │  2  │  1  │   ✅ DONE!
└─────┴─────┴─────┴─────┴─────┘
                ↑
           stays in place

⏱️ Time Complexity: O(N/2) = O(N)
````

### Reverse a Partial Range

````cpp
vector<int> v = {1, 2, 3, 4, 5};

// Reverse only from index 1 to index 4 (exclusive)
reverse(v.begin() + 1, v.begin() + 4);
// v = {1, 4, 3, 2, 5}
````

### Visualization: Partial Reverse

````
v = {1, 2, 3, 4, 5}

reverse(v.begin() + 1, v.begin() + 4);

┌─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │  5  │
├─────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │
└─────┴─────┴─────┴─────┴─────┘
  ↑     ╚══════════════╝   ↑
 stays  REVERSE this part  stays

Result:
┌─────┬─────┬─────┬─────┬─────┐
│  1  │  4  │  3  │  2  │  5  │
└─────┴─────┴─────┴─────┴─────┘
````

### Sort Descending Using Reverse Trick

````cpp
// Method 1: sort + reverse
sort(v.begin(), v.end());          // 1 2 3 4 5
reverse(v.begin(), v.end());       // 5 4 3 2 1

// Method 2: Direct descending sort (better)
sort(v.begin(), v.end(), greater<int>());  // 5 4 3 2 1
````

---

## 20. Iterators — begin() and end() Deep Dive

Iterators are like **smart pointers** that let you traverse containers. They are the bridge between algorithms and containers.

### Types of Iterators

````
                   v.begin()                    v.end()
FORWARD:              ↓                            ↓
                   ┌─────┬─────┬─────┬─────┬─────┐  ┌──────┐
                   │  1  │  2  │  3  │  4  │  5  │  │(past)│
                   └─────┴─────┴─────┴─────┴─────┘  └──────┘
                   ═══════════════════════════════→
                        iterator goes forward (++)

                  v.rbegin()                  v.rend()
REVERSE:              ↓                          ↓
              ┌──────┐  ┌─────┬─────┬─────┬─────┬─────┐
              │(past)│  │  1  │  2  │  3  │  4  │  5  │
              └──────┘  └─────┴─────┴─────┴─────┴─────┘
              ←═══════════════════════════════════
                   reverse iterator goes backward (++)
````

### Forward Iterator Example

````cpp
vector<int> v = {10, 20, 30, 40, 50};

// Using forward iterator
for (auto it = v.begin(); it != v.end(); it++) {
    cout << *it << " ";
}
// Output: 10 20 30 40 50
````

### Reverse Iterator Example

````cpp
vector<int> v = {10, 20, 30, 40, 50};

// Using reverse iterator
for (auto it = v.rbegin(); it != v.rend(); it++) {
    cout << *it << " ";
}
// Output: 50 40 30 20 10
````

### Visualization: Reverse Iterator

````
v = {10, 20, 30, 40, 50}

                v.rend()                       v.rbegin()
                   ↓                               ↓
            ┌──────┐┌──────┬──────┬──────┬──────┬──────┐
            │before││  10  │  20  │  30  │  40  │  50  │
            └──────┘└──────┴──────┴──────┴──────┴──────┘

Iteration with rbegin → rend:
  it = rbegin → *it = 50
  it++        → *it = 40   (++ on reverse iterator moves LEFT)
  it++        → *it = 30
  it++        → *it = 20
  it++        → *it = 10
  it++        → it == rend → STOP

Output: 50 40 30 20 10
````

### Iterator Arithmetic Cheat Sheet

````
auto it = v.begin();    // Points to first element

*it         → Value at iterator position (dereference)
it++        → Move to next element
it--        → Move to previous element
it + n      → Jump forward n positions
it - n      → Jump backward n positions
it1 - it2   → Distance between two iterators

Example:
v = {10, 20, 30, 40, 50}
auto it = v.begin();     // points to 10

*it        → 10
*(it + 2)  → 30
*(it + 4)  → 50

auto it2 = v.begin() + 1;   // points to 20
auto it3 = v.begin() + 4;   // points to 50
int dist = it3 - it2;       // 3
````

---

## 21. Passing Vectors to Functions

### Pass by Value (Creates a Copy — Slow)

````cpp
void printVector(vector<int> v) {    // COPY of vector is made
    for (int x : v) cout << x << " ";
    cout << endl;
}

int main() {
    vector<int> v = {1, 2, 3, 4, 5};
    printVector(v);   // Passes a COPY
    return 0;
}
````

### Pass by Reference (No Copy — Fast, Can Modify)

````cpp
void modifyVector(vector<int>& v) {   // & means reference (no copy)
    v.push_back(100);                  // This modifies the ORIGINAL
}

int main() {
    vector<int> v = {1, 2, 3, 4, 5};
    modifyVector(v);
    // v is now {1, 2, 3, 4, 5, 100}
    return 0;
}
````

### Pass by Const Reference (No Copy — Fast, Can't Modify)

````cpp
void printVector(const vector<int>& v) {   // Can't modify v
    for (int x : v) cout << x << " ";
    cout << endl;
}
````

### Visualization: Value vs Reference

````
Pass by VALUE:
┌─── main() ───┐         ┌── function() ──┐
│ v = {1,2,3}  │ ──COPY──→│ v = {1,2,3}   │  ← Separate copy!
│              │         │ (independent)   │
└──────────────┘         └────────────────┘
Changes in function do NOT affect original.
⚠️ Slow for large vectors (copying takes O(N) time)

Pass by REFERENCE (&):
┌─── main() ───┐         ┌── function() ──┐
│ v = {1,2,3}  │←─SAME──→│ v (alias)      │  ← Same memory!
│              │ MEMORY  │                │
└──────────────┘         └────────────────┘
Changes in function AFFECT original.
✅ Fast! No copying.

Pass by CONST REFERENCE (const &):
┌─── main() ───┐         ┌── function() ──────┐
│ v = {1,2,3}  │←─SAME──→│ v (read-only alias)│  ← Same memory
│              │ MEMORY  │ ❌ Can't modify    │
└──────────────┘         └────────────────────┘
✅ Fast AND safe — best for "read-only" functions
````

### Return a Vector from Function

````cpp
vector<int> createVector(int n) {
    vector<int> v;
    for (int i = 1; i <= n; i++) {
        v.push_back(i * i);
    }
    return v;    // Return the vector
}

int main() {
    vector<int> squares = createVector(5);
    // squares = {1, 4, 9, 16, 25}
    
    for (int x : squares) cout << x << " ";
    return 0;
}
````

---

## 22. 2D Vectors (Vector of Vectors)

A 2D vector is a **vector of vectors** — think of it as a **dynamic 2D array** (like a matrix/table).

### Declaration

````cpp
// Method 1: Empty 2D vector
vector<vector<int>> v2d;

// Method 2: Fixed rows and columns, all zeros
int rows = 3, cols = 4;
vector<vector<int>> matrix(rows, vector<int>(cols, 0));

// Method 3: Initialize with values
vector<vector<int>> grid = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
````

### Visualization: 2D Vector Structure

````
vector<vector<int>> grid = {
    {1, 2, 3},      ← row 0
    {4, 5, 6},      ← row 1
    {7, 8, 9}       ← row 2
};

Visual as a matrix:

         col 0   col 1   col 2
        ┌───────┬───────┬───────┐
row 0   │   1   │   2   │   3   │   grid[0]
        ├───────┼───────┼───────┤
row 1   │   4   │   5   │   6   │   grid[1]
        ├───────┼───────┼───────┤
row 2   │   7   │   8   │   9   │   grid[2]
        └───────┴───────┴───────┘

Access: grid[row][col]
  grid[0][0] = 1
  grid[1][2] = 6
  grid[2][1] = 8

Memory model (vector of vectors):
┌──────────────┐
│  grid        │
│  ┌─────────┐ │
│  │ row 0   │─┼──→ [1, 2, 3]
│  ├─────────┤ │
│  │ row 1   │─┼──→ [4, 5, 6]
│  ├─────────┤ │
│  │ row 2   │─┼──→ [7, 8, 9]
│  └─────────┘ │
└──────────────┘

💡 Each row is itself a vector<int>
   Rows can have DIFFERENT sizes (jagged array)!
````

### Iterating a 2D Vector

````cpp
vector<vector<int>> grid = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Method 1: Index-based
for (int i = 0; i < grid.size(); i++) {
    for (int j = 0; j < grid[i].size(); j++) {
        cout << grid[i][j] << " ";
    }
    cout << endl;
}

// Method 2: Range-based
for (auto& row : grid) {
    for (int val : row) {
        cout << val << " ";
    }
    cout << endl;
}
````

### Visualization: The Nested Loop

````
Outer loop i = 0 (row 0):
  Inner loop j = 0: grid[0][0] = 1
  Inner loop j = 1: grid[0][1] = 2
  Inner loop j = 2: grid[0][2] = 3
  → prints: 1 2 3

Outer loop i = 1 (row 1):
  Inner loop j = 0: grid[1][0] = 4
  Inner loop j = 1: grid[1][1] = 5
  Inner loop j = 2: grid[1][2] = 6
  → prints: 4 5 6

Outer loop i = 2 (row 2):
  Inner loop j = 0: grid[2][0] = 7
  Inner loop j = 1: grid[2][1] = 8
  Inner loop j = 2: grid[2][2] = 9
  → prints: 7 8 9
````

### Dynamic 2D Vector (Adding Rows)

````cpp
vector<vector<int>> v2d;

// Add row by row
v2d.push_back({1, 2, 3});
v2d.push_back({4, 5, 6, 7});    // Different size! This is fine.
v2d.push_back({8, 9});

// This creates a JAGGED array:
// Row 0: [1, 2, 3]       (3 elements)
// Row 1: [4, 5, 6, 7]    (4 elements)
// Row 2: [8, 9]           (2 elements)
````

### Visualization: Jagged 2D Vector

````
v2d (jagged — rows have different sizes):

        ┌─────┬─────┬─────┐
row 0   │  1  │  2  │  3  │              size = 3
        └─────┴─────┴─────┘
        ┌─────┬─────┬─────┬─────┐
row 1   │  4  │  5  │  6  │  7  │        size = 4
        └─────┴─────┴─────┴─────┘
        ┌─────┬─────┐
row 2   │  8  │  9  │                    size = 2
        └─────┴─────┘

v2d.size()       = 3     (number of rows)
v2d[0].size()    = 3     (columns in row 0)
v2d[1].size()    = 4     (columns in row 1)
v2d[2].size()    = 2     (columns in row 2)

💡 Unlike 2D arrays, each row in a 2D vector can have a DIFFERENT length!
````

---

## 23. Practice Problems & Tips

### ✅ Standard Vector Problems to Practice

| # | Problem | Key Concept |
|---|---------|-------------|
| 1 | Read N elements, print in reverse | `push_back`, `reverse` or backward loop |
| 2 | Find the max/min element | `*max_element(v.begin(), v.end())` |
| 3 | Sort and remove duplicates | `sort` + `unique` + `erase` |
| 4 | Rotate array by K positions | Use `rotate()` or manual method |
| 5 | Merge two sorted vectors | Two-pointer technique |
| 6 | 2D matrix problems | 2D vectors, nested loops |

### 💡 Essential Tips

````
TIP 1: Always use .size() instead of hardcoding length
   ❌  for (int i = 0; i < 5; i++)
   ✅  for (int i = 0; i < v.size(); i++)

TIP 2: Use range-based for when you don't need the index
   ✅  for (int x : v) cout << x;

TIP 3: Use & in range-based for to avoid copying
   ❌  for (vector<int> row : grid)     // Copies each row!
   ✅  for (auto& row : grid)           // Reference, no copy

TIP 4: Reserve memory if you know the size in advance
   vector<int> v;
   v.reserve(1000000);   // Pre-allocates memory for 1M elements
                          // Avoids multiple reallocations

TIP 5: Use emplace_back instead of push_back for complex types
   v.emplace_back(args);  // Constructs in-place, slightly faster

TIP 6: Check empty before accessing
   if (!v.empty()) {
       cout << v.front();
   }
````

---

## 24. Complete Cheat Sheet

````cpp
// ═══════════════════════════════════════════════════
//    COMPLETE VECTOR CHEAT SHEET (Part 1 + Part 2)
// ═══════════════════════════════════════════════════

#include <bits/stdc++.h>
using namespace std;

int main() {
    
    // ─── DECLARATION ───────────────────────────────
    vector<int> v;                     // empty
    vector<int> v2(5);                 // [0,0,0,0,0]
    vector<int> v3(5, 10);            // [10,10,10,10,10]
    vector<int> v4 = {1, 2, 3, 4};    // [1,2,3,4]
    vector<int> v5(v4);               // copy of v4
    
    // ─── ADDING ELEMENTS ──────────────────────────
    v.push_back(100);                  // add at END
    v.insert(v.begin() + 2, 99);       // add at index 2
    
    // ─── REMOVING ELEMENTS ────────────────────────
    v.pop_back();                      // remove LAST
    v.erase(v.begin() + 1);           // remove at index 1
    v.erase(v.begin(), v.begin()+3);  // remove range [0,3)
    v.clear();                         // remove ALL
    
    // ─── ACCESSING ────────────────────────────────
    cout << v4[0];                     // first (no bounds check)
    cout << v4.at(0);                  // first (bounds check)
    cout << v4.front();                // first element
    cout << v4.back();                 // last element
    
    // ─── SIZE & CAPACITY ──────────────────────────
    cout << v4.size();                 // number of elements
    cout << v4.capacity();             // allocated slots
    cout << v4.empty();                // true if size == 0
    
    // ─── SORTING ──────────────────────────────────
    sort(v4.begin(), v4.end());                   // ascending
    sort(v4.begin(), v4.end(), greater<int>());    // descending
    
    // ─── REVERSING ────────────────────────────────
    reverse(v4.begin(), v4.end());     // reverse entire vector
    
    // ─── ITERATING ────────────────────────────────
    // Index-based
    for (int i = 0; i < v4.size(); i++)
        cout << v4[i] << " ";
    
    // Range-based
    for (int x : v4)
        cout << x << " ";
    
    // Forward iterator
    for (auto it = v4.begin(); it != v4.end(); it++)
        cout << *it << " ";
    
    // Reverse iterator
    for (auto it = v4.rbegin(); it != v4.rend(); it++)
        cout << *it << " ";
    
    // ─── 2D VECTOR ────────────────────────────────
    vector<vector<int>> grid(3, vector<int>(4, 0));  // 3x4 matrix of 0s
    grid[0][0] = 1;
    
    for (auto& row : grid) {
        for (int val : row)
            cout << val << " ";
        cout << "\n";
    }
    
    return 0;
}
````

---

## 📊 Time Complexity Summary

| Operation | Time Complexity | Notes |
|-----------|:--------------:|-------|
| `push_back()` | **O(1)** amortized | Occasionally O(N) during reallocation |
| `pop_back()` | **O(1)** | Always constant |
| `front()` / `back()` | **O(1)** | Direct access |
| `v[i]` / `v.at(i)` | **O(1)** | Random access by index |
| `size()` / `empty()` | **O(1)** | Stored internally |
| `insert()` | **O(N)** | Elements must shift right |
| `erase()` | **O(N)** | Elements must shift left |
| `clear()` | **O(N)** | Destroys all elements |
| `sort()` | **O(N log N)** | IntroSort (hybrid algorithm) |
| `reverse()` | **O(N)** | Swaps from ends to middle |
| `find()` | **O(N)** | Linear search |

### Visual: When to Use What

````
Need to add/remove at END?
  → push_back() / pop_back()     ⚡ O(1)

Need to add/remove in MIDDLE?
  → insert() / erase()           🐢 O(N)  (consider list if frequent)

Need sorted data?
  → sort()                       ⚡ O(N log N)

Need to search?
  → Unsorted: find()             🐢 O(N)
  → Sorted: binary_search()      ⚡ O(log N)

Need 2D data?
  → vector<vector<int>>          Dynamic matrix
````

---

## 🎯 Key Takeaways from Part 2

| Concept | Key Point |
|---------|-----------|
| **pop_back()** | Removes last element, O(1), doesn't return value |
| **front() / back()** | Access first/last element in O(1) |
| **insert()** | Add at any position, but O(N) due to shifting |
| **erase()** | Remove at any position or range, O(N) |
| **clear()** | Remove all elements, size → 0 |
| **sort()** | O(N log N), ascending by default, use `greater<>()` for descending |
| **reverse()** | O(N), reverses in-place |
| **Iterators** | begin/end for forward, rbegin/rend for reverse |
| **Pass by reference** | Use `&` to avoid copying vectors in functions |
| **2D Vectors** | `vector<vector<int>>` — dynamic matrix with variable row sizes |

