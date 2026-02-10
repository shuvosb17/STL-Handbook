

# 📘 Ultimate STL String Notes

> **Course**: C++ Standard Template Library (STL)
> **Topic**: Almost Everything About STL String
> **Level**: Beginner-Friendly with In-Depth Visualizations

---

## 📌 Table of Contents

1. What is an STL String?
2. Character Array vs STL String
3. Declaring & Initializing Strings
4. Accessing Characters (Indexing)
5. String Size / Length
6. Push Back & Pop Back on Strings
7. String Concatenation (Adding Strings)
8. String Comparison
9. String Input — cin vs getline
10. Iterating Through a String
11. Sorting a String
12. Reversing a String
13. Substring — Extracting Part of a String
14. Find — Searching Inside a String
15. Erase — Removing Characters
16. Insert — Adding Characters at a Position
17. Replace — Replacing Part of a String
18. Character Type Checking (Upper/Lower/Digit)
19. Case Conversion (toupper / tolower)
20. Clear & Empty
21. String as a Vector of Characters
22. Convert String to Integer & Vice Versa
23. Useful String Functions — Quick Reference
24. Practice Problems & Tips
25. Complete Cheat Sheet

---

## 1. What is an STL String?

An STL **string** is a **dynamic array of characters** provided by C++. It's essentially like a `vector<char>` but with many extra string-specific operations built in.

### Header

````cpp
#include <string>       // specific header
// or
#include <bits/stdc++.h> // includes everything
using namespace std;
````

### Why use `string` instead of `char[]`?

| Feature | `char[]` (C-style) | `string` (STL) |
|---------|-------------------:|---------------:|
| Size | Fixed at declaration | Dynamic — grows/shrinks |
| Concatenation | Manual with `strcat()` | Simple with `+` operator |
| Comparison | `strcmp()` function | `==`, `<`, `>` operators |
| Length | `strlen()` — O(N) each call | `.size()` — O(1) |
| Safety | Buffer overflow risk | Automatic memory management |
| Input with spaces | `gets()` (unsafe) | `getline()` |

> 💡 Think of `char[]` as a **static array** and `string` as a **vector** — same relationship! The STL string handles memory for you.

### Visualization: What's Inside a String?

````
string s = "ABCD";

Internally, it's a dynamic array of characters:

Index:   [0]   [1]   [2]   [3]
       ┌─────┬─────┬─────┬─────┐
Value: │ 'A' │ 'B' │ 'C' │ 'D' │    size = 4
       └─────┴─────┴─────┴─────┘

Each element is a single CHARACTER (char type)
Characters are enclosed in SINGLE quotes: 'A', 'B', etc.
Strings are enclosed in DOUBLE quotes: "ABCD"
````

---

## 2. Character Array vs STL String

### C-Style Character Array

````cpp
char name[10] = "Hello";   // Fixed size 10
// name[5] = '\0' (null terminator — marks end of string)
````

````
Memory Layout (char array):
┌─────┬─────┬─────┬─────┬─────┬──────┬─────┬─────┬─────┬─────┐
│ 'H' │ 'e' │ 'l' │ 'l' │ 'o' │ '\0' │  ?  │  ?  │  ?  │  ?  │
├─────┼─────┼─────┼─────┼─────┼──────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │ [5]  │ [6] │ [7] │ [8] │ [9] │
└─────┴─────┴─────┴─────┴─────┴──────┴─────┴─────┴─────┴─────┘
                                  ↑
                           Null terminator
                           (marks the end)
  
❌ Size is FIXED at 10
❌ Wasting slots [6] to [9]
❌ Need to manually manage '\0'
````

### STL String

````cpp
string name = "Hello";   // Dynamic size
````

````
Memory Layout (STL string):
┌─────┬─────┬─────┬─────┬─────┐
│ 'H' │ 'e' │ 'l' │ 'l' │ 'o' │     size = 5
├─────┼─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │ [4] │
└─────┴─────┴─────┴─────┴─────┘

✅ No null terminator to worry about
✅ Size adjusts automatically
✅ Built-in operations (concatenation, comparison, etc.)
````

---

## 3. Declaring & Initializing Strings

````cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    // Method 1: Empty string
    string s1;                        // ""
    
    // Method 2: Initialize with a value
    string s2 = "Hello";             // "Hello"
    
    // Method 3: Using constructor
    string s3("World");              // "World"
    
    // Method 4: Repeat a character N times
    string s4(5, 'A');               // "AAAAA"
    
    // Method 5: Copy from another string
    string s5 = s2;                  // "Hello" (copy of s2)
    
    // Method 6: From part of another string
    string s6(s2, 1, 3);            // "ell" (from index 1, take 3 chars)
    
    return 0;
}
````

### Visualization: All Initialization Methods

````
s1 = "";          (empty)
┌──────────┐
│  (empty) │     size = 0
└──────────┘

s2 = "Hello";
┌─────┬─────┬─────┬─────┬─────┐
│ 'H' │ 'e' │ 'l' │ 'l' │ 'o' │     size = 5
└─────┴─────┴─────┴─────┴─────┘

s4 = string(5, 'A');
┌─────┬─────┬─────┬─────┬─────┐
│ 'A' │ 'A' │ 'A' │ 'A' │ 'A' │     size = 5
└─────┴─────┴─────┴─────┴─────┘

s6 = string(s2, 1, 3);  → substring of "Hello" from index 1, length 3
                 H  e  l  l  o
                [0][1][2][3][4]
                     ╚═══╗
                     "ell"
┌─────┬─────┬─────┐
│ 'e' │ 'l' │ 'l' │                  size = 3
└─────┴─────┴─────┘
````

---

## 4. Accessing Characters (Indexing)

Just like arrays and vectors, you access individual characters using **index notation**.

### Code Example

````cpp
string s = "ABCD";

// Access using []
cout << s[0] << endl;     // 'A'
cout << s[1] << endl;     // 'B'
cout << s[2] << endl;     // 'C'
cout << s[3] << endl;     // 'D'

// Access using .at() — with bounds checking
cout << s.at(0) << endl;  // 'A'

// Modify a character
s[0] = 'Z';               // s = "ZBCD"
````

### Visualization

````
s = "ABCD"

Index:   [0]   [1]   [2]   [3]
       ┌─────┬─────┬─────┬─────┐
       │ 'A' │ 'B' │ 'C' │ 'D' │
       └─────┴─────┴─────┴─────┘

s[0] → 'A'    (first character)
s[1] → 'B'    (second character)
s[2] → 'C'    (third character)
s[3] → 'D'    (last character)

⚠️ s[4] → UNDEFINED BEHAVIOR! (out of bounds)

Modifying:
s[0] = 'Z';

       ┌─────┬─────┬─────┬─────┐
       │ 'Z' │ 'B' │ 'C' │ 'D' │    → "ZBCD"
       └─────┴─────┴─────┴─────┘
         ↑
      Changed!
````

### First and Last Character

````cpp
string s = "ABCD";

// First character
cout << s.front() << endl;     // 'A'
cout << s[0] << endl;          // 'A'

// Last character
cout << s.back() << endl;      // 'D'
cout << s[s.size()-1] << endl; // 'D'
````

````
s = "ABCD"

  s.front()                s.back()
     ↓                        ↓
┌─────┬─────┬─────┬─────┐
│ 'A' │ 'B' │ 'C' │ 'D' │
├─────┼─────┼─────┼─────┤
│ [0] │ [1] │ [2] │ [3] │
└─────┴─────┴─────┴─────┘

s.front() ≡ s[0]
s.back()  ≡ s[s.size() - 1]
````

---

## 5. String Size / Length

Two functions that do the **exact same thing**:

````cpp
string s = "Hello World";

cout << s.size()   << endl;   // 11
cout << s.length() << endl;   // 11  (same as size)
````

### Visualization

````
s = "Hello World"

┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ H │ e │ l │ l │ o │   │ W │ o │ r │ l │ d │
├───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┤
│[0]│[1]│[2]│[3]│[4]│[5]│[6]│[7]│[8]│[9]│[10]│
└───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘

s.size()   = 11
s.length() = 11

💡 The SPACE character counts as a character too!
💡 .size() and .length() are identical — use whichever you prefer.
   Most competitive programmers use .size()
````

---

## 6. Push Back & Pop Back on Strings

Just like vectors, strings support `push_back()` and `pop_back()`.

### Code Example

````cpp
string s = "ABC";

s.push_back('D');       // s = "ABCD"
s.push_back('E');       // s = "ABCDE"

cout << s << endl;      // ABCDE

s.pop_back();           // s = "ABCD"  (removed 'E')
s.pop_back();           // s = "ABC"   (removed 'D')

cout << s << endl;      // ABC
````

### Visualization

````
Initial: s = "ABC"
┌─────┬─────┬─────┐
│ 'A' │ 'B' │ 'C' │     size = 3
└─────┴─────┴─────┘

s.push_back('D');        ← 'D' added at the end
┌─────┬─────┬─────┬─────┐
│ 'A' │ 'B' │ 'C' │ 'D' │     size = 4
└─────┴─────┴─────┴─────┘

s.push_back('E');        ← 'E' added at the end
┌─────┬─────┬─────┬─────┬─────┐
│ 'A' │ 'B' │ 'C' │ 'D' │ 'E' │     size = 5
└─────┴─────┴─────┴─────┴─────┘

s.pop_back();            ← 'E' removed from the end  💥
┌─────┬─────┬─────┬─────┐
│ 'A' │ 'B' │ 'C' │ 'D' │     size = 4
└─────┴─────┴─────┴─────┘

s.pop_back();            ← 'D' removed from the end  💥
┌─────┬─────┬─────┐
│ 'A' │ 'B' │ 'C' │     size = 3
└─────┴─────┴─────┘

⚠️ push_back() only takes a SINGLE character (char), not a string!
   s.push_back('D');    ✅  (single quotes = char)
   s.push_back("D");   ❌  (double quotes = string — ERROR!)
````

---

## 7. String Concatenation (Adding Strings)

You can **combine** strings using the `+` operator or `+=` operator.

### Code Example

````cpp
string s1 = "Hello";
string s2 = " World";

// Method 1: Using + operator
string s3 = s1 + s2;          // "Hello World"

// Method 2: Using += operator
s1 += s2;                     // s1 = "Hello World"

// Method 3: Append function
string s4 = "Good";
s4.append(" Morning");        // s4 = "Good Morning"

// Adding a character
string s5 = "ABC";
s5 += 'D';                    // s5 = "ABCD"

cout << s3 << endl;           // Hello World
cout << s1 << endl;           // Hello World
cout << s4 << endl;           // Good Morning
````

### Visualization

````
s1 = "Hello"          s2 = " World"

┌───┬───┬───┬───┬───┐  ┌───┬───┬───┬───┬───┬───┐
│ H │ e │ l │ l │ o │  │   │ W │ o │ r │ l │ d │
└───┴───┴───┴───┴───┘  └───┴───┴───┴───┴───┴───┘

s3 = s1 + s2;   →  "Hello" + " World"

┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ H │ e │ l │ l │ o │   │ W │ o │ r │ l │ d │
└───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘
│←── from s1 ──→│←────── from s2 ──────→│

s3 = "Hello World"    size = 11

═══════════════════════════════════════════
s5 = "ABC";
s5 += 'D';    →  "ABC" + 'D'

Before:                  After:
┌───┬───┬───┐           ┌───┬───┬───┬───┐
│ A │ B │ C │    →→→    │ A │ B │ C │ D │
└───┴───┴───┘           └───┴───┴───┴───┘

💡 += with a char is equivalent to push_back()
   s5 += 'D';     ≡     s5.push_back('D');
````

### Concatenation Operator Comparison

````
+    →  Creates a NEW string (original unchanged)
+=   →  MODIFIES the original string (more efficient)
.append() → Same as +=

string a = "Hello";
string b = " World";

string c = a + b;   // a is still "Hello", c = "Hello World"
a += b;             // a is now "Hello World"
````

---

## 8. String Comparison

Strings can be compared using **relational operators** (`==`, `!=`, `<`, `>`, `<=`, `>=`). Comparison is done **lexicographically** (dictionary order).

### Code Example

````cpp
string s1 = "Hello";
string s2 = "Hello";
string s3 = "World";

cout << (s1 == s2) << endl;    // 1 (true)  — same content
cout << (s1 == s3) << endl;    // 0 (false) — different
cout << (s1 != s3) << endl;    // 1 (true)
cout << (s1 < s3)  << endl;    // 1 (true)  — "Hello" < "World"
cout << (s1 > s3)  << endl;    // 0 (false)
````

### How Lexicographic Comparison Works

````
Comparison: "Hello" vs "World"

Compare character by character from left to right:

Position 0:  'H' vs 'W'
             ASCII 72 vs ASCII 87
             72 < 87 → "Hello" < "World"
             
STOP! First difference found.
Result: "Hello" < "World"  ✅

═══════════════════════════════════════════
Comparison: "abc" vs "abd"

Position 0: 'a' == 'a' → continue
Position 1: 'b' == 'b' → continue
Position 2: 'c' vs 'd'
            ASCII 99 vs ASCII 100
            99 < 100 → "abc" < "abd"

═══════════════════════════════════════════
Comparison: "abc" vs "abcd"

Position 0: 'a' == 'a' → continue
Position 1: 'b' == 'b' → continue
Position 2: 'c' == 'c' → continue
Position 3: first string ended, second has 'd'
            → shorter string is "less than" → "abc" < "abcd"

════════════════════════════════════════════
Key Rule: Comparison is CASE-SENSITIVE!

'A' (65) < 'Z' (90) < 'a' (97) < 'z' (122)

So: "Apple" < "apple"  (because 'A' < 'a')
    "Zebra" < "apple"  (because 'Z' < 'a')
````

### ASCII Value Reference

````
Character    ASCII Value
─────────    ───────────
'0' - '9'   48 - 57
'A' - 'Z'   65 - 90
'a' - 'z'   97 - 122
' ' (space)  32

Important:  UPPERCASE letters come BEFORE lowercase!
            All digits come BEFORE all letters!
            
            '0' < '9' < 'A' < 'Z' < 'a' < 'z'
             48   57    65    90    97   122
````

---

## 9. String Input — cin vs getline

This is one of the **most important** concepts! `cin` and `getline` behave very differently.

### `cin >>` — Reads Until Space

````cpp
string s;
cin >> s;

// Input: "Hello World"
// s = "Hello"   ← Only first word! Stops at space.
````

### `getline()` — Reads Entire Line (Including Spaces)

````cpp
string s;
getline(cin, s);

// Input: "Hello World"
// s = "Hello World"   ← Full line with spaces!
````

### Visualization: cin vs getline

````
User types: "Hello World"

═══════════════════════════════════════
Using cin >> s:

Input stream: H e l l o   W o r l d \n
              ─────────↑
              STOPS at first space!

s = "Hello"
Remaining in stream: " World\n"

═══════════════════════════════════════
Using getline(cin, s):

Input stream: H e l l o   W o r l d \n
              ───────────────────────↑
              STOPS at newline (\n)

s = "Hello World"
Remaining in stream: (empty)
````

### ⚠️ The Deadly Bug: cin Before getline

````cpp
int n;
cin >> n;           // Reads number, leaves '\n' in buffer

string s;
getline(cin, s);    // Reads the leftover '\n' — EMPTY STRING!
````

### Fix: Use `cin.ignore()`

````cpp
int n;
cin >> n;
cin.ignore();       // ← Consumes the leftover '\n'

string s;
getline(cin, s);    // Now works correctly!
````

### Visualization: The Buffer Problem

````
User types: "5\nHello World\n"

Step 1: cin >> n;
Buffer: 5 \n H e l l o   W o r l d \n
        ↑
        Reads 5, stops before \n
        n = 5
Buffer remaining: \n H e l l o   W o r l d \n

Step 2: getline(cin, s);  (WITHOUT cin.ignore())
Buffer: \n H e l l o   W o r l d \n
        ↑
        Reads until \n — immediately finds \n!
        s = ""  ← EMPTY! Bug! 🐛

═══════════════════════════════════════

With cin.ignore():

Step 1: cin >> n;     → n = 5
Buffer remaining: \n H e l l o   W o r l d \n

Step 2: cin.ignore(); → consumes \n
Buffer remaining: H e l l o   W o r l d \n

Step 3: getline(cin, s);
Buffer: H e l l o   W o r l d \n
        ──────────────────────↑
        s = "Hello World"  ✅ Correct!
````

### Multiple String Input with Spaces

````cpp
int n;
cin >> n;
cin.ignore();        // Important!

for (int i = 0; i < n; i++) {
    string s;
    getline(cin, s);
    cout << s << endl;
}
````

---

## 10. Iterating Through a String

### Method 1: Index-Based For Loop

````cpp
string s = "ABCDE";

for (int i = 0; i < s.size(); i++) {
    cout << s[i] << " ";
}
// Output: A B C D E
````

### Method 2: Range-Based For Loop

````cpp
string s = "ABCDE";

for (char c : s) {
    cout << c << " ";
}
// Output: A B C D E
````

### Method 3: Using Iterators

````cpp
string s = "ABCDE";

for (auto it = s.begin(); it != s.end(); it++) {
    cout << *it << " ";
}
// Output: A B C D E
````

### Method 4: Reverse Iteration

````cpp
string s = "ABCDE";

// Using reverse iterator
for (auto it = s.rbegin(); it != s.rend(); it++) {
    cout << *it << " ";
}
// Output: E D C B A

// Or using backward index loop
for (int i = s.size() - 1; i >= 0; i--) {
    cout << s[i] << " ";
}
// Output: E D C B A
````

### Visualization

````
s = "ABCDE"

Forward iteration (i = 0 to 4):
  i=0  i=1  i=2  i=3  i=4
  ─→   ─→   ─→   ─→   ─→
┌─────┬─────┬─────┬─────┬─────┐
│ 'A' │ 'B' │ 'C' │ 'D' │ 'E' │
└─────┴─────┴─────┴─────┴─────┘
Output: A B C D E

Reverse iteration (i = 4 to 0):
  i=4  i=3  i=2  i=1  i=0
  ←─   ←─   ←─   ←─   ←─
┌─────┬─────┬─────┬─────┬─────┐
│ 'A' │ 'B' │ 'C' │ 'D' │ 'E' │
└─────┴─────┴─────┴─────┴─────┘
Output: E D C B A
````

---

## 11. Sorting a String

The `sort()` function works on strings just like vectors — it sorts **characters** in order.

### Code Example

````cpp
string s = "DCBA";

sort(s.begin(), s.end());          // Ascending
cout << s << endl;                 // "ABCD"

sort(s.begin(), s.end(), greater<char>());  // Descending
cout << s << endl;                 // "DCBA"
````

### Visualization

````
s = "DCBA"

sort(s.begin(), s.end());      ← Ascending (by ASCII value)

Before:
┌─────┬─────┬─────┬─────┐
│ 'D' │ 'C' │ 'B' │ 'A' │
│ 68  │ 67  │ 66  │ 65  │  ← ASCII values
└─────┴─────┴─────┴─────┘

After:
┌─────┬─────┬─────┬─────┐
│ 'A' │ 'B' │ 'C' │ 'D' │
│ 65  │ 66  │ 67  │ 68  │  ← Sorted by ASCII
└─────┴─────┴─────┴─────┘

s = "ABCD"

═══════════════════════════════════════
Example with mixed case:

s = "bAdC"
sort(s.begin(), s.end());

Before: b(98) A(65) d(100) C(67)
After:  A(65) C(67) b(98)  d(100)

Result: "ACbd"

💡 UPPERCASE letters come before lowercase because
   'A'(65) < 'Z'(90) < 'a'(97) < 'z'(122)
````

---

## 12. Reversing a String

### Code Example

````cpp
string s = "Hello";

reverse(s.begin(), s.end());
cout << s << endl;             // "olleH"
````

### Visualization

````
s = "Hello"

reverse(s.begin(), s.end());

Step 1: Swap s[0] and s[4]
┌─────┬─────┬─────┬─────┬─────┐
│ 'o' │ 'e' │ 'l' │ 'l' │ 'H' │
└─────┴─────┴─────┴─────┴─────┘
  ↑←─────────SWAP──────────→↑

Step 2: Swap s[1] and s[3]
┌─────┬─────┬─────┬─────┬─────┐
│ 'o' │ 'l' │ 'l' │ 'e' │ 'H' │
└─────┴─────┴─────┴─────┴─────┘
        ↑←──SWAP──→↑

Step 3: Middle stays
┌─────┬─────┬─────┬─────┬─────┐
│ 'o' │ 'l' │ 'l' │ 'e' │ 'H' │   ✅ DONE!
└─────┴─────┴─────┴─────┴─────┘

s = "olleH"
````

### Reverse a Partial Range

````cpp
string s = "ABCDE";

reverse(s.begin() + 1, s.begin() + 4);
// Reverses characters at index 1, 2, 3
// s = "ADCBE"
````

````
s = "ABCDE"
reverse(s.begin() + 1, s.begin() + 4);

┌─────┬─────┬─────┬─────┬─────┐
│ 'A' │ 'B' │ 'C' │ 'D' │ 'E' │
└─────┴─────┴─────┴─────┴─────┘
  ↑     ╚══════════════╝   ↑
stays  REVERSE this part  stays

Result:
┌─────┬─────┬─────┬─────┬─────┐
│ 'A' │ 'D' │ 'C' │ 'B' │ 'E' │
└─────┴─────┴─────┴─────┴─────┘
s = "ADCBE"
````

---

## 13. Substring — Extracting Part of a String

`.substr(start_index, length)` extracts a portion of the string.

### Code Example

````cpp
string s = "Hello World";

string sub1 = s.substr(0, 5);     // "Hello"
string sub2 = s.substr(6, 5);     // "World"
string sub3 = s.substr(6);        // "World" (from index 6 to end)
string sub4 = s.substr(3, 4);     // "lo W"
````

### Visualization

````
s = "Hello World"

Index: [0][1][2][3][4][5][6][7][8][9][10]
        H  e  l  l  o     W  o  r  l   d

═══════════════════════════════════════
s.substr(0, 5);     start=0, length=5
        ╔═══════════╗
        H  e  l  l  o     W  o  r  l   d
        ╚═══════════╝
Result: "Hello"

═══════════════════════════════════════
s.substr(6, 5);     start=6, length=5
                          ╔═══════════╗
        H  e  l  l  o     W  o  r  l   d
                          ╚═══════════╝
Result: "World"

═══════════════════════════════════════
s.substr(6);        start=6, length=rest
                          ╔═══════════╗
        H  e  l  l  o     W  o  r  l   d
                          ╚═══════════╝
Result: "World"  (takes everything from index 6 to end)

═══════════════════════════════════════
s.substr(3, 4);     start=3, length=4
                 ╔════════════╗
        H  e  l  l  o     W  o  r  l   d
                 ╚════════════╝
Result: "lo W"   (space is included!)

💡 substr(start, length) — NOT substr(start, end)!
   Second parameter is LENGTH, not ending index!
````

---

## 14. Find — Searching Inside a String

`.find()` searches for a character or substring and returns its **position** (index). Returns `string::npos` if not found.

### Code Example

````cpp
string s = "Hello World Hello";

// Find a character
size_t pos1 = s.find('W');          // 6
size_t pos2 = s.find('z');          // string::npos (not found)

// Find a substring
size_t pos3 = s.find("World");     // 6
size_t pos4 = s.find("Hello");     // 0 (first occurrence)

// Find starting from a position
size_t pos5 = s.find("Hello", 1);  // 12 (second occurrence)

// Check if found
if (s.find("World") != string::npos) {
    cout << "Found!" << endl;
}
````

### Visualization

````
s = "Hello World Hello"

Index: [0][1][2][3][4][5][6][7][8][9][10][11][12][13][14][15][16]
        H  e  l  l  o     W  o  r  l   d      H   e   l   l   o

═══════════════════════════════════════════
s.find('W');
Scan from left → right:
H? No. e? No. l? No. l? No. o? No. ' '? No. W? YES! ✅
Position: 6

═══════════════════════════════════════════
s.find("Hello");
Scan for pattern "Hello":
Position 0: H-e-l-l-o → MATCH! ✅
Position: 0  (returns FIRST occurrence)

═══════════════════════════════════════════
s.find("Hello", 1);   ← Start searching from index 1
Skip index 0, scan from index 1:
Position 12: H-e-l-l-o → MATCH! ✅
Position: 12  (second occurrence)

═══════════════════════════════════════════
s.find('z');
Scan entire string... not found.
Returns: string::npos (which is a very large number, typically 18446744073709551615)

💡 Always check: if (pos != string::npos) before using the result!
````

---

## 15. Erase — Removing Characters

### Erase by Position and Length

````cpp
string s = "Hello World";

s.erase(5, 6);         // Erase 6 chars starting at index 5
cout << s << endl;      // "Hello"
````

### Erase a Single Character

````cpp
string s = "ABCDE";

s.erase(s.begin() + 2);   // Erase character at index 2 ('C')
cout << s << endl;          // "ABDE"
````

### Erase a Range

````cpp
string s = "ABCDE";

s.erase(s.begin() + 1, s.begin() + 3);   // Erase index 1 to 2
cout << s << endl;                         // "ADE"
````

### Visualization

````
═══════════════════════════════════════
s = "Hello World"
s.erase(5, 6);     start=5, length=6

Index: [0][1][2][3][4][5][6][7][8][9][10]
        H  e  l  l  o     W  o  r  l   d
                       ╚══════════════╝
                       ERASE these 6 chars

Result:
┌───┬───┬───┬───┬───┐
│ H │ e │ l │ l │ o │     s = "Hello"
└───┴───┴───┴───┴───┘

═══════════════════════════════════════
s = "ABCDE"
s.erase(s.begin() + 2);   ← Erase at index 2

┌─────┬─────┬─────┬─────┬─────┐
│ 'A' │ 'B' │ 'C' │ 'D' │ 'E' │
└─────┴─────┴─────┴─────┴─────┘
               ↑
          DELETE 'C'

Result:
┌─────┬─────┬─────┬─────┐
│ 'A' │ 'B' │ 'D' │ 'E' │     s = "ABDE"
└─────┴─────┴─────┴─────┘

═══════════════════════════════════════
s = "ABCDE"
s.erase(s.begin() + 1, s.begin() + 3);   [1, 3)

┌─────┬─────┬─────┬─────┬─────┐
│ 'A' │ 'B' │ 'C' │ 'D' │ 'E' │
└─────┴─────┴─────┴─────┴─────┘
        ╚═══════╝
        DELETE 'B','C' (index 1 and 2)

Result:
┌─────┬─────┬─────┐
│ 'A' │ 'D' │ 'E' │     s = "ADE"
└─────┴─────┴─────┘
````

---

## 16. Insert — Adding Characters at a Position

### Code Example

````cpp
string s = "Hello World";

s.insert(5, " Beautiful");
cout << s << endl;   // "Hello Beautiful World"

// Insert a character
s.insert(s.begin(), '!');
cout << s << endl;   // "!Hello Beautiful World"
````

### Visualization

````
s = "Hello World"

s.insert(5, " Beautiful");    ← Insert at index 5

Before:
┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ H │ e │ l │ l │ o │   │ W │ o │ r │ l │ d │
├───┼───┼───┼───┼───┤   ├───┼───┼───┼───┼───┤
│[0]│[1]│[2]│[3]│[4]│   │[6]│[7]│[8]│[9]│[10]│
└───┴───┴───┴───┴───┘   └───┴───┴───┴───┴───┘
                     ↑
              Insert " Beautiful" HERE

After:
"Hello Beautiful World"
┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ H │ e │ l │ l │ o │   │ B │ e │ a │ u │ t │ i │ f │ u │ l │   │ W │ o │ r │ l │ d │
└───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘
│←─original─→│←──────inserted──────→│              │←───original───→│
````

---

## 17. Replace — Replacing Part of a String

`.replace(start, length, new_string)` replaces a portion of the string.

### Code Example

````cpp
string s = "Hello World";

s.replace(6, 5, "C++");          // Replace "World" with "C++"
cout << s << endl;                // "Hello C++"
````

### Visualization

````
s = "Hello World"

s.replace(6, 5, "C++");    start=6, length=5, replacement="C++"

Before:
┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ H │ e │ l │ l │ o │   │ W │ o │ r │ l │ d │
└───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘
                          ╚═══════════════╝
                          Replace these 5 chars
                          with "C++"

After:
┌───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ H │ e │ l │ l │ o │   │ C │ + │ + │
└───┴───┴───┴───┴───┴───┴───┴───┴───┘

s = "Hello C++"

💡 The replacement string can be shorter or longer than
   the portion being replaced — string resizes automatically!
````

---

## 18. Character Type Checking (Upper/Lower/Digit)

These are **C-style** functions but extremely useful with STL strings.

### Functions

````cpp
#include <cctype>   // or included via bits/stdc++.h

char c = 'A';

isupper(c)   // Returns non-zero if c is uppercase (A-Z)
islower(c)   // Returns non-zero if c is lowercase (a-z)
isalpha(c)   // Returns non-zero if c is a letter (A-Z or a-z)
isdigit(c)   // Returns non-zero if c is a digit (0-9)
isalnum(c)   // Returns non-zero if c is alphanumeric
isspace(c)   // Returns non-zero if c is whitespace (space, tab, newline)
````

### Code Example

````cpp
string s = "Hello World 123";

for (char c : s) {
    if (isupper(c))      cout << c << " is UPPERCASE" << endl;
    else if (islower(c)) cout << c << " is lowercase" << endl;
    else if (isdigit(c)) cout << c << " is a digit" << endl;
    else if (isspace(c)) cout << c << " is a space" << endl;
}
````

### Visualization: Character Classification

````
String: "Ab3 Z"

Character │ isupper │ islower │ isdigit │ isspace │ isalpha │ isalnum
──────────┼─────────┼─────────┼─────────┼─────────┼─────────┼────────
   'A'    │   ✅    │   ❌    │   ❌    │   ❌    │   ✅    │   ✅
   'b'    │   ❌    │   ✅    │   ❌    │   ❌    │   ✅    │   ✅
   '3'    │   ❌    │   ❌    │   ✅    │   ❌    │   ❌    │   ✅
   ' '    │   ❌    │   ❌    │   ❌    │   ✅    │   ❌    │   ❌
   'Z'    │   ✅    │   ❌    │   ❌    │   ❌    │   ✅    │   ✅

ASCII Layout:
┌──────────────────────────────────────────────────────────────┐
│ 0-31: Control chars  │ 32: Space  │ 33-47: Symbols          │
│ 48-57: Digits (0-9)  │ 58-64: Symbols                       │
│ 65-90: UPPERCASE (A-Z) │ 91-96: Symbols                     │
│ 97-122: lowercase (a-z) │ 123-127: Symbols                  │
└──────────────────────────────────────────────────────────────┘
````

---

## 19. Case Conversion (toupper / tolower)

### Convert Single Character

````cpp
char c = 'a';
char upper = toupper(c);    // 'A'

char d = 'A';
char lower = tolower(d);    // 'a'
````

### Convert Entire String

````cpp
string s = "Hello World";

// Convert to UPPERCASE
for (int i = 0; i < s.size(); i++) {
    s[i] = toupper(s[i]);
}
cout << s << endl;   // "HELLO WORLD"

// Convert to lowercase
for (char& c : s) {       // Note: use reference (&) to modify
    c = tolower(c);
}
cout << s << endl;   // "hello world"
````

### Visualization

````
s = "Hello World"

Convert to UPPERCASE:
┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ H │ e │ l │ l │ o │   │ W │ o │ r │ l │ d │
└───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘
  ↓   ↓   ↓   ↓   ↓   ↓   ↓   ↓   ↓   ↓   ↓
  H   E   L   L   O   ' ' W   O   R   L   D
┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ H │ E │ L │ L │ O │   │ W │ O │ R │ L │ D │
└───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘

💡 toupper('e') = 'E'  (adds 65-97 = subtracts 32)
💡 toupper(' ') = ' '  (non-letter chars unchanged!)
💡 toupper('H') = 'H'  (already uppercase, no change)

The math behind it:
  'a' = 97,  'A' = 65  → difference = 32
  'b' = 98,  'B' = 66  → difference = 32
  
  To convert lowercase → uppercase: subtract 32
  To convert uppercase → lowercase: add 32
  
  But just use toupper()/tolower() — they handle edge cases!
````

---

## 20. Clear & Empty

### clear() — Remove All Characters

````cpp
string s = "Hello";
s.clear();
cout << s.size() << endl;   // 0
cout << s << endl;          // (empty)
````

### empty() — Check If String Is Empty

````cpp
string s = "";

if (s.empty()) {
    cout << "String is empty!" << endl;      // This prints
}

s = "Hi";
if (s.empty()) {
    cout << "Empty" << endl;
} else {
    cout << "Not empty" << endl;              // This prints
}
````

````
s.clear();     → s becomes ""
s.empty();     → returns true if s == "", false otherwise

💡 s.empty() is equivalent to (s.size() == 0)
   but .empty() is more readable
````

---

## 21. String as a Vector of Characters

Strings behave almost **identically** to `vector<char>`. All the vector operations work!

### Side-by-Side Comparison

````cpp
// Vector of characters         // String
vector<char> v;                  string s;
v.push_back('A');                s.push_back('A');     // or s += 'A';
v.pop_back();                    s.pop_back();
v.size();                        s.size();
v[0];                            s[0];
v.front();                       s.front();
v.back();                        s.back();
v.clear();                       s.clear();
v.empty();                       s.empty();
sort(v.begin(), v.end());        sort(s.begin(), s.end());
reverse(v.begin(), v.end());     reverse(s.begin(), s.end());
````

### vector<string> — Vector of Strings

````cpp
vector<string> names;

names.push_back("Alice");
names.push_back("Bob");
names.push_back("Charlie");

for (string name : names) {
    cout << name << endl;
}
// Alice
// Bob
// Charlie

// Sort names alphabetically
sort(names.begin(), names.end());
// Alice, Bob, Charlie (already sorted!)
````

### Visualization

````
vector<string> names = {"Charlie", "Alice", "Bob"};

┌─────────────┐
│   names      │
│  ┌─────────┐ │
│  │ [0]     │─┼──→ "Charlie"  ┌─C─┬─h─┬─a─┬─r─┬─l─┬─i─┬─e─┐
│  ├─────────┤ │                └───┴───┴───┴───┴───┴───┴───┘
│  │ [1]     │─┼──→ "Alice"    ┌─A─┬─l─┬─i─┬─c─┬─e─┐
│  ├─────────┤ │                └───┴───┴───┴───┴───┘
│  │ [2]     │─┼──→ "Bob"      ┌─B─┬─o─┬─b─┐
│  └─────────┘ │                └───┴───┴───┘
└─────────────┘

After sort(names.begin(), names.end()):
  [0] → "Alice"
  [1] → "Bob"
  [2] → "Charlie"
  (sorted lexicographically)
````

---

## 22. Convert String to Integer & Vice Versa

### String to Integer

````cpp
string num_str = "12345";

// Method 1: stoi() — String TO Integer
int num = stoi(num_str);       // 12345

// Other conversions:
long l = stol(num_str);        // String to long
long long ll = stoll(num_str); // String to long long
float f = stof("3.14");       // String to float
double d = stod("3.14159");   // String to double
````

### Integer to String

````cpp
int num = 12345;

// Method: to_string()
string s = to_string(num);    // "12345"

double pi = 3.14159;
string pi_str = to_string(pi); // "3.141590"
````

### Visualization

````
String to Integer:
"12345"  ──stoi()──→  12345
┌───┬───┬───┬───┬───┐        ┌─────────┐
│'1'│'2'│'3'│'4'│'5'│  ────→ │  12345  │
└───┴───┴───┴───┴───┘        └─────────┘
 characters                    number

Integer to String:
12345  ──to_string()──→  "12345"
┌─────────┐              ┌───┬───┬───┬───┬───┐
│  12345  │  ──────────→ │'1'│'2'│'3'│'4'│'5'│
└─────────┘              └───┴───┴───┴───┴───┘
 number                   characters

💡 Useful for problems where you need to manipulate
   individual digits of a number!
````

---

## 23. Useful String Functions — Quick Reference

| Function | What It Does | Example | Result |
|----------|-------------|---------|--------|
| `s.size()` / `s.length()` | Number of characters | `"Hello".size()` | `5` |
| `s.empty()` | Check if empty | `"".empty()` | `true` |
| `s.clear()` | Remove all chars | `s.clear()` | `""` |
| `s.push_back(c)` | Add char at end | `s.push_back('!')` | `"Hello!"` |
| `s.pop_back()` | Remove last char | `"Hello".pop_back()` | `"Hell"` |
| `s.front()` | First character | `"Hello".front()` | `'H'` |
| `s.back()` | Last character | `"Hello".back()` | `'o'` |
| `s[i]` | Access char at index | `"Hello"[1]` | `'e'` |
| `s.at(i)` | Safe access at index | `"Hello".at(1)` | `'e'` |
| `s.substr(pos, len)` | Extract substring | `"Hello".substr(1,3)` | `"ell"` |
| `s.find(str)` | Find first occurrence | `"Hello".find("ll")` | `2` |
| `s.find(str, pos)` | Find from position | `"abcabc".find("abc",1)` | `3` |
| `s.erase(pos, len)` | Remove portion | `"Hello".erase(1,3)` | `"Ho"` |
| `s.insert(pos, str)` | Insert at position | `"Ho".insert(1,"ell")` | `"Hello"` |
| `s.replace(pos,len,str)` | Replace portion | `"Hello".replace(0,5,"Hi")` | `"Hi"` |
| `s.append(str)` | Add string at end | `"Hello".append("!")` | `"Hello!"` |
| `s + t` | Concatenate | `"Hi" + " World"` | `"Hi World"` |
| `s == t` | Compare equal | `"abc" == "abc"` | `true` |
| `s < t` | Lexicographic less | `"abc" < "abd"` | `true` |
| `stoi(s)` | String → int | `stoi("123")` | `123` |
| `to_string(n)` | Int → string | `to_string(123)` | `"123"` |

---

## 24. Practice Problems & Tips

### ✅ Essential String Problems

| # | Problem | Key Concept |
|---|---------|------------|
| 1 | Reverse a string | `reverse()` or manual swap |
| 2 | Check if palindrome | Compare `s` with `reverse(s)` |
| 3 | Count vowels/consonants | Character checking with loop |
| 4 | Convert uppercase ↔ lowercase | `toupper()`, `tolower()` |
| 5 | Remove all spaces from string | `erase` + `find` or remove-erase idiom |
| 6 | Find first non-repeating character | Frequency array |
| 7 | Check if two strings are anagrams | Sort both and compare |
| 8 | Longest common prefix | Character-by-character comparison |
| 9 | Count words in a sentence | Count spaces + 1, or use stringstream |
| 10 | String compression ("aabccc" → "a2b1c3") | Loop with counting |

### Remove a Specific Character from String

````cpp
// Remove all 'a' characters from string
string s = "abracadabra";

// Method: erase-remove idiom
s.erase(remove(s.begin(), s.end(), 'a'), s.end());
cout << s << endl;   // "brcdbr"
````

````
s = "abracadabra"

remove() moves non-'a' chars to front:
┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ a │ b │ r │ a │ c │ a │ d │ a │ b │ r │ a │
└───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘
  ↓
┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ b │ r │ c │ d │ b │ r │ ? │ ? │ ? │ ? │ ? │
└───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘
│←── valid ──────→│←── garbage ────────────→│
                  ↑
            remove() returns iterator here

erase() then removes from that point to end:
┌───┬───┬───┬───┬───┬───┐
│ b │ r │ c │ d │ b │ r │     s = "brcdbr"
└───┴───┴───┴───┴───┴───┘
````

### 💡 Important Tips

````
TIP 1: cin >> s reads only ONE WORD
       Use getline(cin, s) for full line with spaces

TIP 2: After cin >>, always use cin.ignore() before getline()

TIP 3: String comparison is CASE-SENSITIVE
       "Apple" != "apple"
       "Apple" < "apple" (uppercase < lowercase)

TIP 4: s.find() returns string::npos if not found
       ALWAYS check before using the result

TIP 5: substr(pos, LENGTH) — second param is LENGTH, not end index!

TIP 6: For character-level operations, use single quotes: 'A'
       For string operations, use double quotes: "A"

TIP 7: s += 'c' is same as s.push_back('c') — both add one char

TIP 8: Use range-based for with & to MODIFY characters:
       for (char& c : s) c = toupper(c);   ← modifies original
       for (char c : s)  ...               ← works on copy

TIP 9: Sorting a string sorts its characters by ASCII value
       Uppercase letters come BEFORE lowercase

TIP 10: A string is essentially a vector<char> with extra features
        All vector operations work on strings too!
````

---

## 25. Complete Cheat Sheet

````cpp
// ═══════════════════════════════════════════════════════
//         COMPLETE STL STRING CHEAT SHEET
// ═══════════════════════════════════════════════════════

#include <bits/stdc++.h>
using namespace std;

int main() {
    
    // ─── DECLARATION ─────────────────────────────────
    string s;                          // empty ""
    string s2 = "Hello";              // "Hello"
    string s3("World");               // "World"
    string s4(5, 'A');                // "AAAAA"
    string s5 = s2;                   // copy "Hello"
    
    // ─── INPUT ───────────────────────────────────────
    cin >> s;                          // single word (stops at space)
    getline(cin, s);                   // full line (with spaces)
    // After cin >>, use cin.ignore() before getline()!
    
    // ─── OUTPUT ──────────────────────────────────────
    cout << s << endl;
    
    // ─── ACCESS ──────────────────────────────────────
    s[0];                              // first char (no bounds check)
    s.at(0);                           // first char (bounds check)
    s.front();                         // first char
    s.back();                          // last char
    
    // ─── SIZE ────────────────────────────────────────
    s.size();                          // number of characters
    s.length();                        // same as size()
    s.empty();                         // true if size == 0
    
    // ─── ADD / REMOVE ────────────────────────────────
    s.push_back('!');                  // add char at end
    s.pop_back();                      // remove last char
    s += "World";                      // concatenate string
    s += 'X';                          // add single char
    s.append(" more");                 // concatenate
    s.insert(5, " Beautiful");         // insert at position
    s.erase(5, 6);                     // erase 6 chars from index 5
    s.erase(s.begin() + 2);            // erase char at index 2
    s.clear();                         // remove all characters
    
    // ─── SEARCH ──────────────────────────────────────
    size_t pos = s.find("World");      // find substring
    if (pos != string::npos) { }       // check if found
    s.find('W');                       // find character
    s.find("Hello", 5);               // find starting from index 5
    
    // ─── EXTRACT ─────────────────────────────────────
    string sub = s.substr(0, 5);       // substring (pos, length)
    
    // ─── REPLACE ─────────────────────────────────────
    s.replace(6, 5, "C++");            // replace at pos, len, with str
    
    // ─── COMPARE ─────────────────────────────────────
    if (s == "Hello") { }              // equal
    if (s != "Hello") { }              // not equal
    if (s < "World")  { }              // lexicographic less
    if (s > "Apple")  { }              // lexicographic greater
    
    // ─── SORT & REVERSE ──────────────────────────────
    sort(s.begin(), s.end());          // sort chars ascending
    sort(s.begin(), s.end(), greater<char>());  // descending
    reverse(s.begin(), s.end());       // reverse string
    
    // ─── CHARACTER FUNCTIONS ─────────────────────────
    isupper('A');                       // is uppercase?
    islower('a');                       // is lowercase?
    isdigit('5');                       // is digit?
    isalpha('A');                       // is letter?
    isalnum('A');                       // is letter or digit?
    isspace(' ');                       // is whitespace?
    toupper('a');                       // → 'A'
    tolower('A');                       // → 'a'
    
    // ─── CONVERSION ──────────────────────────────────
    int n = stoi("123");               // string → int
    string ns = to_string(123);        // int → string
    long l = stol("123456789");        // string → long
    double d = stod("3.14");           // string → double
    
    // ─── ITERATE ─────────────────────────────────────
    for (int i = 0; i < s.size(); i++) cout << s[i];    // index
    for (char c : s) cout << c;                          // range
    for (auto it = s.begin(); it != s.end(); it++)       // iterator
        cout << *it;
    for (auto it = s.rbegin(); it != s.rend(); it++)     // reverse
        cout << *it;
    
    // ─── VECTOR OF STRINGS ──────────────────────────
    vector<string> words;
    words.push_back("Hello");
    words.push_back("World");
    sort(words.begin(), words.end());   // sort alphabetically
    
    // ─── REMOVE SPECIFIC CHAR ───────────────────────
    s.erase(remove(s.begin(), s.end(), 'a'), s.end());   // remove all 'a'
    
    return 0;
}
````

---

## 📊 Time Complexity Summary

| Operation | Time Complexity | Notes |
|-----------|:--------------:|-------|
| `s[i]` / `s.at(i)` | **O(1)** | Random access |
| `s.front()` / `s.back()` | **O(1)** | Direct access |
| `s.size()` / `s.length()` | **O(1)** | Stored internally |
| `s.empty()` | **O(1)** | Checks size |
| `s.push_back(c)` | **O(1)** amortized | Like vector |
| `s.pop_back()` | **O(1)** | Always constant |
| `s += t` (concatenation) | **O(M)** | M = length of t |
| `s + t` | **O(N+M)** | Creates new string |
| `s.find(t)` | **O(N×M)** | Naive search |
| `s.substr(pos, len)` | **O(len)** | Creates new string |
| `s.insert(pos, t)` | **O(N+M)** | Shifts existing chars |
| `s.erase(pos, len)` | **O(N)** | Shifts remaining chars |
| `s.replace(pos,len,t)` | **O(N+M)** | Erase + insert |
| `sort(s.begin(), s.end())` | **O(N log N)** | Sort characters |
| `reverse(s.begin(), s.end())` | **O(N)** | Swap from ends |
| `s == t` | **O(N)** | Character by character |
| `s < t` | **O(N)** | Lexicographic comparison |
| `stoi(s)` / `to_string(n)` | **O(N)** | N = number of digits |

---

## 🎯 Key Takeaways

| Concept | Key Point |
|---------|-----------|
| **string** | Dynamic array of chars — like `vector<char>` with extras |
| **cin vs getline** | `cin` stops at space; `getline` reads full line |
| **cin.ignore()** | Must use after `cin >>` before `getline()` |
| **Indexing** | `s[i]`, `s.at(i)`, `s.front()`, `s.back()` |
| **Concatenation** | `+` creates new; `+=` modifies in-place (faster) |
| **Comparison** | Lexicographic, case-sensitive (`'A' < 'a'`) |
| **substr** | `.substr(pos, LENGTH)` — second param is length! |
| **find** | Returns `string::npos` if not found — always check! |
| **Case conversion** | `toupper()`, `tolower()` on individual chars |
| **Sort/Reverse** | Same as vector: `sort()`, `reverse()` from `<algorithm>` |
| **Convert** | `stoi()` string→int, `to_string()` int→string |
| **Memory** | Strings grow dynamically like vectors (doubling strategy) |

---

> ✅ **You now have comprehensive notes covering almost everything about STL Strings!** Practice the string problems listed in Section 24 to solidify your understanding. Strings are one of the most frequently tested topics in competitive programming and interviews! 🚀
