# Python Mastery — Complete Engineering Curriculum
## Zero to Senior Software Engineer

> **Covers:** Python Basics · Data Types · OOP · Modules · File I/O · Exceptions · Decorators · Generators · Async · Testing · APIs · Performance · Internals · Design Patterns · Scalable Architecture
> **Track:** Software Engineering Career Path | Beginner → Senior Engineer
> **Based on:** Official Python Documentation — https://docs.python.org/3/

---

## How to Use This Document

- Work through every lesson in order — each concept builds on the previous
- Type every code example yourself — do not copy-paste — muscle memory matters
- Complete every exercise before moving on — struggling is part of learning
- When you hit an error, read the full traceback — it tells you exactly what went wrong
- The best Python engineer you know still Googles things — learn how to read docs

---

## Table of Contents

### PHASE 1 — Foundations (Beginner)
- [Lesson 1 — Python Basics and Environment Setup](#lesson-1--python-basics-and-environment-setup)
- [Lesson 2 — Variables and Data Types](#lesson-2--variables-and-data-types)
- [Lesson 3 — Strings — The Most Used Data Type](#lesson-3--strings--the-most-used-data-type)
- [Lesson 4 — Numbers and Operators](#lesson-4--numbers-and-operators)
- [Lesson 5 — Lists — Ordered, Mutable Sequences](#lesson-5--lists--ordered-mutable-sequences)
- [Lesson 6 — Tuples, Sets, and Dictionaries](#lesson-6--tuples-sets-and-dictionaries)
- [Lesson 7 — Conditional Statements](#lesson-7--conditional-statements)
- [Lesson 8 — Loops](#lesson-8--loops)
- [Lesson 9 — Functions](#lesson-9--functions)
- [Lesson 10 — Practice Project — CLI Calculator](#lesson-10--practice-project--cli-calculator)

### PHASE 2 — Intermediate
- [Lesson 11 — Modules and Packages](#lesson-11--modules-and-packages)
- [Lesson 12 — File Handling](#lesson-12--file-handling)
- [Lesson 13 — Exception Handling](#lesson-13--exception-handling)
- [Lesson 14 — Object-Oriented Programming — Classes](#lesson-14--object-oriented-programming--classes)
- [Lesson 15 — Inheritance and Polymorphism](#lesson-15--inheritance-and-polymorphism)
- [Lesson 16 — Decorators](#lesson-16--decorators)
- [Lesson 17 — Iterators and Generators](#lesson-17--iterators-and-generators)
- [Lesson 18 — Practice Project — Contact Book App](#lesson-18--practice-project--contact-book-app)

### PHASE 3 — Advanced
- [Lesson 19 — Multithreading and Multiprocessing](#lesson-19--multithreading-and-multiprocessing)
- [Lesson 20 — Async Programming](#lesson-20--async-programming)
- [Lesson 21 — Logging](#lesson-21--logging)
- [Lesson 22 — Testing with PyTest](#lesson-22--testing-with-pytest)
- [Lesson 23 — REST APIs with FastAPI](#lesson-23--rest-apis-with-fastapi)
- [Lesson 24 — Performance Optimisation](#lesson-24--performance-optimisation)
- [Lesson 25 — Practice Project — REST API with Tests](#lesson-25--practice-project--rest-api-with-tests)

### PHASE 4 — Expert Level
- [Lesson 26 — Python Internals and Memory Management](#lesson-26--python-internals-and-memory-management)
- [Lesson 27 — Metaclasses](#lesson-27--metaclasses)
- [Lesson 28 — Design Patterns in Python](#lesson-28--design-patterns-in-python)
- [Lesson 29 — Scalable Python Architecture](#lesson-29--scalable-python-architecture)
- [Lesson 30 — Debugging Complex Applications](#lesson-30--debugging-complex-applications)
- [Lesson 31 — Interview Preparation — Python Edition](#lesson-31--interview-preparation--python-edition)

---

---

# PHASE 1 — FOUNDATIONS
## Python Beginner Level

---

## Lesson 1 — Python Basics and Environment Setup

> **Level:** Absolute Beginner
> **Goal:** Install Python, understand what it is, write your first program

---

### 1.1 What is Python?

Python is a high-level, interpreted programming language created by Guido van Rossum in 1991. "High-level" means it reads like English. "Interpreted" means Python runs your code line by line — you don't need to compile it first.

**Why Python?**
- Readable — code that looks almost like plain English
- Versatile — web development, data science, automation, AI/ML, scripting
- Massive ecosystem — over 400,000 packages on PyPI
- Dominant in data science, AI/ML (NumPy, Pandas, TensorFlow, PyTorch)
- Strong in backend web development (Django, FastAPI, Flask)
- The most-taught first language — vast learning resources

**Python in the real world:**
- Instagram's backend runs on Django (Python)
- Google uses Python extensively for tooling and services
- Netflix uses Python for recommendation systems and tooling
- NASA uses Python for scientific computing
- Every major company's data science team uses Python

---

### 1.2 Installing Python

**macOS:**
```bash
# Check if Python is already installed
python3 --version

# Install via Homebrew (recommended)
brew install python3

# Verify
python3 --version     # Should show Python 3.11+ or 3.12+
pip3 --version        # Package manager
```

**Ubuntu / Debian Linux:**
```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv

# Verify
python3 --version
pip3 --version
```

**Windows:**
```
1. Go to https://python.org/downloads/
2. Download Python 3.12.x (latest stable)
3. Run installer — CHECK "Add Python to PATH"
4. Verify in PowerShell or Command Prompt:
   python --version
   pip --version
```

---

### 1.3 The Python Interpreter — Your Interactive Sandbox

The Python interpreter lets you run Python code interactively, one line at a time. Perfect for experimenting.

```bash
# Start the interpreter
python3

# You'll see the prompt:
# Python 3.12.0 (...)
# >>>
```

```python
# Try these in the interpreter:
>>> 2 + 2
4
>>> "Hello, World!"
'Hello, World!'
>>> print("My name is Python")
My name is Python
>>> 10 / 3
3.3333333333333335
>>> 10 // 3
3
>>> exit()   # Exit the interpreter
```

> **The REPL (Read-Eval-Print Loop):** The interpreter reads your input, evaluates it, prints the result, and loops back. Use it constantly while learning — test small ideas before putting them in a file.

---

### 1.4 Virtual Environments — The Right Way to Work

A virtual environment is an isolated Python installation for each project. This means Project A can use Django 4.2 and Project B can use Django 3.2 — no conflicts.

```bash
# Create a virtual environment named 'venv' in the current directory
python3 -m venv venv

# Activate it
# macOS / Linux:
source venv/bin/activate

# Windows:
venv\Scripts\activate

# Your prompt changes to show the environment is active:
# (venv) $

# Install packages INTO this environment only
pip install requests

# See what's installed
pip list

# Save dependencies to a file (share with others)
pip freeze > requirements.txt

# Install from requirements file (on another machine)
pip install -r requirements.txt

# Deactivate when done
deactivate
```

> **Golden Rule:** Every Python project gets its own virtual environment. Never install packages into the system Python. This becomes critical when working with teams and deployment.

---

### 1.5 Your First Python File

```bash
# Create a file
touch hello.py
```

```python
# hello.py
print("Hello, World!")
print("My name is Python")
print("I am", 3.12, "years into learning Python")
```

```bash
# Run it
python3 hello.py

# Output:
# Hello, World!
# My name is Python
# I am 3.12 years into learning Python
```

---

### 1.6 Code Editors

**VS Code (recommended):**
```bash
# Install VS Code from https://code.visualstudio.com/
# Install the Python extension (Microsoft)
# Install Pylint or Ruff for linting
# The Python extension provides: syntax highlighting, autocomplete, debugging
```

**PyCharm:**
- Full-featured Python IDE
- Community edition is free
- Best for large projects

---

### 1.7 Python Style Guide — PEP 8

PEP 8 is Python's official style guide. Professional Python code follows PEP 8.

```python
# Good PEP 8 style
first_name = "Alice"           # snake_case for variables
MAX_CONNECTIONS = 100          # UPPER_SNAKE_CASE for constants
class UserAccount:             # PascalCase for classes
    pass

def calculate_total(price, tax):  # snake_case for functions
    return price + tax

# Bad style
FirstName = "Alice"            # Don't use PascalCase for variables
maxConnections = 100           # Don't use camelCase
def CalculateTotal(p, t):      # Don't use PascalCase for functions
    return p + t
```

---

### 1.8 Hands-On Lab 1

```bash
mkdir python-mastery && cd python-mastery
python3 -m venv venv
source venv/bin/activate   # or venv\Scripts\activate on Windows
```

Create `lab1.py` and type each line:

```python
# lab1.py — My first Python program

# 1. Print statements
print("=== Python Lab 1 ===")
print("Hello from Python!")

# 2. Basic arithmetic
print(10 + 5)
print(10 - 3)
print(4 * 7)
print(15 / 4)
print(15 // 4)   # Floor division
print(15 % 4)    # Modulo (remainder)
print(2 ** 8)    # Power (2 to the power of 8)

# 3. Comments
# This is a single-line comment
# Python ignores everything after the # symbol

# 4. The print function can take multiple values
print("I am", 25, "years old")
print("Pi is approximately", 3.14159)
```

```bash
python3 lab1.py
```

**Exercise:** Modify the program to calculate and print the area of a rectangle with width 12 and height 8. Then calculate the perimeter.

---

### 1.9 Practice Questions — Lesson 1

**Q1.** What is the difference between `python3 script.py` and opening the Python interpreter?

<details>
<summary>Answer</summary>

`python3 script.py` runs a file from top to bottom and exits. The interpreter (REPL) is interactive — you type one expression at a time and see the result immediately. Use scripts for complete programs. Use the interpreter for experimenting, testing small ideas, and quick calculations.

</details>

---

**Q2.** Why do we use virtual environments instead of installing packages globally?

<details>
<summary>Answer</summary>

Different projects often need different versions of the same library. If you install everything globally, Project A needing requests==2.28 and Project B needing requests==2.31 will conflict. Virtual environments give each project its own isolated Python and packages. It also means you can delete a project's environment without affecting anything else on your system.

</details>

---

---

## Lesson 2 — Variables and Data Types

> **Level:** Beginner
> **Goal:** Store and work with different kinds of data

---

### 2.1 Variables — Named Storage

A variable is a name that refers to a value stored in memory. Unlike some languages, Python doesn't require you to declare the type — Python figures it out.

```python
# Creating variables
name = "Alice"        # String
age = 28              # Integer
height = 1.75         # Float
is_student = True     # Boolean

# Print them
print(name)
print(age)
print(height)
print(is_student)

# Check the type of any variable
print(type(name))       # <class 'str'>
print(type(age))        # <class 'int'>
print(type(height))     # <class 'float'>
print(type(is_student)) # <class 'bool'>
```

---

### 2.2 Python's Built-in Data Types

```python
# ─── NUMERIC TYPES ────────────────────────────────────────────────
integer_num = 42           # int — whole numbers
float_num = 3.14           # float — decimal numbers
complex_num = 3 + 4j       # complex — real + imaginary (used in scientific computing)

print(type(integer_num))   # <class 'int'>
print(type(float_num))     # <class 'float'>
print(type(complex_num))   # <class 'complex'>

# ─── TEXT TYPE ────────────────────────────────────────────────────
text = "Hello, World"      # str — sequence of characters

# ─── BOOLEAN TYPE ─────────────────────────────────────────────────
is_valid = True
is_empty = False
# Booleans are a subclass of int: True == 1, False == 0
print(True + True)         # 2
print(True * 5)            # 5

# ─── NONE TYPE ────────────────────────────────────────────────────
nothing = None             # NoneType — represents absence of value
print(type(nothing))       # <class 'NoneType'>
print(nothing is None)     # True  (use 'is' to check for None, not ==)

# ─── SEQUENCE TYPES ───────────────────────────────────────────────
my_list  = [1, 2, 3]      # list  — ordered, mutable
my_tuple = (1, 2, 3)      # tuple — ordered, immutable
my_range = range(5)        # range — sequence of numbers

# ─── MAPPING TYPE ─────────────────────────────────────────────────
my_dict = {"name": "Alice", "age": 28}  # dict — key-value pairs

# ─── SET TYPES ────────────────────────────────────────────────────
my_set      = {1, 2, 3}         # set — unordered, unique, mutable
my_frozenset = frozenset({1, 2}) # frozenset — immutable set
```

---

### 2.3 Dynamic Typing — Python's Superpower and Pitfall

Python is dynamically typed — a variable can change type during the program.

```python
x = 10          # x is an int
print(type(x))  # <class 'int'>

x = "hello"     # Now x is a str — no error!
print(type(x))  # <class 'str'>

x = [1, 2, 3]  # Now x is a list
print(type(x))  # <class 'list'>
```

> **This is powerful but dangerous.** In large codebases, you lose track of what type a variable holds. Python 3.5+ added **type hints** to solve this — we'll cover them later.

---

### 2.4 Type Conversion

```python
# Converting between types
age_str = "25"
age_int = int(age_str)      # "25" → 25
age_float = float(age_str)  # "25" → 25.0

price = 19.99
price_int = int(price)      # 19.99 → 19  (truncates, doesn't round)
price_str = str(price)      # 19.99 → "19.99"

# Explicit vs implicit conversion
result = 5 + 2.0            # int + float → Python automatically gives float
print(result)               # 7.0
print(type(result))         # <class 'float'>

# bool() — what evaluates to False?
print(bool(0))       # False
print(bool(""))      # False  (empty string)
print(bool([]))      # False  (empty list)
print(bool(None))    # False
print(bool(1))       # True
print(bool("hi"))    # True
print(bool([1]))     # True   (non-empty list)
```

---

### 2.5 Multiple Assignment

```python
# Assign the same value to multiple variables
x = y = z = 0
print(x, y, z)  # 0 0 0

# Unpack multiple values at once (tuple unpacking)
a, b, c = 1, 2, 3
print(a, b, c)  # 1 2 3

# Swap values — elegant Python idiom
x, y = 10, 20
x, y = y, x
print(x, y)   # 20 10

# Unpack with * (collect remaining items)
first, *rest = [1, 2, 3, 4, 5]
print(first)  # 1
print(rest)   # [2, 3, 4, 5]

head, *middle, last = [1, 2, 3, 4, 5]
print(head)   # 1
print(middle) # [2, 3, 4]
print(last)   # 5
```

---

### 2.6 Exercises — Lesson 2

**Exercise 1:** Create variables for a person's profile:
- name (string), age (integer), height in metres (float), is_employed (boolean)
- Print each with its type using `type()`
- Convert age to a string and print: "Alice is 28 years old"

**Exercise 2:** Given `x = 7` and `y = 3`, compute and print:
- Sum, difference, product, quotient (float), floor division, remainder, x to the power of y

**Exercise 3:** What does this print and why?
```python
a = "5"
b = 3
print(a * b)
print(int(a) + b)
```

<details>
<summary>Exercise 3 Answer</summary>

`a * b` where a is a string and b is an int: Python repeats the string b times → `"555"`
`int(a) + b` converts "5" to 5, then adds 3 → `8`

</details>

---

---

## Lesson 3 — Strings — The Most Used Data Type

> **Level:** Beginner → Intermediate
> **Goal:** Master string creation, indexing, slicing, and all key methods

---

### 3.1 Creating Strings

```python
# Four ways to create strings
single    = 'Hello'
double    = "World"
triple_s  = '''This spans
multiple lines'''
triple_d  = """Also spans
multiple lines"""

# String with special characters
path    = "C:\\Users\\Alice"     # Backslash must be escaped
path2   = r"C:\Users\Alice"      # Raw string — backslash not treated as escape
newline = "Line 1\nLine 2"       # \n = newline
tab     = "Column1\tColumn2"     # \t = tab

print(newline)
print(tab)
```

---

### 3.2 String Indexing and Slicing

```python
text = "Python"
#       012345   ← positive indices
#      -654321   ← negative indices

# Indexing — get one character
print(text[0])    # 'P'  (first character)
print(text[3])    # 'h'
print(text[-1])   # 'n'  (last character)
print(text[-2])   # 'o'  (second from last)

# Slicing — get a substring
# text[start:stop:step]  (stop is exclusive)
print(text[0:3])   # 'Pyt'   (chars 0, 1, 2)
print(text[2:])    # 'thon'  (from index 2 to end)
print(text[:4])    # 'Pyth'  (from start to index 3)
print(text[::2])   # 'Pto'   (every 2nd character)
print(text[::-1])  # 'nohtyP' (reversed!)
```

---

### 3.3 String Methods — The Complete Toolkit

```python
text = "  Hello, World!  "

# ─── CASE ──────────────────────────────────────────────────────────
print(text.upper())       # "  HELLO, WORLD!  "
print(text.lower())       # "  hello, world!  "
print(text.title())       # "  Hello, World!  " (capitalise each word)
print(text.capitalize())  # "  hello, world!  " (only first char of string)
print(text.swapcase())    # "  hELLO, wORLD!  "

# ─── WHITESPACE ────────────────────────────────────────────────────
print(text.strip())       # "Hello, World!"  (removes leading/trailing spaces)
print(text.lstrip())      # "Hello, World!  "
print(text.rstrip())      # "  Hello, World!"

# ─── SEARCH ────────────────────────────────────────────────────────
s = "the cat sat on the mat"
print(s.find("cat"))        # 4   (index of first occurrence, -1 if not found)
print(s.rfind("at"))        # 20  (index of last occurrence)
print(s.index("sat"))       # 8   (like find but raises ValueError if not found)
print(s.count("at"))        # 3   (count occurrences)
print(s.startswith("the"))  # True
print(s.endswith("mat"))    # True
print("cat" in s)           # True (membership test)

# ─── REPLACE AND SPLIT ─────────────────────────────────────────────
print(s.replace("cat", "dog"))    # "the dog sat on the mat"
print(s.replace("at", "AT", 2))   # Replace only first 2 occurrences

words = s.split()           # Split on whitespace → ["the", "cat", ...]
print(words)
csv = "Alice,28,Engineer"
parts = csv.split(",")      # Split on comma
print(parts)                # ["Alice", "28", "Engineer"]

# Join (opposite of split)
joined = " ".join(["Hello", "World"])
print(joined)               # "Hello World"
path = "/".join(["home", "alice", "documents"])
print(path)                 # "home/alice/documents"

# ─── CHECK ─────────────────────────────────────────────────────────
print("hello".isalpha())   # True  (only letters)
print("hello123".isalnum()) # True  (letters and digits)
print("12345".isdigit())   # True  (only digits)
print("  ".isspace())      # True  (only whitespace)
```

---

### 3.4 String Formatting — Three Ways

```python
name = "Alice"
age = 28
score = 95.678

# ─── METHOD 1: f-strings (Python 3.6+) — USE THIS ──────────────────
print(f"Name: {name}, Age: {age}")
print(f"Score: {score:.2f}")     # 2 decimal places → 95.68
print(f"Age: {age:05d}")         # Zero-pad to 5 digits → 00028
print(f"{'Alice':>10}")          # Right-align in 10 chars → "     Alice"
print(f"{'Alice':<10}")          # Left-align → "Alice     "
print(f"{'Alice':^10}")          # Centre → "  Alice   "
print(f"{1_000_000:,}")          # Thousands separator → 1,000,000
print(f"{0.75:.1%}")             # Percentage → 75.0%

# Expressions inside f-strings
print(f"3 squared is {3**2}")
print(f"Name length: {len(name)}")
print(f"Upper: {name.upper()}")

# ─── METHOD 2: .format() ────────────────────────────────────────────
print("Name: {}, Age: {}".format(name, age))
print("Name: {n}, Age: {a}".format(n=name, a=age))
print("Score: {:.2f}".format(score))

# ─── METHOD 3: % formatting (old — avoid in new code) ───────────────
print("Name: %s, Age: %d" % (name, age))
```

---

### 3.5 String Immutability

Strings in Python are immutable — you cannot change characters in place.

```python
name = "Alice"
# name[0] = "B"   ← This raises TypeError: 'str' object does not support item assignment

# To "modify" a string, create a new one
new_name = "B" + name[1:]
print(new_name)  # "Blice"

# Strings are also compared by value
s1 = "hello"
s2 = "hello"
print(s1 == s2)      # True  (same content)
print(s1 is s2)      # True  (CPython interns short strings — same object in memory)
```

---

### 3.6 Exercises — Lesson 3

**Exercise 1:** Given `sentence = "the quick brown fox jumps over the lazy dog"`:
- Capitalise the first letter of every word
- Count how many times "the" appears
- Replace "fox" with "cat"
- Reverse the entire string
- Check if it ends with "dog"

**Exercise 2:** Build a username generator. Given `full_name = "Alice Johnson"` and `birth_year = 1995`:
- Create username: first initial + last name + last 2 digits of birth year, all lowercase
- Expected output: `ajohnson95`

**Exercise 3:** Format this data as a table using f-strings:
```python
products = [("Apple", 1.20, 50), ("Banana", 0.50, 120), ("Cherry", 3.00, 30)]
# Print: Product     Price   Stock
#        Apple        1.20      50
#        Banana       0.50     120
#        Cherry       3.00      30
```

<details>
<summary>Exercise 2 Answer</summary>

```python
full_name = "Alice Johnson"
birth_year = 1995

parts = full_name.lower().split()
first_initial = parts[0][0]
last_name = parts[1]
year_suffix = str(birth_year)[-2:]
username = first_initial + last_name + year_suffix
print(username)  # ajohnson95
```

</details>

---

---

## Lesson 4 — Numbers and Operators

> **Level:** Beginner
> **Goal:** Master Python's numeric types and all operators

---

### 4.1 Integer — Unlimited Precision

```python
# Python integers have no size limit
big = 9999999999999999999999999999999999999999
print(big + 1)    # Works perfectly — no overflow

# Different bases
binary  = 0b1010   # Binary (base 2) → 10
octal   = 0o12     # Octal (base 8) → 10
hex_num = 0xA      # Hexadecimal (base 16) → 10
print(binary, octal, hex_num)  # 10 10 10

# Convert to different bases
print(bin(255))    # '0b11111111'
print(oct(255))    # '0o377'
print(hex(255))    # '0xff'

# Underscore as thousands separator (Python 3.6+)
million = 1_000_000
print(million)     # 1000000
```

---

### 4.2 Float — IEEE 754 Double Precision

```python
# Float precision issue — this is not Python's bug, it's IEEE 754
print(0.1 + 0.2)        # 0.30000000000000004 ← famous float imprecision

# Solution: use decimal for financial calculations
from decimal import Decimal
print(Decimal("0.1") + Decimal("0.2"))  # 0.3  (exact)

# Math module for numeric operations
import math
print(math.sqrt(16))     # 4.0
print(math.ceil(4.1))    # 5   (round up)
print(math.floor(4.9))   # 4   (round down)
print(round(4.567, 2))   # 4.57  (built-in round)
print(math.pi)           # 3.141592653589793
print(math.e)            # 2.718281828459045
print(abs(-42))          # 42   (absolute value)
```

---

### 4.3 All Python Operators

```python
# ─── ARITHMETIC ────────────────────────────────────────────────────
print(7 + 3)   # 10   addition
print(7 - 3)   # 4    subtraction
print(7 * 3)   # 21   multiplication
print(7 / 3)   # 2.333...  division (always returns float)
print(7 // 3)  # 2    floor division (returns int)
print(7 % 3)   # 1    modulo (remainder)
print(7 ** 3)  # 343  exponentiation

# ─── COMPARISON ────────────────────────────────────────────────────
print(7 == 7)  # True   equal to
print(7 != 3)  # True   not equal to
print(7 > 3)   # True   greater than
print(7 < 3)   # False  less than
print(7 >= 7)  # True   greater than or equal to
print(7 <= 3)  # False  less than or equal to

# Chained comparisons — Python supports this!
x = 5
print(1 < x < 10)      # True
print(1 < x and x < 10)  # Same result, less readable

# ─── LOGICAL ───────────────────────────────────────────────────────
print(True and False)  # False
print(True or False)   # True
print(not True)        # False

# Short-circuit evaluation
x = 0
# 'and' stops at first False, 'or' stops at first True
result = x != 0 and 10 / x > 1   # x != 0 is False → stops, no ZeroDivisionError
print(result)  # False

# ─── ASSIGNMENT ────────────────────────────────────────────────────
x = 10
x += 3    # x = x + 3 → 13
x -= 2    # x = x - 2 → 11
x *= 2    # x = x * 2 → 22
x //= 3   # x = x // 3 → 7
x **= 2   # x = x ** 2 → 49
x %= 10   # x = x % 10 → 9
print(x)  # 9

# ─── BITWISE (lower level — used in systems programming, flags) ─────
print(5 & 3)   # 1    AND
print(5 | 3)   # 7    OR
print(5 ^ 3)   # 6    XOR
print(~5)      # -6   NOT
print(5 << 1)  # 10   left shift (multiply by 2)
print(5 >> 1)  # 2    right shift (divide by 2)

# ─── IDENTITY AND MEMBERSHIP ───────────────────────────────────────
a = [1, 2, 3]
b = a
c = [1, 2, 3]
print(a is b)      # True  (same object in memory)
print(a is c)      # False (different objects, same content)
print(a == c)      # True  (same content)
print(2 in a)      # True
print(5 not in a)  # True
```

---

### 4.4 Operator Precedence

```python
# PEMDAS / BODMAS — Python follows standard math rules
# Highest to lowest:
# () Parentheses
# ** Exponent
# +x, -x, ~x Unary operators
# *, /, //, % Multiplication, Division
# +, - Addition, Subtraction
# <<, >> Bitwise shifts
# & Bitwise AND
# ^ Bitwise XOR
# | Bitwise OR
# ==, !=, <, >, <=, >= Comparisons
# not Logical NOT
# and Logical AND
# or Logical OR

print(2 + 3 * 4)      # 14 (multiplication first)
print((2 + 3) * 4)    # 20 (parentheses first)
print(2 ** 3 ** 2)    # 512 (right-to-left: 2 ** (3**2) = 2**9 = 512)
print((2 ** 3) ** 2)  # 64
```

---

---

## Lesson 5 — Lists — Ordered, Mutable Sequences

> **Level:** Beginner → Intermediate
> **Goal:** Master Python's most versatile data structure

---

### 5.1 Creating and Accessing Lists

```python
# Creating lists
empty    = []
numbers  = [1, 2, 3, 4, 5]
strings  = ["apple", "banana", "cherry"]
mixed    = [1, "hello", 3.14, True, None]   # Lists can mix types (but usually don't)
nested   = [[1, 2], [3, 4], [5, 6]]         # List of lists

# Accessing elements (same indexing as strings)
fruits = ["apple", "banana", "cherry", "date"]
print(fruits[0])    # "apple"
print(fruits[-1])   # "date"
print(fruits[1:3])  # ["banana", "cherry"]
print(fruits[::-1]) # ["date", "cherry", "banana", "apple"]

# Nested list access
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(matrix[1][2])   # 6  (row 1, col 2)
```

---

### 5.2 Modifying Lists

```python
fruits = ["apple", "banana", "cherry"]

# Modify an element (lists are mutable — strings are not)
fruits[1] = "blueberry"
print(fruits)  # ["apple", "blueberry", "cherry"]

# Add elements
fruits.append("date")           # Add to end
fruits.insert(1, "avocado")    # Insert at index 1
fruits.extend(["elderberry", "fig"])   # Add multiple elements
print(fruits)

# Remove elements
fruits.remove("apple")          # Remove by value (first occurrence)
last = fruits.pop()             # Remove and return last element
second = fruits.pop(1)          # Remove and return element at index 1
del fruits[0]                   # Delete by index (no return value)
fruits.clear()                  # Remove all elements

# Find elements
fruits = ["apple", "banana", "cherry", "banana"]
print(fruits.index("banana"))   # 1  (index of first occurrence)
print(fruits.count("banana"))   # 2  (count occurrences)
print("cherry" in fruits)       # True
```

---

### 5.3 List Methods — Complete Reference

```python
nums = [3, 1, 4, 1, 5, 9, 2, 6, 5]

# Sort in place (modifies the list)
nums.sort()
print(nums)  # [1, 1, 2, 3, 4, 5, 5, 6, 9]

nums.sort(reverse=True)
print(nums)  # [9, 6, 5, 5, 4, 3, 2, 1, 1]

# Sorted (returns new list, original unchanged)
original = [3, 1, 4, 1, 5]
sorted_list = sorted(original)
print(original)    # [3, 1, 4, 1, 5]  unchanged
print(sorted_list) # [1, 1, 3, 4, 5]

# Sort strings by length
words = ["banana", "fig", "apple", "kiwi"]
words.sort(key=len)   # Sort by length
print(words)          # ["fig", "kiwi", "apple", "banana"]

# Reverse in place
nums.reverse()

# Copy
original = [1, 2, 3]
copy1 = original.copy()   # Shallow copy
copy2 = original[:]       # Also shallow copy
copy3 = list(original)    # Also shallow copy

# Why shallow copy matters
nested = [[1, 2], [3, 4]]
shallow = nested.copy()
shallow[0].append(99)     # Modifies inner list
print(nested)             # [[1, 2, 99], [3, 4]]  ← original changed!

import copy
deep = copy.deepcopy(nested)  # Deep copy — completely independent
```

---

### 5.4 List Comprehensions — Python's Most Elegant Feature

```python
# Traditional loop
squares = []
for i in range(1, 6):
    squares.append(i ** 2)
print(squares)  # [1, 4, 9, 16, 25]

# List comprehension — same result, much more readable
squares = [i ** 2 for i in range(1, 6)]
print(squares)  # [1, 4, 9, 16, 25]

# With condition (filter)
even_squares = [i ** 2 for i in range(1, 11) if i % 2 == 0]
print(even_squares)  # [4, 16, 36, 64, 100]

# Transform strings
names = ["alice", "bob", "charlie"]
upper_names = [name.upper() for name in names]
print(upper_names)  # ["ALICE", "BOB", "CHARLIE"]

# Nested comprehension
matrix = [[i * j for j in range(1, 4)] for i in range(1, 4)]
print(matrix)  # [[1, 2, 3], [2, 4, 6], [3, 6, 9]]

# Flatten a nested list
nested = [[1, 2], [3, 4], [5, 6]]
flat = [x for row in nested for x in row]
print(flat)  # [1, 2, 3, 4, 5, 6]
```

---

### 5.5 Useful Built-in Functions with Lists

```python
nums = [3, 1, 4, 1, 5, 9, 2, 6]

print(len(nums))    # 8
print(sum(nums))    # 31
print(min(nums))    # 1
print(max(nums))    # 9

# zip — combine two lists element by element
names = ["Alice", "Bob", "Charlie"]
scores = [95, 87, 92]
combined = list(zip(names, scores))
print(combined)  # [("Alice", 95), ("Bob", 87), ("Charlie", 92)]

# enumerate — get index and value together
for index, name in enumerate(names):
    print(f"{index}: {name}")
# 0: Alice
# 1: Bob
# 2: Charlie

# enumerate with start value
for index, name in enumerate(names, start=1):
    print(f"{index}. {name}")
# 1. Alice
# 2. Bob
# 3. Charlie
```

---

---

## Lesson 6 — Tuples, Sets, and Dictionaries

> **Level:** Beginner → Intermediate

---

### 6.1 Tuples — Immutable Sequences

```python
# Creating tuples
empty     = ()
single    = (42,)       # Note the comma — (42) is just 42 in parentheses
point     = (3, 4)
rgb       = (255, 128, 0)
mixed     = (1, "hello", 3.14)

# Tuple packing / unpacking
coords = (10, 20)
x, y = coords           # Unpacking
print(x, y)             # 10 20

# Accessing (same as lists — but no modification!)
print(rgb[0])           # 255
print(rgb[-1])          # 0
print(rgb[1:])          # (128, 0)

# Tuples are immutable
# rgb[0] = 100   ← TypeError!

# Why use tuples over lists?
# 1. Immutability signals "this data should not change"
# 2. Slightly faster than lists
# 3. Can be used as dictionary keys (lists cannot)
# 4. Functions return multiple values as tuples

def get_dimensions():
    return 1920, 1080   # Returns a tuple

width, height = get_dimensions()
print(width, height)    # 1920 1080

# Named tuples — tuples with field names
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(3, 4)
print(p.x, p.y)         # 3 4
print(p[0], p[1])       # 3 4  (still accessible by index)
```

---

### 6.2 Sets — Unique, Unordered Collections

```python
# Creating sets
empty_set = set()           # NOT {} — that creates an empty dict!
fruits = {"apple", "banana", "cherry", "apple"}
print(fruits)               # {"apple", "banana", "cherry"}  (duplicate removed!)

# ─── SET OPERATIONS (based on mathematical set theory) ─────────────
a = {1, 2, 3, 4, 5}
b = {4, 5, 6, 7, 8}

print(a | b)     # {1,2,3,4,5,6,7,8}  union (all elements)
print(a & b)     # {4, 5}              intersection (common elements)
print(a - b)     # {1, 2, 3}          difference (in a but not b)
print(a ^ b)     # {1,2,3,6,7,8}      symmetric difference (not in both)

# Method versions (same operations)
print(a.union(b))
print(a.intersection(b))
print(a.difference(b))

# Modifying sets
fruits.add("date")
fruits.discard("apple")   # remove without error if not found
fruits.remove("banana")   # remove — raises KeyError if not found

# Checking membership (O(1) — much faster than list for large collections)
print("cherry" in fruits)   # True
print("mango" in fruits)    # False

# Subset / superset
print({1, 2}.issubset({1, 2, 3}))    # True
print({1, 2, 3}.issuperset({1, 2}))  # True

# Use case: fast deduplication
duplicates = [1, 2, 2, 3, 3, 3, 4]
unique = list(set(duplicates))
print(unique)   # [1, 2, 3, 4]  (order may vary)
```

---

### 6.3 Dictionaries — Key-Value Stores

```python
# Creating dictionaries
empty = {}
person = {
    "name": "Alice",
    "age": 28,
    "city": "London",
    "skills": ["Python", "SQL", "Docker"]
}

# ─── ACCESSING ─────────────────────────────────────────────────────
print(person["name"])           # "Alice"
print(person.get("age"))        # 28
print(person.get("salary", 0))  # 0  (default if key missing — avoids KeyError)

# Prefer .get() over [] when key might not exist
# person["salary"]   ← KeyError if key doesn't exist!

# ─── MODIFYING ─────────────────────────────────────────────────────
person["age"] = 29              # Update existing
person["email"] = "alice@example.com"  # Add new key
del person["city"]              # Delete a key
popped = person.pop("email")    # Remove and return

# ─── CHECKING ──────────────────────────────────────────────────────
print("name" in person)         # True
print("city" in person)         # False
print(len(person))              # 3

# ─── ITERATING ─────────────────────────────────────────────────────
# Iterate over keys (default)
for key in person:
    print(key)

# Iterate over values
for value in person.values():
    print(value)

# Iterate over key-value pairs
for key, value in person.items():
    print(f"{key}: {value}")

# ─── METHODS ───────────────────────────────────────────────────────
print(person.keys())    # dict_keys(['name', 'age', 'skills'])
print(person.values())  # dict_values(['Alice', 29, [...]])
print(person.items())   # dict_items([('name', 'Alice'), ...])

# Update (merge another dict)
updates = {"age": 30, "language": "English"}
person.update(updates)

# Merge with | operator (Python 3.9+)
combined = person | {"new_key": "value"}

# ─── DICT COMPREHENSION ────────────────────────────────────────────
squares = {n: n**2 for n in range(1, 6)}
print(squares)  # {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# Filter a dict
scores = {"Alice": 95, "Bob": 72, "Charlie": 88, "Diana": 65}
passing = {name: score for name, score in scores.items() if score >= 75}
print(passing)  # {"Alice": 95, "Charlie": 88}

# defaultdict — avoid KeyError when key missing
from collections import defaultdict
word_count = defaultdict(int)   # Default value is int() = 0
text = "the cat sat on the mat the cat"
for word in text.split():
    word_count[word] += 1       # No KeyError even on first occurrence
print(dict(word_count))
```

---

### 6.4 Exercises — Lessons 5–6

**Exercise 1 (Lists):** Write a function that takes a list of numbers and returns a new list with:
- Duplicates removed
- Sorted in descending order
- Only numbers greater than 10

**Exercise 2 (Dict):** Given a list of student scores:
```python
scores = [("Alice", 95), ("Bob", 72), ("Alice", 88), ("Charlie", 95)]
```
Create a dictionary where each student's name maps to their AVERAGE score.

**Exercise 3 (Sets):** Given two lists of tags:
```python
python_jobs = ["python", "sql", "docker", "aws", "linux"]
data_jobs = ["python", "sql", "r", "tableau", "statistics"]
```
Find: tags required for both jobs, tags unique to python jobs, all unique tags.

---

---

## Lesson 7 — Conditional Statements

> **Level:** Beginner
> **Goal:** Make programs that make decisions

---

### 7.1 if / elif / else

```python
# Basic if statement
temperature = 25

if temperature > 30:
    print("It's hot!")

# if-else
if temperature > 30:
    print("It's hot!")
else:
    print("It's not hot")

# if-elif-else (check multiple conditions)
if temperature > 35:
    print("Extreme heat warning")
elif temperature > 25:
    print("Warm day")
elif temperature > 15:
    print("Mild day")
elif temperature > 5:
    print("Cool day")
else:
    print("Cold day!")

# IMPORTANT: Python uses indentation (4 spaces) to define code blocks
# This is not optional — wrong indentation is a syntax error
```

---

### 7.2 Truthy and Falsy Values

```python
# Python evaluates conditions as truthy or falsy, not just True/False
# FALSY VALUES (evaluate to False in a condition):
# False, None, 0, 0.0, 0j, "", [], (), {}, set()

# TRUTHY VALUES: everything else

# Examples
name = ""
if name:
    print(f"Hello, {name}")
else:
    print("Name is empty")   # ← This runs

items = [1, 2, 3]
if items:
    print("List has items")   # ← This runs

user = None
if user:
    print("User exists")
else:
    print("No user")          # ← This runs

# Practical: check if list is non-empty before accessing
data = []
if data:
    print(data[0])     # Safe — only runs if data is non-empty
```

---

### 7.3 Conditional Expressions (Ternary)

```python
# Traditional if-else
age = 20
if age >= 18:
    status = "adult"
else:
    status = "minor"

# Ternary operator: value_if_true if condition else value_if_false
status = "adult" if age >= 18 else "minor"
print(status)  # "adult"

# Practical uses
absolute = x if x >= 0 else -x     # absolute value (without abs())
label = "yes" if is_valid else "no"
greeting = "Good morning" if hour < 12 else "Good afternoon"
```

---

### 7.4 Match Statement (Python 3.10+)

```python
# match is Python's version of switch/case
command = "quit"

match command:
    case "quit" | "exit":
        print("Exiting...")
    case "help":
        print("Available commands: quit, help, status")
    case "status":
        print("System running normally")
    case _:                      # Default case (wildcard)
        print(f"Unknown command: {command}")

# Match with patterns — very powerful
point = (0, 5)
match point:
    case (0, 0):
        print("Origin")
    case (0, y):
        print(f"On Y-axis at y={y}")
    case (x, 0):
        print(f"On X-axis at x={x}")
    case (x, y):
        print(f"Point at ({x}, {y})")
```

---

---

## Lesson 8 — Loops

> **Level:** Beginner → Intermediate
> **Goal:** Repeat operations efficiently

---

### 8.1 for Loops

```python
# Iterate over a sequence
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

# Range — generate a sequence of numbers
for i in range(5):         # 0, 1, 2, 3, 4
    print(i)

for i in range(2, 10):     # 2, 3, 4, 5, 6, 7, 8, 9
    print(i)

for i in range(0, 20, 3):  # 0, 3, 6, 9, 12, 15, 18
    print(i)

for i in range(10, 0, -1): # 10, 9, 8, 7, 6, 5, 4, 3, 2, 1 (countdown)
    print(i)

# Iterate over a string
for char in "Python":
    print(char)

# Iterate over dict items
person = {"name": "Alice", "age": 28}
for key, value in person.items():
    print(f"{key}: {value}")

# enumerate — get index + value
for index, fruit in enumerate(fruits, start=1):
    print(f"{index}. {fruit}")
```

---

### 8.2 while Loops

```python
# Run as long as condition is True
count = 0
while count < 5:
    print(count)
    count += 1   # DON'T FORGET THIS — or you get infinite loop!

# while with break — exit loop early
while True:
    user_input = input("Enter 'quit' to exit: ")
    if user_input.lower() == "quit":
        break
    print(f"You entered: {user_input}")

# Practical: retry logic
import random
attempts = 0
max_attempts = 3
while attempts < max_attempts:
    number = random.randint(1, 10)
    if number == 7:
        print(f"Got 7 after {attempts + 1} attempts!")
        break
    attempts += 1
else:
    # The else clause runs if loop completes WITHOUT break
    print("Didn't get 7 in 3 attempts")
```

---

### 8.3 Loop Control — break, continue, else

```python
# break — exit loop immediately
for i in range(10):
    if i == 5:
        break
    print(i)         # Prints 0, 1, 2, 3, 4

# continue — skip rest of this iteration, continue with next
for i in range(10):
    if i % 2 == 0:
        continue     # Skip even numbers
    print(i)         # Prints 1, 3, 5, 7, 9

# Loop else — runs when loop completes WITHOUT a break
# Very Pythonic — used to signal "item not found"
def find_prime(numbers):
    for n in numbers:
        for divisor in range(2, n):
            if n % divisor == 0:
                break      # n is not prime — break inner loop
        else:
            # Inner loop completed without break → n is prime
            return n
    return None
```

---

### 8.4 Nested Loops and Comprehensions

```python
# Multiplication table
for i in range(1, 4):
    for j in range(1, 4):
        print(f"{i*j:2}", end=" ")
    print()    # Newline after each row
# 1  2  3
# 2  4  6
# 3  6  9

# Practical: process a 2D dataset
students = [
    {"name": "Alice", "grades": [90, 85, 92]},
    {"name": "Bob",   "grades": [78, 82, 88]},
]
for student in students:
    avg = sum(student["grades"]) / len(student["grades"])
    print(f"{student['name']}: {avg:.1f}")
```

---

---

## Lesson 9 — Functions

> **Level:** Beginner → Intermediate
> **Goal:** Write reusable, clean, well-documented functions

---

### 9.1 Defining and Calling Functions

```python
# Basic function
def greet():
    print("Hello, World!")

greet()   # Calling the function

# Function with parameters
def greet_person(name):
    print(f"Hello, {name}!")

greet_person("Alice")
greet_person("Bob")

# Function with return value
def add(a, b):
    return a + b

result = add(3, 4)
print(result)   # 7

# Functions are first-class objects in Python
print(type(add))   # <class 'function'>
double = add        # Assign function to variable
print(double(3, 4)) # 7
```

---

### 9.2 Parameters — All Types

```python
# ─── POSITIONAL PARAMETERS ────────────────────────────────────────
def power(base, exponent):
    return base ** exponent

print(power(2, 8))      # 256  (positional — order matters)

# ─── DEFAULT PARAMETERS ───────────────────────────────────────────
def greet(name, greeting="Hello"):   # greeting has a default
    return f"{greeting}, {name}!"

print(greet("Alice"))           # "Hello, Alice!"
print(greet("Bob", "Hi"))       # "Hi, Bob!"
print(greet("Charlie", greeting="Hey"))  # "Hey, Charlie!"

# Default parameters are evaluated ONCE at function definition time
# Common pitfall:
def add_item(item, items=[]):       # BAD — mutable default!
    items.append(item)
    return items

print(add_item("a"))  # ["a"]
print(add_item("b"))  # ["a", "b"]   ← Unexpected! Shared across calls!

# Correct way:
def add_item(item, items=None):     # GOOD
    if items is None:
        items = []
    items.append(item)
    return items

# ─── KEYWORD ARGUMENTS ────────────────────────────────────────────
def describe_pet(name, animal_type, age):
    print(f"{name} is a {age}-year-old {animal_type}")

describe_pet(age=3, name="Buddy", animal_type="dog")   # Order doesn't matter

# ─── VARIABLE POSITIONAL ARGUMENTS (*args) ────────────────────────
def total(*numbers):
    print(type(numbers))   # <class 'tuple'>
    return sum(numbers)

print(total(1, 2, 3))         # 6
print(total(1, 2, 3, 4, 5))   # 15

# ─── VARIABLE KEYWORD ARGUMENTS (**kwargs) ────────────────────────
def create_profile(**details):
    print(type(details))   # <class 'dict'>
    for key, value in details.items():
        print(f"  {key}: {value}")

create_profile(name="Alice", age=28, city="London")

# ─── COMBINING ALL PARAMETER TYPES ────────────────────────────────
# Order: positional, *args, keyword-only, **kwargs
def full_function(a, b, *args, keyword=None, **kwargs):
    print(f"a={a}, b={b}")
    print(f"extra positional: {args}")
    print(f"keyword: {keyword}")
    print(f"extra keyword: {kwargs}")

full_function(1, 2, 3, 4, 5, keyword="hello", x=10, y=20)
```

---

### 9.3 Return Values

```python
# Return multiple values (as tuple)
def get_stats(numbers):
    return min(numbers), max(numbers), sum(numbers) / len(numbers)

minimum, maximum, average = get_stats([1, 2, 3, 4, 5])
print(minimum, maximum, average)   # 1 5 3.0

# Functions without explicit return → return None
def no_return():
    x = 42   # Does something but returns nothing

result = no_return()
print(result)   # None

# Early returns — cleaner than deeply nested if
def get_grade(score):
    if score < 0 or score > 100:
        return "Invalid score"
    if score >= 90:
        return "A"
    if score >= 80:
        return "B"
    if score >= 70:
        return "C"
    return "F"
```

---

### 9.4 Docstrings and Type Hints

```python
def calculate_bmi(weight_kg: float, height_m: float) -> float:
    """
    Calculate Body Mass Index (BMI).

    Args:
        weight_kg: Weight in kilograms.
        height_m: Height in metres.

    Returns:
        BMI as a float rounded to 2 decimal places.

    Raises:
        ValueError: If weight or height is not positive.

    Example:
        >>> calculate_bmi(70, 1.75)
        22.86
    """
    if weight_kg <= 0 or height_m <= 0:
        raise ValueError("Weight and height must be positive")
    return round(weight_kg / height_m ** 2, 2)

# Access docstring
print(calculate_bmi.__doc__)
help(calculate_bmi)
```

---

### 9.5 Lambda Functions

```python
# Lambda: anonymous one-line functions
square = lambda x: x ** 2
print(square(5))   # 25

# Same as:
def square(x):
    return x ** 2

# Lambda shines as arguments to higher-order functions
numbers = [5, 2, 8, 1, 9, 3]
sorted_nums = sorted(numbers)
print(sorted_nums)

# Sort by custom key
words = ["banana", "fig", "apple", "kiwi", "elderberry"]
words.sort(key=lambda w: len(w))      # Sort by length
words.sort(key=lambda w: w[-1])       # Sort by last character

# map and filter (modern Python: use comprehensions instead)
doubled = list(map(lambda x: x * 2, [1, 2, 3, 4]))      # [2, 4, 6, 8]
evens   = list(filter(lambda x: x % 2 == 0, [1,2,3,4])) # [2, 4]

# Comprehension equivalents (preferred):
doubled = [x * 2 for x in [1, 2, 3, 4]]
evens   = [x for x in [1, 2, 3, 4] if x % 2 == 0]
```

---

### 9.6 Exercises — Lessons 7–9

**Exercise 1 (Conditionals + Loops):** Write FizzBuzz — for numbers 1 to 100:
- Print "Fizz" for multiples of 3
- Print "Buzz" for multiples of 5
- Print "FizzBuzz" for multiples of both
- Print the number otherwise

**Exercise 2 (Functions):** Write a function `is_palindrome(text)` that returns True if a string reads the same forwards and backwards. It should ignore case and spaces.
- "racecar" → True
- "A man a plan a canal Panama" → True
- "hello" → False

**Exercise 3 (Functions):** Write a function `word_frequency(text)` that returns a dictionary of each word and how many times it appears. Sort the result by frequency (highest first).

---

---

## Lesson 10 — Practice Project — CLI Calculator

> **Level:** Beginner → Intermediate
> **Goal:** Build a real application combining everything from Lessons 1–9

---

### 10.1 Project Overview

Build a command-line calculator that:
- Accepts two numbers and an operator from the user
- Performs the calculation
- Shows a history of calculations
- Handles invalid input gracefully
- Can be run repeatedly until the user quits

---

### 10.2 Complete Solution

```python
# calculator.py — CLI Calculator
"""
A command-line calculator with history.
Demonstrates: variables, types, strings, functions, loops, conditionals.
"""

def add(a: float, b: float) -> float:
    """Return the sum of a and b."""
    return a + b

def subtract(a: float, b: float) -> float:
    """Return a minus b."""
    return a - b

def multiply(a: float, b: float) -> float:
    """Return a times b."""
    return a * b

def divide(a: float, b: float) -> float:
    """Return a divided by b. Raises ValueError if b is zero."""
    if b == 0:
        raise ValueError("Cannot divide by zero")
    return a / b

def power(a: float, b: float) -> float:
    """Return a to the power of b."""
    return a ** b

# Map operator symbols to functions
OPERATIONS = {
    "+": add,
    "-": subtract,
    "*": multiply,
    "/": divide,
    "**": power,
}

def display_history(history: list) -> None:
    """Print the calculation history."""
    if not history:
        print("No calculations yet.")
        return
    print("\n─── History ─────────────────")
    for i, entry in enumerate(history, 1):
        print(f"  {i}. {entry}")
    print("─────────────────────────────")

def get_number(prompt: str) -> float:
    """Prompt user for a number, retry on invalid input."""
    while True:
        try:
            return float(input(prompt))
        except ValueError:
            print("  Invalid input — please enter a number.")

def main():
    """Main calculator loop."""
    print("=" * 40)
    print("  Python CLI Calculator")
    print(f"  Operations: {' '.join(OPERATIONS.keys())}")
    print("  Type 'history' to view history")
    print("  Type 'quit' to exit")
    print("=" * 40)

    history = []

    while True:
        print()
        user_input = input("Enter operator (or 'history'/'quit'): ").strip().lower()

        if user_input == "quit":
            print("Goodbye!")
            break

        if user_input == "history":
            display_history(history)
            continue

        if user_input not in OPERATIONS:
            valid = ", ".join(OPERATIONS.keys())
            print(f"  Unknown operator. Use: {valid}")
            continue

        operator = user_input
        a = get_number("  First number: ")
        b = get_number("  Second number: ")

        try:
            result = OPERATIONS[operator](a, b)
            # Format nicely: show int if whole number
            display_result = int(result) if result == int(result) else round(result, 6)
            calculation = f"{a} {operator} {b} = {display_result}"
            print(f"  Result: {display_result}")
            history.append(calculation)
        except ValueError as e:
            print(f"  Error: {e}")

if __name__ == "__main__":
    main()
```

```bash
# Run it
python3 calculator.py
```

---

### 10.3 Mini Quiz — Phase 1

**Q1.** What is the output of this code?
```python
x = [1, 2, 3]
y = x
y.append(4)
print(x)
```

<details>
<summary>Answer</summary>

`[1, 2, 3, 4]`

`y = x` does NOT create a copy — both `x` and `y` point to the SAME list in memory. Modifying `y` modifies `x`. To copy: `y = x.copy()` or `y = x[:]`.

</details>

---

**Q2.** What does this print?
```python
def func(n, result=[]):
    result.append(n)
    return result

print(func(1))
print(func(2))
print(func(3))
```

<details>
<summary>Answer</summary>

```
[1]
[1, 2]
[1, 2, 3]
```

This is the mutable default argument pitfall! The `result=[]` default is created ONCE when the function is defined, not on every call. All calls share the same list object.

</details>

---

**Q3.** What is the difference between `is` and `==`?

<details>
<summary>Answer</summary>

`==` checks **value equality** — are the contents the same?
`is` checks **identity** — are they the exact same object in memory?

```python
a = [1, 2, 3]
b = [1, 2, 3]
print(a == b)   # True  (same content)
print(a is b)   # False (different objects)

c = a
print(a is c)   # True  (same object)
```

Use `is` only to check `None`: `if x is None`. Use `==` for everything else.

</details>


---

---

# PHASE 2 — INTERMEDIATE

---

## Lesson 11 — Modules and Packages

> **Level:** Intermediate
> **Goal:** Organise code into reusable, importable units

---

### 11.1 What are Modules?

A module is simply a `.py` file. Any Python file you write is a module. Modules let you organise code across files and reuse it across projects.

```python
# math_utils.py — your custom module
"""Utility functions for mathematical operations."""

PI = 3.14159265358979

def circle_area(radius: float) -> float:
    """Calculate area of a circle."""
    return PI * radius ** 2

def circle_circumference(radius: float) -> float:
    """Calculate circumference of a circle."""
    return 2 * PI * radius

def is_prime(n: int) -> bool:
    """Return True if n is prime."""
    if n < 2:
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True
```

```python
# main.py — import and use the module
import math_utils

print(math_utils.circle_area(5))          # 78.539...
print(math_utils.PI)                       # 3.14159...

# Import specific names
from math_utils import circle_area, is_prime

print(circle_area(5))   # No need for module prefix
print(is_prime(17))     # True

# Import with alias
import math_utils as mu
print(mu.circle_area(5))

# Import everything (use sparingly — pollutes namespace)
from math_utils import *
```

---

### 11.2 The `__name__ == "__main__"` Guard

```python
# math_utils.py
def circle_area(radius):
    return 3.14159 * radius ** 2

# This block ONLY runs when you execute this file directly
# It does NOT run when this file is imported as a module
if __name__ == "__main__":
    # Testing code
    print("Testing circle_area:")
    print(circle_area(5))     # 78.5398...
    print(circle_area(10))    # 314.159...
    print("All tests passed!")
```

```bash
python3 math_utils.py   # → prints test output
python3 main.py         # → imports math_utils, __name__ guard does NOT run
```

---

### 11.3 Python's Standard Library — Know These Modules

```python
# ─── os — Operating System Interface ──────────────────────────────
import os

print(os.getcwd())                    # Current working directory
print(os.listdir("."))               # List directory contents
os.makedirs("new_dir/sub_dir", exist_ok=True)  # Create nested dirs
os.path.join("home", "alice", "doc.txt")       # Safe path joining
os.path.exists("file.txt")            # Check if path exists
os.path.isfile("file.txt")            # Is it a file?
os.path.isdir("mydir")               # Is it a directory?
os.path.basename("/home/alice/file.txt")  # "file.txt"
os.path.dirname("/home/alice/file.txt")   # "/home/alice"
print(os.environ.get("HOME"))         # Read environment variable

# ─── pathlib — Modern Path Handling (prefer over os.path) ──────────
from pathlib import Path

p = Path("/home/alice/documents")
print(p.name)        # "documents"
print(p.parent)      # /home/alice
print(p.suffix)      # ""

f = Path("config.json")
print(f.stem)        # "config"
print(f.suffix)      # ".json"

home = Path.home()                    # User's home directory
config = home / "myapp" / "config"    # Path joining with /
config.mkdir(parents=True, exist_ok=True)

# Read/write files with pathlib
text = Path("file.txt").read_text()
Path("output.txt").write_text("Hello, World!")

# ─── sys — System-Specific Parameters ──────────────────────────────
import sys

print(sys.version)          # Python version string
print(sys.platform)         # "darwin", "linux", "win32"
print(sys.argv)             # Command-line arguments
sys.exit(0)                 # Exit program (0 = success, 1 = error)
sys.path.append("/custom/modules")   # Add to module search path

# ─── datetime — Dates and Times ────────────────────────────────────
from datetime import datetime, date, timedelta

now = datetime.now()
print(now)                              # 2024-01-15 14:30:00.123456
print(now.strftime("%Y-%m-%d %H:%M"))  # "2024-01-15 14:30"
print(now.year, now.month, now.day)    # 2024 1 15

today = date.today()
birthday = date(1995, 6, 15)
age_days = (today - birthday).days
print(f"Age: {age_days // 365} years")

future = now + timedelta(days=30, hours=2)
print(future.strftime("%B %d, %Y"))   # "February 14, 2024"

parsed = datetime.strptime("2024-01-15", "%Y-%m-%d")

# ─── json — JSON Serialisation ─────────────────────────────────────
import json

data = {"name": "Alice", "age": 28, "skills": ["Python", "SQL"]}
json_string = json.dumps(data, indent=2)   # dict → string
print(json_string)

parsed = json.loads(json_string)           # string → dict
print(parsed["name"])

with open("data.json", "w") as f:
    json.dump(data, f, indent=2)           # dict → file

with open("data.json", "r") as f:
    loaded = json.load(f)                  # file → dict

# ─── random ────────────────────────────────────────────────────────
import random

print(random.randint(1, 10))       # Random int between 1 and 10 inclusive
print(random.choice([1, 2, 3, 4])) # Random element from list
random.shuffle([1, 2, 3, 4])       # Shuffle in place
print(random.random())             # Float between 0.0 and 1.0
sample = random.sample(range(100), 10)  # 10 unique random numbers

# ─── collections ───────────────────────────────────────────────────
from collections import Counter, defaultdict, OrderedDict, deque

# Counter — count occurrences
text = "the quick brown fox jumps over the lazy dog"
word_counts = Counter(text.split())
print(word_counts.most_common(3))   # 3 most common words

char_counts = Counter("mississippi")
print(char_counts)   # Counter({'s': 4, 'i': 4, 'p': 2, 'm': 1})

# deque — efficient append/pop from both ends
dq = deque([1, 2, 3])
dq.appendleft(0)    # [0, 1, 2, 3]
dq.popleft()        # 0

# ─── itertools ─────────────────────────────────────────────────────
import itertools

# Infinite iterator — use with break
counter = itertools.count(start=10, step=2)  # 10, 12, 14, ...

# Combinations and permutations
print(list(itertools.combinations("ABC", 2)))    # [('A','B'), ('A','C'), ('B','C')]
print(list(itertools.permutations("ABC", 2)))    # All ordered pairs
print(list(itertools.product([0,1], repeat=3)))  # All 3-bit binary numbers
```

---

### 11.4 Packages — Organising Multiple Modules

A package is a directory containing modules and an `__init__.py` file.

```
mypackage/
├── __init__.py          ← Makes it a package (can be empty or import things)
├── math_utils.py
├── string_utils.py
└── data/
    ├── __init__.py
    └── validators.py
```

```python
# mypackage/__init__.py
from .math_utils import circle_area, is_prime
from .string_utils import clean_text

# Now users can do:
from mypackage import circle_area    # instead of from mypackage.math_utils import ...
```

```python
# Using the package
import mypackage.math_utils as math_utils
from mypackage.data.validators import is_valid_email

# After __init__.py setup:
from mypackage import circle_area
```

---

### 11.5 Third-Party Packages with pip

```bash
# Install packages
pip install requests               # HTTP library
pip install pandas numpy           # Data analysis
pip install fastapi uvicorn        # Web API framework
pip install pytest                 # Testing

# Install specific version
pip install requests==2.31.0

# Install from requirements file
pip install -r requirements.txt

# Show installed packages
pip list
pip show requests    # Detailed info about a package

# Uninstall
pip uninstall requests

# Generate requirements.txt
pip freeze > requirements.txt
```

---

---

## Lesson 12 — File Handling

> **Level:** Intermediate
> **Goal:** Read and write files safely

---

### 12.1 Opening and Reading Files

```python
# ─── ALWAYS use context manager (with) — auto-closes the file ──────
# File modes:
# "r"  — read (default)
# "w"  — write (creates new or overwrites)
# "a"  — append (adds to end)
# "rb" — read binary
# "wb" — write binary
# "r+" — read + write

# Read entire file
with open("data.txt", "r") as f:
    content = f.read()    # Entire file as one string
    print(content)

# Read line by line (memory efficient for large files)
with open("data.txt", "r") as f:
    for line in f:
        print(line.strip())   # strip() removes trailing \n

# Read all lines into a list
with open("data.txt", "r") as f:
    lines = f.readlines()   # ["line 1\n", "line 2\n", ...]
    # OR:
    lines = f.read().splitlines()  # ["line 1", "line 2", ...]  (no \n)

# Read with specific encoding (always specify for text files)
with open("data.txt", "r", encoding="utf-8") as f:
    content = f.read()
```

---

### 12.2 Writing Files

```python
# Write (creates new file or overwrites existing)
with open("output.txt", "w", encoding="utf-8") as f:
    f.write("Hello, World!\n")
    f.write("Second line\n")

# Write multiple lines at once
lines = ["Line 1", "Line 2", "Line 3"]
with open("output.txt", "w", encoding="utf-8") as f:
    f.writelines(line + "\n" for line in lines)  # Generator — memory efficient

# Append to existing file
with open("log.txt", "a", encoding="utf-8") as f:
    f.write("New log entry\n")

# Print to file
with open("output.txt", "w") as f:
    print("Hello", "World", sep=", ", end="!\n", file=f)
```

---

### 12.3 Working with CSV and JSON Files

```python
# ─── CSV ─────────────────────────────────────────────────────────
import csv

# Writing CSV
data = [
    ["Name", "Age", "City"],
    ["Alice", 28, "London"],
    ["Bob", 32, "Paris"],
]
with open("people.csv", "w", newline="", encoding="utf-8") as f:
    writer = csv.writer(f)
    writer.writerows(data)

# Reading CSV
with open("people.csv", "r", encoding="utf-8") as f:
    reader = csv.DictReader(f)   # Each row as a dict
    for row in reader:
        print(f"{row['Name']} lives in {row['City']}")

# ─── JSON ────────────────────────────────────────────────────────
import json
from datetime import datetime

# Custom JSON encoder for types Python can't serialise by default
class CustomEncoder(json.JSONEncoder):
    def default(self, obj):
        if isinstance(obj, datetime):
            return obj.isoformat()
        return super().default(obj)

data = {"name": "Alice", "created": datetime.now()}
json_str = json.dumps(data, cls=CustomEncoder, indent=2)
print(json_str)
```

---

### 12.4 pathlib for File Operations

```python
from pathlib import Path

# Create and navigate paths
base = Path("project")
base.mkdir(exist_ok=True)

data_dir = base / "data"
data_dir.mkdir(exist_ok=True)

# Write and read
config_file = base / "config.json"
config_file.write_text('{"debug": true, "port": 8080}')
config = config_file.read_text()

# Find files
project = Path(".")
for py_file in project.rglob("*.py"):     # Recursive glob
    print(py_file)

for txt_file in project.glob("*.txt"):    # Non-recursive
    print(txt_file)

# File info
f = Path("data.txt")
if f.exists():
    print(f.stat().st_size)         # File size in bytes
    print(f.stat().st_mtime)        # Last modified timestamp
    f.rename(Path("data_old.txt"))  # Rename
    f.unlink()                      # Delete

# Temporary files
import tempfile
with tempfile.NamedTemporaryFile(mode="w", suffix=".txt", delete=False) as f:
    f.write("temporary content")
    temp_path = f.name
print(f"Temp file: {temp_path}")
```

---

---

## Lesson 13 — Exception Handling

> **Level:** Intermediate
> **Goal:** Write robust code that handles errors gracefully

---

### 13.1 Understanding Exceptions

```python
# Without exception handling — program crashes
result = 10 / 0          # ZeroDivisionError
name = None
name.upper()             # AttributeError
number = int("abc")      # ValueError
my_list = [1, 2, 3]
print(my_list[10])       # IndexError
d = {"a": 1}
print(d["b"])            # KeyError

# Python's exception hierarchy (partial):
# BaseException
#   └── Exception
#         ├── ArithmeticError
#         │     └── ZeroDivisionError
#         ├── LookupError
#         │     ├── IndexError
#         │     └── KeyError
#         ├── TypeError
#         ├── ValueError
#         ├── AttributeError
#         ├── IOError / OSError
#         │     └── FileNotFoundError
#         ├── ImportError
#         └── RuntimeError
```

---

### 13.2 try / except / else / finally

```python
# Basic structure
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")

# Catch multiple exception types
try:
    number = int(input("Enter a number: "))
    result = 100 / number
except ValueError:
    print("That's not a valid number")
except ZeroDivisionError:
    print("Cannot divide by zero")

# Catch multiple exceptions in one except clause
try:
    x = int("abc")
except (ValueError, TypeError) as e:
    print(f"Conversion error: {e}")

# Catch ANY exception (use carefully)
try:
    something_risky()
except Exception as e:
    print(f"An error occurred: {type(e).__name__}: {e}")

# else — runs only if NO exception was raised
try:
    result = int("42")
except ValueError:
    print("Invalid number")
else:
    print(f"Got number: {result}")   # Only runs if try succeeded

# finally — ALWAYS runs (cleanup code)
file = None
try:
    file = open("data.txt")
    data = file.read()
except FileNotFoundError:
    print("File not found")
finally:
    if file:
        file.close()   # Always close the file

# Better: use context manager (with) — automatically handles finally
with open("data.txt") as f:   # File always closed, even on exception
    data = f.read()
```

---

### 13.3 Raising Exceptions

```python
# Raise an exception manually
def validate_age(age: int) -> int:
    if not isinstance(age, int):
        raise TypeError(f"Age must be int, got {type(age).__name__}")
    if age < 0:
        raise ValueError(f"Age cannot be negative, got {age}")
    if age > 150:
        raise ValueError(f"Age {age} seems unrealistic")
    return age

# Re-raise — catch, log, then re-raise for caller to handle
def process_data(data):
    try:
        result = risky_operation(data)
    except Exception as e:
        print(f"Logging error: {e}")   # Log it
        raise                          # Re-raise same exception

# Raise with chained exception (from)
def load_config(path):
    try:
        with open(path) as f:
            import json
            return json.load(f)
    except FileNotFoundError as e:
        raise RuntimeError(f"Config file not found: {path}") from e
```

---

### 13.4 Custom Exceptions

```python
# Define a hierarchy of custom exceptions for your application
class AppError(Exception):
    """Base exception for all application errors."""
    pass

class ValidationError(AppError):
    """Raised when input validation fails."""
    def __init__(self, field: str, message: str):
        self.field = field
        self.message = message
        super().__init__(f"Validation error on '{field}': {message}")

class DatabaseError(AppError):
    """Raised when database operations fail."""
    def __init__(self, operation: str, original_error: Exception = None):
        self.operation = operation
        super().__init__(f"Database error during {operation}")
        if original_error:
            self.__cause__ = original_error

class NotFoundError(AppError):
    """Raised when a requested resource doesn't exist."""
    def __init__(self, resource: str, resource_id):
        super().__init__(f"{resource} with id={resource_id} not found")

# Using custom exceptions
def get_user(user_id: int):
    if not isinstance(user_id, int):
        raise ValidationError("user_id", "Must be an integer")
    user = database.find(user_id)
    if user is None:
        raise NotFoundError("User", user_id)
    return user

# Caller handles them specifically
try:
    user = get_user("abc")
except ValidationError as e:
    print(f"Bad input: {e.field} — {e.message}")
except NotFoundError as e:
    print(f"Not found: {e}")
except AppError as e:
    print(f"Application error: {e}")   # Catches any AppError
```

---

---

## Lesson 14 — Object-Oriented Programming — Classes

> **Level:** Intermediate
> **Goal:** Model real-world concepts as objects

---

### 14.1 Why OOP?

Procedural programming groups related code into functions. OOP groups related data AND code together into objects. When your data and the functions that operate on it are always together, your code is easier to understand, test, and extend.

```python
# Procedural approach — data and functions separate
def calculate_area(width, height):
    return width * height

def calculate_perimeter(width, height):
    return 2 * (width + height)

w, h = 5, 3
area = calculate_area(w, h)

# OOP approach — data and functions together in an object
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

rect = Rectangle(5, 3)
print(rect.area())       # 15
print(rect.perimeter())  # 16
```

---

### 14.2 Defining Classes — Complete Reference

```python
class BankAccount:
    """
    Represents a bank account.

    Demonstrates: instance variables, class variables,
    instance methods, class methods, static methods,
    properties, and dunder methods.
    """
    # Class variable — shared by ALL instances
    interest_rate = 0.05
    _total_accounts = 0    # Convention: _ means "internal use"

    def __init__(self, owner: str, initial_deposit: float = 0.0):
        """Constructor — called when BankAccount() is created."""
        # Instance variables — unique to each instance
        self.owner = owner
        self._balance = initial_deposit    # _ prefix = private by convention
        self.transactions = []

        # Update class variable
        BankAccount._total_accounts += 1

        # Record opening deposit
        if initial_deposit > 0:
            self.transactions.append(("deposit", initial_deposit))

    # ─── INSTANCE METHODS ────────────────────────────────────────
    def deposit(self, amount: float) -> None:
        """Add money to the account."""
        if amount <= 0:
            raise ValueError("Deposit amount must be positive")
        self._balance += amount
        self.transactions.append(("deposit", amount))
        print(f"Deposited £{amount:.2f}. New balance: £{self._balance:.2f}")

    def withdraw(self, amount: float) -> None:
        """Remove money from the account."""
        if amount <= 0:
            raise ValueError("Withdrawal amount must be positive")
        if amount > self._balance:
            raise ValueError(f"Insufficient funds. Balance: £{self._balance:.2f}")
        self._balance -= amount
        self.transactions.append(("withdrawal", amount))
        print(f"Withdrew £{amount:.2f}. New balance: £{self._balance:.2f}")

    def get_statement(self) -> str:
        """Return a formatted account statement."""
        lines = [f"Account: {self.owner}", "-" * 30]
        for t_type, amount in self.transactions:
            lines.append(f"  {t_type.capitalize():15} £{amount:>8.2f}")
        lines.append("-" * 30)
        lines.append(f"  {'Balance':15} £{self._balance:>8.2f}")
        return "\n".join(lines)

    # ─── PROPERTY — controlled attribute access ──────────────────
    @property
    def balance(self) -> float:
        """Get the current balance (read-only)."""
        return self._balance

    # balance = 100   ← This would raise AttributeError (no setter defined)

    # ─── CLASS METHOD — operates on the class itself ─────────────
    @classmethod
    def get_total_accounts(cls) -> int:
        """Return the total number of accounts ever created."""
        return cls._total_accounts

    @classmethod
    def from_dict(cls, data: dict) -> "BankAccount":
        """Alternative constructor — create from a dictionary."""
        return cls(data["owner"], data.get("balance", 0))

    # ─── STATIC METHOD — utility, no access to class or instance ─
    @staticmethod
    def is_valid_amount(amount: float) -> bool:
        """Check if an amount is valid (positive number)."""
        return isinstance(amount, (int, float)) and amount > 0

    # ─── DUNDER (MAGIC) METHODS ──────────────────────────────────
    def __str__(self) -> str:
        """Called by str() and print() — human-readable."""
        return f"BankAccount({self.owner}, £{self._balance:.2f})"

    def __repr__(self) -> str:
        """Called by repr() — developer representation."""
        return f"BankAccount(owner={self.owner!r}, initial_deposit={self._balance})"

    def __len__(self) -> int:
        """Called by len() — return number of transactions."""
        return len(self.transactions)

    def __eq__(self, other: object) -> bool:
        """Called by == — compare by owner and balance."""
        if not isinstance(other, BankAccount):
            return NotImplemented
        return self.owner == other.owner and self._balance == other._balance

    def __lt__(self, other: "BankAccount") -> bool:
        """Called by < — compare by balance."""
        return self._balance < other._balance

    def __add__(self, other: "BankAccount") -> "BankAccount":
        """Called by + — merge two accounts."""
        new_balance = self._balance + other._balance
        return BankAccount(f"{self.owner}+{other.owner}", new_balance)
```

```python
# Using the class
account = BankAccount("Alice", 1000)
account.deposit(500)
account.withdraw(200)

print(account)             # BankAccount(Alice, £1300.00)
print(repr(account))       # BankAccount(owner='Alice', initial_deposit=1300.0)
print(len(account))        # 3 (transactions)
print(account.balance)     # 1300.0 (via property)
print(BankAccount.get_total_accounts())  # Class method
print(BankAccount.is_valid_amount(-5))   # False (static method)
print(account.get_statement())
```

---

### 14.3 Dataclasses — The Modern Way for Data

```python
from dataclasses import dataclass, field
from typing import List

@dataclass
class Product:
    """A product in an e-commerce system."""
    name: str
    price: float
    category: str
    tags: List[str] = field(default_factory=list)  # Mutable default

    # Computed at init (post-init)
    def __post_init__(self):
        if self.price < 0:
            raise ValueError("Price cannot be negative")
        self.price = round(self.price, 2)

    @property
    def price_with_tax(self) -> float:
        return round(self.price * 1.20, 2)

# Dataclasses auto-generate __init__, __repr__, __eq__
p1 = Product("Laptop", 999.99, "Electronics", ["tech", "portable"])
p2 = Product("Laptop", 999.99, "Electronics", ["tech", "portable"])

print(p1)             # Product(name='Laptop', price=999.99, ...)
print(p1 == p2)       # True  (__eq__ auto-generated)
print(p1.price_with_tax)  # 1199.99
```

---

---

## Lesson 15 — Inheritance and Polymorphism

> **Level:** Intermediate
> **Goal:** Model "is-a" relationships and write flexible code

---

### 15.1 Inheritance

```python
class Animal:
    """Base class for all animals."""
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    def eat(self) -> str:
        return f"{self.name} is eating"

    def sleep(self) -> str:
        return f"{self.name} is sleeping"

    def speak(self) -> str:
        raise NotImplementedError("Subclasses must implement speak()")

    def __str__(self) -> str:
        return f"{type(self).__name__}(name={self.name}, age={self.age})"


class Dog(Animal):
    """Dog inherits from Animal."""
    def __init__(self, name: str, age: int, breed: str):
        super().__init__(name, age)   # Call parent __init__
        self.breed = breed

    def speak(self) -> str:
        return f"{self.name} says: Woof!"

    def fetch(self, item: str) -> str:
        return f"{self.name} fetches the {item}"


class Cat(Animal):
    """Cat inherits from Animal."""
    def __init__(self, name: str, age: int, indoor: bool = True):
        super().__init__(name, age)
        self.indoor = indoor

    def speak(self) -> str:
        return f"{self.name} says: Meow!"

    def purr(self) -> str:
        return f"{self.name} purrs contentedly"
```

---

### 15.2 Polymorphism

```python
# Same method name, different behaviour based on object type
animals = [
    Dog("Rex", 3, "Labrador"),
    Cat("Whiskers", 5),
    Dog("Buddy", 1, "Poodle"),
]

for animal in animals:
    print(animal.speak())   # Each object responds differently
# Rex says: Woof!
# Whiskers says: Meow!
# Buddy says: Woof!

# isinstance and type checks
for animal in animals:
    if isinstance(animal, Dog):
        print(animal.fetch("ball"))   # Only dogs can fetch
    print(f"Is Animal: {isinstance(animal, Animal)}")  # True for all

# Duck typing — "if it walks like a duck and quacks like a duck..."
class Robot:
    def speak(self) -> str:
        return "Beep boop"

# Robot doesn't inherit from Animal but has speak()
things = [Dog("Rex", 3, "Lab"), Cat("W", 2), Robot()]
for thing in things:
    if hasattr(thing, "speak"):
        print(thing.speak())     # Works! Python doesn't care about type
```

---

### 15.3 Abstract Base Classes

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    """Abstract base class — cannot be instantiated directly."""

    @abstractmethod
    def area(self) -> float:
        """Calculate area — MUST be implemented by subclasses."""
        pass

    @abstractmethod
    def perimeter(self) -> float:
        """Calculate perimeter — MUST be implemented by subclasses."""
        pass

    def describe(self) -> str:
        """Concrete method — uses abstract methods."""
        return f"{type(self).__name__}: area={self.area():.2f}, perimeter={self.perimeter():.2f}"


class Circle(Shape):
    import math
    def __init__(self, radius: float):
        self.radius = radius

    def area(self) -> float:
        import math
        return math.pi * self.radius ** 2

    def perimeter(self) -> float:
        import math
        return 2 * math.pi * self.radius


class Rectangle(Shape):
    def __init__(self, width: float, height: float):
        self.width = width
        self.height = height

    def area(self) -> float:
        return self.width * self.height

    def perimeter(self) -> float:
        return 2 * (self.width + self.height)


# Shape()  ← TypeError: Can't instantiate abstract class
circle = Circle(5)
rect = Rectangle(4, 6)

shapes = [circle, rect]
for shape in shapes:
    print(shape.describe())
# Circle: area=78.54, perimeter=31.42
# Rectangle: area=24.00, perimeter=20.00
```

---

### 15.4 Multiple Inheritance and MRO

```python
class Flyable:
    def fly(self) -> str:
        return f"{self.__class__.__name__} is flying"

class Swimmable:
    def swim(self) -> str:
        return f"{self.__class__.__name__} is swimming"

class Duck(Animal, Flyable, Swimmable):
    def speak(self) -> str:
        return f"{self.name} says: Quack!"

donald = Duck("Donald", 3)
print(donald.speak())  # Donald says: Quack!
print(donald.fly())    # Duck is flying
print(donald.swim())   # Duck is swimming

# Method Resolution Order — how Python resolves method calls
print(Duck.__mro__)
# (Duck, Animal, Flyable, Swimmable, object)
```

---

---

## Lesson 16 — Decorators

> **Level:** Intermediate → Advanced
> **Goal:** Modify function and class behaviour without changing their code

---

### 16.1 Functions as First-Class Objects

```python
# In Python, functions are objects — they can be:
# - Assigned to variables
# - Passed as arguments
# - Returned from functions
# - Stored in data structures

def greet(name):
    return f"Hello, {name}"

# Assign to variable
say_hello = greet
print(say_hello("Alice"))    # "Hello, Alice"

# Pass as argument
def apply(func, value):
    return func(value)

print(apply(greet, "Bob"))   # "Hello, Bob"

# Return from function (closure)
def make_multiplier(factor):
    def multiply(number):
        return number * factor    # 'factor' captured from outer scope
    return multiply

double = make_multiplier(2)
triple = make_multiplier(3)
print(double(5))    # 10
print(triple(5))    # 15
```

---

### 16.2 Building a Decorator from Scratch

```python
import time
import functools

# A decorator is a function that takes a function and returns a function
def timer(func):
    """Decorator that measures how long a function takes to run."""
    @functools.wraps(func)   # Preserves func's metadata (__name__, __doc__)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = func(*args, **kwargs)    # Call the original function
        end = time.perf_counter()
        print(f"{func.__name__} took {end - start:.4f}s")
        return result
    return wrapper

# Apply decorator
@timer
def slow_function():
    time.sleep(1)
    return "Done"

# @timer above is equivalent to: slow_function = timer(slow_function)
slow_function()   # slow_function took 1.0012s
```

---

### 16.3 Practical Decorators

```python
import functools
import logging
import time

# ─── LOGGING DECORATOR ───────────────────────────────────────────
def log_calls(func):
    """Log every call to the function with its arguments and result."""
    logger = logging.getLogger(func.__module__)

    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        logger.info(f"Calling {func.__name__} with args={args}, kwargs={kwargs}")
        try:
            result = func(*args, **kwargs)
            logger.info(f"{func.__name__} returned {result}")
            return result
        except Exception as e:
            logger.error(f"{func.__name__} raised {type(e).__name__}: {e}")
            raise
    return wrapper

# ─── RETRY DECORATOR ─────────────────────────────────────────────
def retry(max_attempts=3, delay=1.0, exceptions=(Exception,)):
    """Retry a function on failure."""
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            last_error = None
            for attempt in range(1, max_attempts + 1):
                try:
                    return func(*args, **kwargs)
                except exceptions as e:
                    last_error = e
                    if attempt < max_attempts:
                        print(f"Attempt {attempt} failed: {e}. Retrying in {delay}s...")
                        time.sleep(delay)
            raise RuntimeError(f"All {max_attempts} attempts failed") from last_error
        return wrapper
    return decorator

@retry(max_attempts=3, delay=0.5)
def fetch_data(url: str):
    import random
    if random.random() < 0.7:
        raise ConnectionError("Network error")
    return "Data fetched!"

# ─── CACHE DECORATOR ─────────────────────────────────────────────
from functools import lru_cache

@lru_cache(maxsize=128)   # Built-in — caches results
def fibonacci(n: int) -> int:
    if n < 2:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(40))   # Instant — results are cached

# ─── VALIDATE TYPES DECORATOR ────────────────────────────────────
def validate_types(**type_map):
    """Validate argument types at runtime."""
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            import inspect
            params = list(inspect.signature(func).parameters.keys())
            for i, (arg, param) in enumerate(zip(args, params)):
                if param in type_map and not isinstance(arg, type_map[param]):
                    raise TypeError(
                        f"Argument '{param}' must be {type_map[param].__name__}, "
                        f"got {type(arg).__name__}"
                    )
            return func(*args, **kwargs)
        return wrapper
    return decorator

@validate_types(name=str, age=int)
def create_user(name: str, age: int):
    return {"name": name, "age": age}

create_user("Alice", 28)      # Works
# create_user(123, 28)        # TypeError: Argument 'name' must be str, got int
```

---

---

## Lesson 17 — Iterators and Generators

> **Level:** Intermediate → Advanced
> **Goal:** Work with sequences lazily and memory-efficiently

---

### 17.1 Iterators — The Protocol

```python
# Everything you loop over in Python is an iterable
# iter() creates an iterator, next() gets the next value

my_list = [1, 2, 3]
iterator = iter(my_list)    # Create iterator

print(next(iterator))  # 1
print(next(iterator))  # 2
print(next(iterator))  # 3
# next(iterator)         # StopIteration exception — no more items

# A for loop is syntactic sugar for this exact pattern:
for item in my_list:        # Python internally calls iter() and next()
    print(item)

# Build a custom iterator class
class CountDown:
    """Iterator that counts down from n to 1."""
    def __init__(self, start: int):
        self.current = start

    def __iter__(self):
        return self    # The iterator object IS self

    def __next__(self):
        if self.current <= 0:
            raise StopIteration
        value = self.current
        self.current -= 1
        return value

for n in CountDown(5):
    print(n, end=" ")  # 5 4 3 2 1
```

---

### 17.2 Generators — Lazy Evaluation

```python
# A generator function uses yield instead of return
# It produces values one at a time, on demand (lazy)
# This means it doesn't compute or store all values upfront

def count_up(start: int, stop: int, step: int = 1):
    """Generator that yields integers from start to stop."""
    current = start
    while current < stop:
        yield current         # Pause here, return value, resume later
        current += step

gen = count_up(0, 5)
print(type(gen))              # <class 'generator'>
print(next(gen))              # 0
print(next(gen))              # 1
print(list(count_up(0, 5)))   # [0, 1, 2, 3, 4]

# Compare memory usage:
# List — stores ALL values in memory at once
big_list = [x ** 2 for x in range(10_000_000)]   # Uses ~400MB!

# Generator — computes values one at a time
def squares_gen(n):
    for i in range(n):
        yield i ** 2

big_gen = squares_gen(10_000_000)   # Uses < 1KB! (just the generator object)
# Values are computed only when requested


# ─── GENERATOR EXPRESSIONS ───────────────────────────────────────
# Like list comprehensions but lazy (use parentheses)
gen_expr = (x ** 2 for x in range(1_000_000))   # Lazy — no computation yet
total = sum(gen_expr)    # Computes as needed

# Very useful for processing large data
def read_large_file(filename):
    """Read a file line by line without loading it all into memory."""
    with open(filename) as f:
        for line in f:
            yield line.strip()

# Process a 10GB log file:
for line in read_large_file("massive_log.txt"):
    if "ERROR" in line:
        print(line)   # Process one line at a time — constant memory usage


# ─── ADVANCED GENERATOR PATTERNS ─────────────────────────────────
def fibonacci_gen():
    """Infinite Fibonacci sequence generator."""
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

# Take first 10 Fibonacci numbers
fib = fibonacci_gen()
first_10 = [next(fib) for _ in range(10)]
print(first_10)   # [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]

# itertools.islice — take n items from any iterator
import itertools
first_20 = list(itertools.islice(fibonacci_gen(), 20))

# Generator pipeline — chain generators together
def read_lines(filename):
    with open(filename) as f:
        yield from f                      # yield from delegates to another iterable

def filter_errors(lines):
    for line in lines:
        if "ERROR" in line:
            yield line

def parse_error(lines):
    for line in lines:
        yield line.strip().split(" ", 3)  # Parse each error line

# Chain them
pipeline = parse_error(filter_errors(read_lines("app.log")))
for timestamp, level, service, message in pipeline:
    print(f"[{timestamp}] {service}: {message}")
```

---

---

## Lesson 18 — Practice Project — Contact Book App

> **Level:** Intermediate
> **Goal:** Build a full OOP application combining Lessons 11–17

---

### 18.1 Project Design

```python
# contact_book/
# ├── __init__.py
# ├── models.py       ← Contact class
# ├── storage.py      ← File persistence
# ├── validator.py    ← Input validation
# └── main.py         ← CLI interface
```

---

### 18.2 Complete Implementation

```python
# models.py
from dataclasses import dataclass, field
from datetime import datetime
from typing import List, Optional

@dataclass
class Contact:
    """Represents a contact in the address book."""
    name: str
    phone: str
    email: str
    tags: List[str] = field(default_factory=list)
    notes: str = ""
    created_at: str = field(default_factory=lambda: datetime.now().isoformat())

    def matches(self, query: str) -> bool:
        """Return True if contact matches the search query."""
        query = query.lower()
        return (
            query in self.name.lower() or
            query in self.phone or
            query in self.email.lower() or
            any(query in tag.lower() for tag in self.tags)
        )

    def to_dict(self) -> dict:
        return {
            "name": self.name,
            "phone": self.phone,
            "email": self.email,
            "tags": self.tags,
            "notes": self.notes,
            "created_at": self.created_at,
        }

    @classmethod
    def from_dict(cls, data: dict) -> "Contact":
        return cls(**data)

    def __str__(self) -> str:
        tags = f" [{', '.join(self.tags)}]" if self.tags else ""
        return f"{self.name} | {self.phone} | {self.email}{tags}"
```

```python
# storage.py
import json
from pathlib import Path
from typing import List
from .models import Contact

class ContactStorage:
    """Handles loading and saving contacts to a JSON file."""

    def __init__(self, filepath: str = "contacts.json"):
        self.path = Path(filepath)

    def load(self) -> List[Contact]:
        """Load contacts from file. Returns empty list if file doesn't exist."""
        if not self.path.exists():
            return []
        try:
            data = json.loads(self.path.read_text(encoding="utf-8"))
            return [Contact.from_dict(c) for c in data]
        except (json.JSONDecodeError, KeyError) as e:
            raise RuntimeError(f"Failed to load contacts: {e}") from e

    def save(self, contacts: List[Contact]) -> None:
        """Save contacts to file."""
        data = [c.to_dict() for c in contacts]
        self.path.write_text(
            json.dumps(data, indent=2, ensure_ascii=False),
            encoding="utf-8"
        )
```

```python
# main.py
import sys
from models import Contact
from storage import ContactStorage

class ContactBook:
    """Main application class."""

    def __init__(self, storage_path: str = "contacts.json"):
        self.storage = ContactStorage(storage_path)
        self.contacts: list = self.storage.load()

    def add(self, name: str, phone: str, email: str,
            tags: list = None, notes: str = "") -> Contact:
        """Add a new contact."""
        contact = Contact(
            name=name, phone=phone, email=email,
            tags=tags or [], notes=notes
        )
        self.contacts.append(contact)
        self.storage.save(self.contacts)
        return contact

    def search(self, query: str) -> list:
        """Find contacts matching query."""
        return [c for c in self.contacts if c.matches(query)]

    def delete(self, name: str) -> bool:
        """Delete contact by name. Returns True if found and deleted."""
        before = len(self.contacts)
        self.contacts = [c for c in self.contacts if c.name.lower() != name.lower()]
        if len(self.contacts) < before:
            self.storage.save(self.contacts)
            return True
        return False

    def list_all(self) -> list:
        return sorted(self.contacts, key=lambda c: c.name.lower())

def main():
    book = ContactBook()
    commands = {
        "add":    "Add a new contact",
        "search": "Search contacts",
        "list":   "List all contacts",
        "delete": "Delete a contact",
        "quit":   "Exit",
    }

    print("=== Contact Book ===")
    while True:
        print("\nCommands:", " | ".join(commands.keys()))
        cmd = input("> ").strip().lower()

        if cmd == "quit":
            print("Goodbye!")
            break
        elif cmd == "list":
            contacts = book.list_all()
            if not contacts:
                print("No contacts yet.")
            else:
                for i, c in enumerate(contacts, 1):
                    print(f"{i:3}. {c}")
        elif cmd == "add":
            name  = input("Name: ").strip()
            phone = input("Phone: ").strip()
            email = input("Email: ").strip()
            tags  = input("Tags (comma-separated, optional): ").strip()
            tags  = [t.strip() for t in tags.split(",") if t.strip()]
            c = book.add(name, phone, email, tags)
            print(f"Added: {c}")
        elif cmd == "search":
            query = input("Search query: ").strip()
            results = book.search(query)
            if not results:
                print(f"No contacts matching '{query}'")
            else:
                for c in results:
                    print(f"  {c}")
        elif cmd == "delete":
            name = input("Name to delete: ").strip()
            if book.delete(name):
                print(f"Deleted '{name}'")
            else:
                print(f"Contact '{name}' not found")
        else:
            print(f"Unknown command '{cmd}'")

if __name__ == "__main__":
    main()
```

```bash
python3 main.py
```

---

### 18.3 Phase 2 Quiz

**Q1.** What is the difference between `__str__` and `__repr__`?

<details>
<summary>Answer</summary>

`__str__` is for human-readable output — what `print(obj)` displays. It should be readable and descriptive.

`__repr__` is for developer/debugging output — what `repr(obj)` and the REPL display. It should ideally be valid Python code that could recreate the object.

Rule of thumb: implement `__repr__` in all classes you write. Only add `__str__` if you want a different (more user-friendly) display.

</details>

---

**Q2.** When would you use a generator instead of a list?

<details>
<summary>Answer</summary>

Use a generator when:
1. The sequence is very large or infinite — you can't or don't want to hold all values in memory at once
2. You might not need all values — if processing can stop early, generators don't compute the rest
3. Values are expensive to compute — lazy evaluation only computes what's needed
4. You're building a pipeline — generators chain together without intermediate storage

Use a list when:
- You need to access elements by index
- You need to iterate multiple times
- The sequence is small and you need all values immediately

</details>


---

---

# PHASE 3 — ADVANCED

---

## Lesson 19 — Multithreading and Multiprocessing

> **Level:** Advanced
> **Goal:** Run tasks concurrently to improve performance

---

### 19.1 Concurrency vs Parallelism vs Async

```
CONCURRENCY:  Multiple tasks in progress at the same time
              (not necessarily simultaneously — could be interleaved)

PARALLELISM:  Multiple tasks executing simultaneously
              (requires multiple CPU cores)

ASYNC:        Single thread handles multiple tasks by not waiting
              (waiting time is used for other work)

Python's choices:
  I/O-bound tasks  → threading OR async (both work, async is more modern)
  CPU-bound tasks  → multiprocessing (bypass the GIL)
```

**The GIL (Global Interpreter Lock):**
CPython (standard Python) has a GIL — a mutex that allows only one thread to execute Python bytecode at a time. This means:
- Multiple threads CAN run concurrently for I/O-bound tasks (file I/O, network — GIL released during I/O)
- Multiple threads CANNOT truly parallelise CPU-bound tasks
- Solution for CPU-bound: multiprocessing (separate processes = separate GILs)

---

### 19.2 Threading — I/O-Bound Concurrency

```python
import threading
import time
import requests
from concurrent.futures import ThreadPoolExecutor, as_completed

# ─── BASIC THREADING ─────────────────────────────────────────────
def download_page(url: str, results: dict) -> None:
    """Download a URL and store the result."""
    print(f"Downloading: {url}")
    # Simulated network request
    time.sleep(1)
    results[url] = f"Content from {url}"
    print(f"Done: {url}")

urls = [
    "https://example.com/page1",
    "https://example.com/page2",
    "https://example.com/page3",
]
results = {}

# Sequential: takes 3 seconds
start = time.perf_counter()
for url in urls:
    download_page(url, results)
print(f"Sequential: {time.perf_counter() - start:.2f}s")   # ~3.0s

# Threaded: takes ~1 second (all three run concurrently)
results = {}
threads = []
start = time.perf_counter()
for url in urls:
    t = threading.Thread(target=download_page, args=(url, results))
    threads.append(t)
    t.start()

for t in threads:
    t.join()   # Wait for all threads to complete

print(f"Threaded: {time.perf_counter() - start:.2f}s")   # ~1.0s

# ─── THREADPOOLEXECUTOR — The Modern Way ─────────────────────────
def fetch_url(url: str) -> dict:
    """Fetch a URL and return result dict."""
    time.sleep(1)   # Simulate I/O
    return {"url": url, "status": 200, "content": "page content"}

with ThreadPoolExecutor(max_workers=5) as executor:
    # Submit all tasks
    futures = {executor.submit(fetch_url, url): url for url in urls}

    # Process results as they complete
    for future in as_completed(futures):
        url = futures[future]
        try:
            result = future.result()
            print(f"Completed: {result['url']}")
        except Exception as e:
            print(f"Failed {url}: {e}")

# map() — simpler when you just want results in order
with ThreadPoolExecutor(max_workers=5) as executor:
    results = list(executor.map(fetch_url, urls))

# ─── THREAD SAFETY — Locks ────────────────────────────────────────
counter = 0
lock = threading.Lock()

def increment_counter():
    global counter
    # Without lock: race condition — counter value is unpredictable
    with lock:              # Only one thread can be here at a time
        current = counter
        time.sleep(0.001)   # Simulate work
        counter = current + 1

threads = [threading.Thread(target=increment_counter) for _ in range(100)]
for t in threads:
    t.start()
for t in threads:
    t.join()
print(f"Counter: {counter}")   # Always 100 with lock; < 100 without
```

---

### 19.3 Multiprocessing — CPU-Bound Parallelism

```python
import multiprocessing
from concurrent.futures import ProcessPoolExecutor
import time

def cpu_intensive(n: int) -> int:
    """CPU-bound function — calculate sum of squares."""
    return sum(i ** 2 for i in range(n))

numbers = [10_000_000, 8_000_000, 12_000_000, 9_000_000]

# Sequential: uses 1 core
start = time.perf_counter()
results = [cpu_intensive(n) for n in numbers]
print(f"Sequential: {time.perf_counter() - start:.2f}s")

# Multiprocessing: uses all cores
start = time.perf_counter()
with ProcessPoolExecutor(max_workers=multiprocessing.cpu_count()) as executor:
    results = list(executor.map(cpu_intensive, numbers))
print(f"Parallel: {time.perf_counter() - start:.2f}s")
# ~4x faster on a 4-core machine!

# IMPORTANT: Must guard with __name__ == "__main__" on Windows/macOS
if __name__ == "__main__":
    with ProcessPoolExecutor() as executor:
        futures = [executor.submit(cpu_intensive, n) for n in numbers]
        results = [f.result() for f in futures]
```

---

---

## Lesson 20 — Async Programming

> **Level:** Advanced
> **Goal:** Handle thousands of concurrent I/O operations efficiently

---

### 20.1 Why Async?

Threading works for concurrent I/O but has overhead: each thread uses ~8MB of RAM and OS context switching is expensive. For 10,000 concurrent connections, that's 80GB of RAM for threads alone.

Async (asyncio) uses a single thread with an event loop. When one task is waiting (for network, disk, etc.), the event loop switches to another task. No OS context switching, minimal memory overhead.

**Rule of thumb:**
- Thousands of concurrent I/O operations → asyncio
- Dozens of concurrent I/O operations → threading is fine
- CPU-bound work → multiprocessing

---

### 20.2 asyncio Fundamentals

```python
import asyncio
import aiohttp   # pip install aiohttp — async HTTP client
import time

# async def defines a coroutine — doesn't run until awaited
async def say_hello(name: str, delay: float) -> str:
    print(f"Hello, {name}! Waiting {delay}s...")
    await asyncio.sleep(delay)   # Non-blocking wait (releases event loop)
    print(f"Goodbye, {name}!")
    return f"Done with {name}"

# Running a single coroutine
result = asyncio.run(say_hello("Alice", 1))

# Running multiple coroutines CONCURRENTLY
async def main():
    # gather — run all concurrently, wait for all to finish
    start = time.perf_counter()
    results = await asyncio.gather(
        say_hello("Alice", 1),
        say_hello("Bob", 2),
        say_hello("Charlie", 1.5),
    )
    elapsed = time.perf_counter() - start
    print(f"All done in {elapsed:.2f}s")  # ~2.0s (not 4.5s!)
    return results

asyncio.run(main())
```

---

### 20.3 Async HTTP Requests — Real-World Example

```python
import asyncio
import aiohttp
import time

async def fetch_url(session: aiohttp.ClientSession, url: str) -> dict:
    """Async HTTP GET request."""
    async with session.get(url) as response:
        content = await response.text()
        return {
            "url": url,
            "status": response.status,
            "length": len(content),
        }

async def fetch_all(urls: list) -> list:
    """Fetch all URLs concurrently."""
    async with aiohttp.ClientSession() as session:
        tasks = [fetch_url(session, url) for url in urls]
        return await asyncio.gather(*tasks, return_exceptions=True)

urls = [
    "https://httpbin.org/delay/1",
    "https://httpbin.org/delay/1",
    "https://httpbin.org/delay/1",
]

# Sequential: ~3 seconds
# Async: ~1 second
start = time.perf_counter()
results = asyncio.run(fetch_all(urls))
print(f"Fetched {len(results)} URLs in {time.perf_counter() - start:.2f}s")
```

---

### 20.4 Async Context Managers and Generators

```python
import asyncio

# Async context manager
class AsyncDatabaseConnection:
    async def __aenter__(self):
        print("Connecting to database...")
        await asyncio.sleep(0.1)   # Simulate connection
        return self

    async def __aexit__(self, exc_type, exc_val, exc_tb):
        print("Closing database connection...")
        await asyncio.sleep(0.05)
        return False   # Don't suppress exceptions

    async def query(self, sql: str) -> list:
        await asyncio.sleep(0.01)   # Simulate query
        return [{"id": 1, "name": "Alice"}]

async def main():
    async with AsyncDatabaseConnection() as db:
        results = await db.query("SELECT * FROM users")
        print(results)

# Async generator
async def async_range(start: int, stop: int, delay: float = 0):
    for i in range(start, stop):
        await asyncio.sleep(delay)
        yield i

async def main():
    async for i in async_range(0, 5, delay=0.1):
        print(i)

asyncio.run(main())
```

---

---

## Lesson 21 — Logging

> **Level:** Advanced
> **Goal:** Replace print() with professional logging

---

### 21.1 Why Logging Matters

`print()` for debugging has problems:
- No timestamps — you don't know when something happened
- No severity levels — a debug message looks the same as a critical error
- No easy way to disable debug output in production
- Can't easily send logs to files, databases, or monitoring services

---

### 21.2 The Logging Module

```python
import logging
import sys
from pathlib import Path

# ─── BASIC SETUP ────────────────────────────────────────────────
# Five levels (lowest to highest): DEBUG, INFO, WARNING, ERROR, CRITICAL
logging.basicConfig(level=logging.DEBUG)
logging.debug("Detailed diagnostic information")
logging.info("General information — things are working")
logging.warning("Something unexpected but not fatal")
logging.error("A serious error — some functionality failed")
logging.critical("Critical error — system may crash")

# ─── PRODUCTION SETUP ────────────────────────────────────────────
def setup_logging(
    app_name: str,
    log_level: str = "INFO",
    log_file: str = None,
) -> logging.Logger:
    """Configure logging for production applications."""
    logger = logging.getLogger(app_name)
    logger.setLevel(getattr(logging, log_level.upper()))

    # Formatter — what each log line looks like
    formatter = logging.Formatter(
        fmt="%(asctime)s | %(levelname)-8s | %(name)s | %(funcName)s:%(lineno)d | %(message)s",
        datefmt="%Y-%m-%d %H:%M:%S",
    )

    # Console handler — log to stdout
    console_handler = logging.StreamHandler(sys.stdout)
    console_handler.setLevel(logging.DEBUG)
    console_handler.setFormatter(formatter)
    logger.addHandler(console_handler)

    # File handler — log to rotating file
    if log_file:
        from logging.handlers import RotatingFileHandler
        file_handler = RotatingFileHandler(
            log_file,
            maxBytes=10 * 1024 * 1024,  # 10MB per file
            backupCount=5,               # Keep 5 rotated files
            encoding="utf-8",
        )
        file_handler.setLevel(logging.INFO)
        file_handler.setFormatter(formatter)
        logger.addHandler(file_handler)

    return logger

# Usage
logger = setup_logging("myapp", log_level="DEBUG", log_file="app.log")
logger.info("Application started")
logger.debug(f"Config loaded: port=8080")
logger.warning("Database connection pool is 80% full")
logger.error("Failed to process request", exc_info=True)   # Include traceback

# Per-module loggers — best practice in large applications
# In each module:
logger = logging.getLogger(__name__)  # e.g., "myapp.services.user"
# Root configuration propagates to all child loggers
```

---

---

## Lesson 22 — Testing with PyTest

> **Level:** Advanced
> **Goal:** Write professional automated tests

---

### 22.1 Why Tests?

- **Catch bugs before they reach users** — automated checks run on every change
- **Enable confident refactoring** — change code without fear if tests pass
- **Document behaviour** — tests show how code is supposed to work
- **Save debugging time** — a failing test points directly to the problem

---

### 22.2 PyTest Fundamentals

```bash
pip install pytest pytest-cov
```

```python
# test_calculator.py
# PyTest discovers files named test_*.py or *_test.py
# Test functions start with test_

def add(a, b):
    return a + b

def divide(a, b):
    if b == 0:
        raise ValueError("Cannot divide by zero")
    return a / b

# ─── BASIC TESTS ──────────────────────────────────────────────────
def test_add_positive_numbers():
    assert add(2, 3) == 5

def test_add_negative_numbers():
    assert add(-1, -2) == -3

def test_add_with_zero():
    assert add(0, 5) == 5

def test_divide_normal():
    assert divide(10, 2) == 5.0

def test_divide_by_zero():
    import pytest
    with pytest.raises(ValueError, match="Cannot divide by zero"):
        divide(10, 0)

def test_divide_returns_float():
    result = divide(7, 2)
    assert isinstance(result, float)
    assert result == 3.5
```

```bash
# Run tests
pytest
pytest -v                    # Verbose: show each test name
pytest -v test_calculator.py # Run specific file
pytest -k "add"              # Run tests with "add" in name
pytest --tb=short            # Short traceback on failure
pytest --cov=. --cov-report=html  # Coverage report
```

---

### 22.3 Fixtures — Shared Test Setup

```python
import pytest
from contact_book import ContactBook, Contact

# Fixture: shared setup code, injected into tests that need it
@pytest.fixture
def empty_book(tmp_path):
    """Provide a fresh ContactBook for each test."""
    return ContactBook(storage_path=str(tmp_path / "test_contacts.json"))

@pytest.fixture
def populated_book(empty_book):
    """ContactBook with sample data."""
    empty_book.add("Alice", "555-0001", "alice@example.com", tags=["friend"])
    empty_book.add("Bob", "555-0002", "bob@example.com", tags=["work"])
    empty_book.add("Charlie", "555-0003", "charlie@example.com", tags=["friend", "work"])
    return empty_book

# Tests use fixtures by name
def test_add_contact(empty_book):
    contact = empty_book.add("Alice", "555-1234", "alice@test.com")
    assert contact.name == "Alice"
    assert len(empty_book.list_all()) == 1

def test_search_by_name(populated_book):
    results = populated_book.search("Alice")
    assert len(results) == 1
    assert results[0].name == "Alice"

def test_search_by_tag(populated_book):
    results = populated_book.search("friend")
    assert len(results) == 2
    names = {c.name for c in results}
    assert names == {"Alice", "Charlie"}

def test_delete_existing(populated_book):
    result = populated_book.delete("Alice")
    assert result is True
    assert len(populated_book.list_all()) == 2

def test_delete_missing(populated_book):
    result = populated_book.delete("Nonexistent")
    assert result is False
    assert len(populated_book.list_all()) == 3
```

---

### 22.4 Parametrize and Mocking

```python
import pytest
from unittest.mock import MagicMock, patch

# ─── PARAMETRIZE — run one test with multiple inputs ──────────────
@pytest.mark.parametrize("email,expected", [
    ("alice@example.com", True),
    ("bob@test.co.uk", True),
    ("notanemail", False),
    ("@example.com", False),
    ("alice@", False),
    ("", False),
])
def test_email_validation(email, expected):
    from validator import is_valid_email
    assert is_valid_email(email) == expected

# ─── MOCKING — replace real dependencies with fake ones ───────────
from api_client import fetch_user

def test_fetch_user_success():
    mock_response = MagicMock()
    mock_response.status_code = 200
    mock_response.json.return_value = {"id": 1, "name": "Alice"}

    with patch("api_client.requests.get", return_value=mock_response):
        user = fetch_user(1)
        assert user["name"] == "Alice"

def test_fetch_user_not_found():
    mock_response = MagicMock()
    mock_response.status_code = 404

    with patch("api_client.requests.get", return_value=mock_response):
        with pytest.raises(ValueError, match="User 99 not found"):
            fetch_user(99)
```

---

---

## Lesson 23 — REST APIs with FastAPI

> **Level:** Advanced
> **Goal:** Build production-grade REST APIs

---

### 23.1 FastAPI Introduction

```bash
pip install fastapi uvicorn[standard] pydantic
```

FastAPI is a modern Python web framework for building APIs:
- **Fast** — comparable to Node.js and Go in benchmarks
- **Automatic docs** — generates OpenAPI (Swagger) docs automatically
- **Type-safe** — uses Python type hints for validation
- **Async** — built on asyncio for high concurrency

---

### 23.2 Complete FastAPI Application

```python
# main.py — Production FastAPI API
from fastapi import FastAPI, HTTPException, Depends, status, Query
from fastapi.middleware.cors import CORSMiddleware
from pydantic import BaseModel, EmailStr, validator, Field
from typing import List, Optional
from datetime import datetime
import uuid

# ─── MODELS (Pydantic validates automatically) ────────────────────
class ContactCreate(BaseModel):
    name: str = Field(..., min_length=1, max_length=100)
    phone: str = Field(..., pattern=r"^\+?[\d\s\-()]{7,20}$")
    email: EmailStr
    tags: List[str] = []
    notes: str = Field("", max_length=500)

    @validator("tags", each_item=True)
    def clean_tags(cls, tag):
        return tag.strip().lower()

class ContactUpdate(BaseModel):
    name: Optional[str] = Field(None, min_length=1, max_length=100)
    phone: Optional[str] = None
    email: Optional[EmailStr] = None
    tags: Optional[List[str]] = None
    notes: Optional[str] = None

class ContactResponse(BaseModel):
    id: str
    name: str
    phone: str
    email: str
    tags: List[str]
    notes: str
    created_at: datetime

    class Config:
        from_attributes = True

# ─── IN-MEMORY DATABASE (replace with real DB in production) ──────
fake_db: dict = {}

# ─── APP SETUP ────────────────────────────────────────────────────
app = FastAPI(
    title="Contact Book API",
    description="RESTful API for managing contacts",
    version="1.0.0",
    docs_url="/docs",       # Swagger UI
    redoc_url="/redoc",     # ReDoc UI
)

app.add_middleware(
    CORSMiddleware,
    allow_origins=["http://localhost:3000"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

# ─── ROUTES ───────────────────────────────────────────────────────

@app.get("/health")
async def health_check():
    """Health check endpoint for load balancers."""
    return {"status": "healthy", "timestamp": datetime.utcnow()}

@app.post("/contacts", response_model=ContactResponse, status_code=status.HTTP_201_CREATED)
async def create_contact(contact: ContactCreate):
    """Create a new contact."""
    contact_id = str(uuid.uuid4())
    new_contact = {
        "id": contact_id,
        "created_at": datetime.utcnow(),
        **contact.dict()
    }
    fake_db[contact_id] = new_contact
    return new_contact

@app.get("/contacts", response_model=List[ContactResponse])
async def list_contacts(
    q: Optional[str] = Query(None, description="Search query"),
    tag: Optional[str] = Query(None, description="Filter by tag"),
    skip: int = Query(0, ge=0),
    limit: int = Query(20, ge=1, le=100),
):
    """List contacts with optional search and pagination."""
    contacts = list(fake_db.values())

    if q:
        q_lower = q.lower()
        contacts = [
            c for c in contacts
            if q_lower in c["name"].lower() or
               q_lower in c["email"].lower() or
               q_lower in c.get("phone", "")
        ]
    if tag:
        contacts = [c for c in contacts if tag.lower() in c["tags"]]

    contacts.sort(key=lambda c: c["name"].lower())
    return contacts[skip : skip + limit]

@app.get("/contacts/{contact_id}", response_model=ContactResponse)
async def get_contact(contact_id: str):
    """Get a specific contact by ID."""
    if contact_id not in fake_db:
        raise HTTPException(
            status_code=status.HTTP_404_NOT_FOUND,
            detail=f"Contact {contact_id} not found"
        )
    return fake_db[contact_id]

@app.patch("/contacts/{contact_id}", response_model=ContactResponse)
async def update_contact(contact_id: str, update: ContactUpdate):
    """Partially update a contact."""
    if contact_id not in fake_db:
        raise HTTPException(status_code=404, detail="Contact not found")

    contact = fake_db[contact_id].copy()
    update_data = update.dict(exclude_unset=True)
    contact.update(update_data)
    fake_db[contact_id] = contact
    return contact

@app.delete("/contacts/{contact_id}", status_code=status.HTTP_204_NO_CONTENT)
async def delete_contact(contact_id: str):
    """Delete a contact."""
    if contact_id not in fake_db:
        raise HTTPException(status_code=404, detail="Contact not found")
    del fake_db[contact_id]
```

```bash
# Run the server
uvicorn main:app --reload

# Visit:
# http://localhost:8000/docs  ← Swagger UI (interactive)
# http://localhost:8000/redoc ← ReDoc documentation
```

---

---

## Lesson 24 — Performance Optimisation

> **Level:** Advanced
> **Goal:** Identify and fix Python performance bottlenecks

---

### 24.1 Profiling First — Measure Before Optimising

```python
# ─── cProfile — CPU profiling ────────────────────────────────────
import cProfile
import pstats

def my_program():
    result = []
    for i in range(100_000):
        result.append(str(i) + " squared is " + str(i**2))
    return result

# Profile it
profiler = cProfile.Profile()
profiler.enable()
my_program()
profiler.disable()

stats = pstats.Stats(profiler)
stats.sort_stats("cumulative")
stats.print_stats(10)   # Show top 10 functions by cumulative time

# ─── timeit — micro-benchmarking ────────────────────────────────
import timeit

# Compare string concatenation vs join
setup = "data = [str(i) for i in range(1000)]"

concat_time = timeit.timeit(
    'result = ""; \n[result := result + s for s in data]',
    setup=setup, number=1000
)
join_time = timeit.timeit(
    'result = "".join(data)',
    setup=setup, number=1000
)
print(f"Concat: {concat_time:.3f}s  Join: {join_time:.3f}s")
# Join is typically 10-50x faster!

# ─── memory_profiler ─────────────────────────────────────────────
# pip install memory-profiler
from memory_profiler import profile

@profile
def memory_heavy():
    big_list = [i ** 2 for i in range(1_000_000)]
    return sum(big_list)
```

---

### 24.2 Key Optimisation Techniques

```python
# ─── 1. Use built-ins and standard library (C implementations) ───
import time

nums = list(range(1_000_000))

# Slow: Python loop
start = time.perf_counter()
total = 0
for n in nums:
    total += n
print(f"Loop: {time.perf_counter() - start:.4f}s")

# Fast: built-in sum() (implemented in C)
start = time.perf_counter()
total = sum(nums)
print(f"sum(): {time.perf_counter() - start:.4f}s")   # ~10x faster

# ─── 2. List comprehensions > loops ───────────────────────────────
# Slow
result = []
for i in range(100_000):
    result.append(i ** 2)

# Fast (comprehension has less overhead)
result = [i ** 2 for i in range(100_000)]

# ─── 3. Generators for large data ─────────────────────────────────
# Memory-heavy (builds entire list first)
total = sum([i ** 2 for i in range(10_000_000)])

# Memory-efficient (computes values one at a time)
total = sum(i ** 2 for i in range(10_000_000))

# ─── 4. Set lookups O(1) vs list O(n) ─────────────────────────────
import random
haystack_list = list(range(1_000_000))
haystack_set  = set(haystack_list)
needle = random.randint(0, 999_999)

start = time.perf_counter()
_ = needle in haystack_list   # O(n) — checks each element
list_time = time.perf_counter() - start

start = time.perf_counter()
_ = needle in haystack_set    # O(1) — hash lookup
set_time = time.perf_counter() - start
print(f"List: {list_time:.6f}s  Set: {set_time:.6f}s")  # Set ~1000x faster!

# ─── 5. String building ────────────────────────────────────────────
# Slow: string concatenation is O(n²) — creates new string each time
result = ""
for i in range(10_000):
    result += str(i)   # Slow!

# Fast: join is O(n) — builds once at the end
result = "".join(str(i) for i in range(10_000))

# ─── 6. Cache expensive computations ──────────────────────────────
from functools import lru_cache

@lru_cache(maxsize=None)   # Cache all results
def expensive_calculation(n: int) -> int:
    if n < 2:
        return n
    return expensive_calculation(n-1) + expensive_calculation(n-2)

# ─── 7. NumPy for numerical work ──────────────────────────────────
import numpy as np

# Python: 0.5 seconds
nums = list(range(1_000_000))
start = time.perf_counter()
result = [x * 2 for x in nums]
print(f"Python: {time.perf_counter() - start:.4f}s")

# NumPy: 0.002 seconds (250x faster — C implementation)
arr = np.arange(1_000_000)
start = time.perf_counter()
result = arr * 2   # Vectorised — no Python loop
print(f"NumPy: {time.perf_counter() - start:.4f}s")
```

---

---

## Lesson 25 — Practice Project — REST API with Tests

```python
# Full project: FastAPI contacts API with PyTest test suite

# tests/test_api.py
import pytest
from fastapi.testclient import TestClient
from main import app

@pytest.fixture
def client():
    """FastAPI test client — no real server needed."""
    return TestClient(app)

@pytest.fixture
def sample_contact():
    return {
        "name": "Alice Smith",
        "phone": "+44 7700 900001",
        "email": "alice@example.com",
        "tags": ["friend", "tech"],
        "notes": "Met at conference",
    }

def test_health_check(client):
    response = client.get("/health")
    assert response.status_code == 200
    assert response.json()["status"] == "healthy"

def test_create_contact(client, sample_contact):
    response = client.post("/contacts", json=sample_contact)
    assert response.status_code == 201
    data = response.json()
    assert data["name"] == "Alice Smith"
    assert data["email"] == "alice@example.com"
    assert "id" in data
    assert "created_at" in data

def test_create_invalid_email(client):
    response = client.post("/contacts", json={
        "name": "Test", "phone": "555-0000", "email": "notanemail"
    })
    assert response.status_code == 422   # Validation error

def test_get_contact(client, sample_contact):
    create_response = client.post("/contacts", json=sample_contact)
    contact_id = create_response.json()["id"]

    get_response = client.get(f"/contacts/{contact_id}")
    assert get_response.status_code == 200
    assert get_response.json()["id"] == contact_id

def test_get_nonexistent_contact(client):
    response = client.get("/contacts/nonexistent-id")
    assert response.status_code == 404

def test_list_contacts(client, sample_contact):
    client.post("/contacts", json=sample_contact)
    response = client.get("/contacts")
    assert response.status_code == 200
    contacts = response.json()
    assert isinstance(contacts, list)
    assert len(contacts) >= 1

def test_search_contacts(client, sample_contact):
    client.post("/contacts", json=sample_contact)
    response = client.get("/contacts", params={"q": "Alice"})
    assert response.status_code == 200
    results = response.json()
    assert any(c["name"] == "Alice Smith" for c in results)

def test_delete_contact(client, sample_contact):
    create_response = client.post("/contacts", json=sample_contact)
    contact_id = create_response.json()["id"]

    delete_response = client.delete(f"/contacts/{contact_id}")
    assert delete_response.status_code == 204

    get_response = client.get(f"/contacts/{contact_id}")
    assert get_response.status_code == 404
```

```bash
# Run tests with coverage
pytest tests/ -v --cov=. --cov-report=term-missing
```

---

---

# PHASE 4 — EXPERT LEVEL

---

## Lesson 26 — Python Internals and Memory Management

> **Level:** Expert
> **Goal:** Understand how Python works under the hood

---

### 26.1 CPython Object Model

```python
import sys
import ctypes

# Every Python object has:
# - ob_refcnt: reference count
# - ob_type: pointer to type object

# Reference counting
a = [1, 2, 3]
print(sys.getrefcount(a))    # 2 (one for 'a', one for getrefcount argument)

b = a
print(sys.getrefcount(a))    # 3 (now also 'b' refers to it)

del b
print(sys.getrefcount(a))    # Back to 2

# Object identity
x = 256
y = 256
print(x is y)    # True — CPython caches integers -5 to 256

x = 1000
y = 1000
print(x is y)    # False — large integers not cached (in most contexts)

# Memory address
print(id(x))     # Memory address as integer
print(hex(id(x)))  # As hex
```

---

### 26.2 Memory Management

```python
import gc
import sys
import tracemalloc

# ─── GARBAGE COLLECTOR ────────────────────────────────────────────
# Python uses reference counting PLUS a cyclic garbage collector

# Cyclic reference — reference counting alone can't handle this
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None   # Will create a cycle

a = Node(1)
b = Node(2)
a.next = b
b.next = a    # Cycle! a → b → a

del a, b      # Reference counts go to 1, not 0 — wouldn't be collected
gc.collect()  # Cyclic GC finds and collects the cycle

# Check GC stats
print(gc.get_count())      # (generation0, generation1, generation2) counts
print(gc.get_threshold())  # When each generation is collected

# ─── MEMORY PROFILING ─────────────────────────────────────────────
tracemalloc.start()

# Code to profile
data = {i: str(i) for i in range(100_000)}

snapshot = tracemalloc.take_snapshot()
top_stats = snapshot.statistics("lineno")

print("Top memory consumers:")
for stat in top_stats[:5]:
    print(stat)

tracemalloc.stop()

# ─── SLOTS — Reduce memory per instance ───────────────────────────
class WithDict:
    """Normal class — each instance has a __dict__ (~200 bytes overhead)."""
    def __init__(self, x, y):
        self.x = x
        self.y = y

class WithSlots:
    """Slots class — no __dict__ (~50% less memory per instance)."""
    __slots__ = ["x", "y"]   # Pre-declare attributes
    def __init__(self, x, y):
        self.x = x
        self.y = y

# For 1 million objects:
normal = [WithDict(i, i*2) for i in range(1_000_000)]
slotted = [WithSlots(i, i*2) for i in range(1_000_000)]

print(sys.getsizeof(normal[0]))   # ~56 bytes (just the object shell)
# WithDict instances also have a __dict__ of ~200+ bytes
# Total per normal object: ~260 bytes
# Total per slot object: ~56 bytes → 4.5x less memory!
```

---

---

## Lesson 27 — Metaclasses

> **Level:** Expert
> **Goal:** Understand classes of classes — control class creation

---

### 27.1 Type — The Metaclass of All Classes

```python
# In Python, EVERYTHING is an object — including classes
print(type(42))          # <class 'int'>
print(type("hello"))     # <class 'str'>
print(type([1,2,3]))     # <class 'list'>

# Even classes are objects!
class MyClass:
    pass

print(type(MyClass))     # <class 'type'>
print(type(type))        # <class 'type'>  (type is its own metaclass!)

# type() can also CREATE classes dynamically:
# type(name, bases, namespace)
Dog = type("Dog", (object,), {
    "species": "Canis lupus familiaris",
    "bark": lambda self: "Woof!"
})

d = Dog()
print(d.bark())    # "Woof!"
print(Dog.species) # "Canis lupus familiaris"

# This is what happens when you write 'class Dog:' — Python calls type()
```

---

### 27.2 Custom Metaclasses

```python
# A metaclass controls how a class is created
class SingletonMeta(type):
    """Metaclass that ensures only one instance of a class exists."""
    _instances = {}

    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]

class Database(metaclass=SingletonMeta):
    def __init__(self, url: str):
        self.url = url
        print(f"Connecting to {url}")

db1 = Database("postgresql://localhost/mydb")   # Prints "Connecting..."
db2 = Database("postgresql://localhost/mydb")   # Does NOT print — returns same instance
print(db1 is db2)   # True


class ValidateMeta(type):
    """Metaclass that validates class attributes at definition time."""
    def __new__(mcs, name, bases, namespace):
        # Called when the class is CREATED (not instantiated)
        if "describe" not in namespace:
            raise TypeError(f"Class {name} must define a 'describe' method")
        return super().__new__(mcs, name, bases, namespace)

class ValidatedBase(metaclass=ValidateMeta):
    def describe(self):
        return "I am the base"

# This would raise TypeError at class definition:
# class BadClass(metaclass=ValidateMeta):
#     pass   # Missing describe() method!
```

---

---

## Lesson 28 — Design Patterns in Python

> **Level:** Expert
> **Goal:** Apply proven solutions to common software design problems

---

### 28.1 Creational Patterns

```python
# ─── SINGLETON ───────────────────────────────────────────────────
# (Shown via metaclass above — also common via module-level instance)

# ─── FACTORY ─────────────────────────────────────────────────────
from abc import ABC, abstractmethod

class Notification(ABC):
    @abstractmethod
    def send(self, message: str) -> None:
        pass

class EmailNotification(Notification):
    def __init__(self, address: str):
        self.address = address
    def send(self, message: str) -> None:
        print(f"Email to {self.address}: {message}")

class SMSNotification(Notification):
    def __init__(self, phone: str):
        self.phone = phone
    def send(self, message: str) -> None:
        print(f"SMS to {self.phone}: {message}")

class PushNotification(Notification):
    def __init__(self, device_id: str):
        self.device_id = device_id
    def send(self, message: str) -> None:
        print(f"Push to {self.device_id}: {message}")

def create_notification(type: str, **kwargs) -> Notification:
    """Factory function — creates correct type based on string."""
    types = {
        "email": EmailNotification,
        "sms": SMSNotification,
        "push": PushNotification,
    }
    if type not in types:
        raise ValueError(f"Unknown notification type: {type}")
    return types[type](**kwargs)

notifier = create_notification("email", address="alice@example.com")
notifier.send("Your order has shipped!")
```

---

### 28.2 Structural Patterns

```python
# ─── DECORATOR (design pattern, not @decorator syntax) ────────────
class TextFormatter:
    def format(self, text: str) -> str:
        return text

class BoldDecorator:
    def __init__(self, formatter):
        self._formatter = formatter
    def format(self, text: str) -> str:
        return f"<b>{self._formatter.format(text)}</b>"

class ItalicDecorator:
    def __init__(self, formatter):
        self._formatter = formatter
    def format(self, text: str) -> str:
        return f"<i>{self._formatter.format(text)}</i>"

text = TextFormatter()
bold = BoldDecorator(text)
bold_italic = ItalicDecorator(bold)

print(bold_italic.format("Hello"))   # <i><b>Hello</b></i>

# ─── OBSERVER ────────────────────────────────────────────────────
from typing import Callable, List

class EventEmitter:
    """Observer pattern — notify subscribers of events."""
    def __init__(self):
        self._handlers: dict[str, List[Callable]] = {}

    def on(self, event: str, handler: Callable) -> None:
        self._handlers.setdefault(event, []).append(handler)

    def emit(self, event: str, *args, **kwargs) -> None:
        for handler in self._handlers.get(event, []):
            handler(*args, **kwargs)

    def off(self, event: str, handler: Callable) -> None:
        if event in self._handlers:
            self._handlers[event].remove(handler)

# Usage
order_events = EventEmitter()

def on_order_placed(order_id, amount):
    print(f"Email: Order {order_id} placed for £{amount:.2f}")

def on_order_placed_analytics(order_id, amount):
    print(f"Analytics: Tracking order {order_id}")

order_events.on("order.placed", on_order_placed)
order_events.on("order.placed", on_order_placed_analytics)
order_events.emit("order.placed", "ORD-001", 99.99)
```

---

---

## Lesson 29 — Scalable Python Architecture

> **Level:** Expert
> **Goal:** Design Python systems that handle production load

---

### 29.1 Project Structure for Large Applications

```
myapp/
├── pyproject.toml          ← Project config, dependencies (modern standard)
├── src/
│   └── myapp/
│       ├── __init__.py
│       ├── main.py         ← Entry point
│       ├── config.py       ← Configuration management
│       ├── api/
│       │   ├── __init__.py
│       │   ├── routes/
│       │   │   ├── users.py
│       │   │   └── orders.py
│       │   └── middleware.py
│       ├── domain/
│       │   ├── models.py   ← Business entities
│       │   └── services.py ← Business logic
│       ├── infrastructure/
│       │   ├── database.py ← DB connection
│       │   └── cache.py    ← Redis connection
│       └── core/
│           ├── exceptions.py
│           └── logging.py
└── tests/
    ├── unit/
    ├── integration/
    └── conftest.py         ← Shared fixtures
```

---

### 29.2 Configuration Management

```python
# config.py — Environment-based configuration
from pydantic_settings import BaseSettings
from functools import lru_cache
from typing import Optional

class Settings(BaseSettings):
    """All configuration from environment variables."""
    # App settings
    app_name: str = "MyApp"
    debug: bool = False
    log_level: str = "INFO"

    # Database
    database_url: str
    db_pool_size: int = 5
    db_max_overflow: int = 10

    # Redis
    redis_url: str = "redis://localhost:6379"
    cache_ttl: int = 300

    # Security
    secret_key: str
    access_token_expire_minutes: int = 30

    class Config:
        env_file = ".env"         # Load from .env file
        env_file_encoding = "utf-8"
        case_sensitive = False

@lru_cache()
def get_settings() -> Settings:
    """Cached settings — reads env once."""
    return Settings()

# Usage
settings = get_settings()
print(settings.database_url)
```

---

---

## Lesson 30 — Debugging Complex Applications

> **Level:** Expert
> **Goal:** Find and fix bugs in production Python systems

---

### 30.1 The Debugging Toolkit

```python
# ─── pdb — Python Debugger ────────────────────────────────────────
import pdb

def complex_function(data):
    result = []
    for item in data:
        pdb.set_trace()   # Execution pauses here, drops into interactive debugger
        processed = process(item)
        result.append(processed)
    return result

# pdb commands:
# n (next)      — execute current line, stop at next
# s (step)      — step INTO function call
# c (continue)  — continue until next breakpoint
# l (list)      — show source code around current line
# p expr        — print expression value
# pp expr       — pretty-print expression
# b lineno      — set breakpoint at line
# w (where)     — show call stack
# q (quit)      — stop debugging

# Modern: use breakpoint() built-in (Python 3.7+)
def my_function():
    x = 42
    breakpoint()   # Same as pdb.set_trace() — can be overridden by env var
    return x

# ─── LOGGING-BASED DEBUGGING ──────────────────────────────────────
import logging
import functools

def trace(logger=None):
    """Decorator to trace function calls — great for debugging."""
    if logger is None:
        logger = logging.getLogger(__name__)

    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            logger.debug(f"CALL  {func.__qualname__}({args!r}, {kwargs!r})")
            try:
                result = func(*args, **kwargs)
                logger.debug(f"RETURN {func.__qualname__} → {result!r}")
                return result
            except Exception as e:
                logger.debug(f"RAISE  {func.__qualname__} → {type(e).__name__}: {e}")
                raise
        return wrapper
    return decorator

# ─── TRACEBACK ANALYSIS ───────────────────────────────────────────
import traceback

try:
    risky_code()
except Exception:
    print(traceback.format_exc())    # Full traceback as string
    traceback.print_exc()            # Print to stderr

# ─── Inspect Running Code ─────────────────────────────────────────
import inspect

def who_called_me():
    frame = inspect.currentframe()
    caller = frame.f_back
    print(f"Called from: {caller.f_code.co_filename}:{caller.f_lineno}")
    print(f"In function: {caller.f_code.co_name}")

# ─── PERFORMANCE DEBUGGING ────────────────────────────────────────
import cProfile
import io
import pstats

def profile_function(func, *args, **kwargs):
    """Profile a function and print results."""
    profiler = cProfile.Profile()
    profiler.enable()
    result = func(*args, **kwargs)
    profiler.disable()

    buf = io.StringIO()
    ps = pstats.Stats(profiler, stream=buf)
    ps.sort_stats("cumulative")
    ps.print_stats(20)
    print(buf.getvalue())
    return result
```

---

---

## Lesson 31 — Interview Preparation — Python Edition

> **Level:** Senior Engineer

---

### 31.1 Core Interview Questions — With Strong Answers

**Q: "Explain Python's GIL and its implications."**

> The GIL (Global Interpreter Lock) is a mutex in CPython that prevents multiple native threads from executing Python bytecodes simultaneously. This means even on a multi-core machine, Python's threads don't achieve true CPU parallelism. The GIL exists because CPython's memory management (reference counting) is not thread-safe — the GIL makes it so. The practical implications: threading works fine for I/O-bound tasks (the GIL is released during I/O waits), but for CPU-bound computation, threading doesn't help and can actually be slightly slower than sequential code due to GIL contention. For CPU-bound parallelism, use the `multiprocessing` module (separate processes, separate GILs) or consider NumPy/Cython operations which release the GIL.

---

**Q: "What is the difference between a list and a generator in Python?"**

> A list stores all elements in memory at once. A generator produces elements lazily — one at a time, on demand. When you write `[x**2 for x in range(1_000_000)]`, Python immediately computes all one million values and allocates memory for them. When you write `(x**2 for x in range(1_000_000))`, you get a generator object that uses a few hundred bytes regardless of size — values are computed only when requested via `next()`. Generators are ideal when: the sequence is large or infinite, you might not need all values (early termination), values are expensive to compute, or you're building processing pipelines. The trade-off: you can only iterate a generator once.

---

**Q: "How does Python's decorator syntax work?"**

> `@decorator` above a function is syntactic sugar for `func = decorator(func)`. A decorator is a higher-order function — it takes a function as input and returns a (usually enhanced) function as output. The `functools.wraps` decorator should always be used inside a decorator to preserve the wrapped function's `__name__`, `__doc__`, and other metadata. Decorators can also take arguments by adding an extra layer of nesting — the outer function takes the arguments and returns the actual decorator. Common uses: logging, timing, authentication checks, retry logic, caching (Python ships `functools.lru_cache`), input validation.

---

**Q: "What is the difference between `__init__` and `__new__`?"**

> `__new__` is the constructor — it creates and returns the new instance object. `__init__` is the initialiser — it receives the already-created instance and sets up its attributes. In normal use, you only override `__init__`. You override `__new__` when you need to control instance creation itself — for example, to implement the Singleton pattern (return the existing instance if one exists), to create instances of immutable types like tuples (since you can't modify them in `__init__`), or when subclassing immutable built-in types.

---

**Q: "How would you implement a thread-safe counter in Python?"**

> Use `threading.Lock` to synchronise access to the shared variable. Without a lock, two threads can both read the current value, both increment it, and both write the same result back — losing one increment. With a lock, only one thread can be inside the `with lock:` block at a time. Alternatively, use `threading.Semaphore` for counting resources or `queue.Queue` which is itself thread-safe and often the right tool for producer-consumer patterns.

---

### 31.2 Python Code Challenges

```python
# ─── CHALLENGE 1: Flatten a nested list ──────────────────────────
# Input: [[1, [2, 3]], [4, [5, [6]]]]
# Output: [1, 2, 3, 4, 5, 6]

def flatten(lst):
    result = []
    for item in lst:
        if isinstance(item, list):
            result.extend(flatten(item))
        else:
            result.append(item)
    return result

# Or with a generator:
def flatten_gen(lst):
    for item in lst:
        if isinstance(item, list):
            yield from flatten_gen(item)
        else:
            yield item

# ─── CHALLENGE 2: Find two numbers that sum to target ────────────
def two_sum(nums: list, target: int) -> tuple:
    """Return indices of two numbers that sum to target. O(n) time."""
    seen = {}   # value → index
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return (seen[complement], i)
        seen[num] = i
    return None

print(two_sum([2, 7, 11, 15], 9))   # (0, 1)

# ─── CHALLENGE 3: LRU Cache ───────────────────────────────────────
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.cache = OrderedDict()

    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1
        self.cache.move_to_end(key)    # Mark as recently used
        return self.cache[key]

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self.cache.move_to_end(key)
        self.cache[key] = value
        if len(self.cache) > self.capacity:
            self.cache.popitem(last=False)   # Remove LRU (first item)

cache = LRUCache(2)
cache.put(1, 1)
cache.put(2, 2)
print(cache.get(1))    # 1
cache.put(3, 3)        # Evicts key 2
print(cache.get(2))    # -1 (evicted)
```

---

### 31.3 Python Best Practices Checklist

```
□ Use virtual environments for every project
□ Use type hints on all function signatures
□ Write docstrings for all public functions and classes
□ Use dataclasses for simple data containers
□ Prefer f-strings over .format() and % formatting
□ Use pathlib instead of os.path for file operations
□ Use context managers (with) for resources (files, connections, locks)
□ Use specific exception types, never bare except:
□ Always use 'is' to check for None, not ==
□ Use list/dict/set comprehensions instead of loops where readable
□ Use generators for large data processing
□ Use functools.lru_cache for expensive pure functions
□ Use logging, not print(), in production code
□ Write tests before or alongside code, not after
□ Use pytest fixtures for test setup
□ Use ABC for interfaces (abstract base classes)
□ Follow PEP 8 style guide
□ Use black or ruff for automatic formatting
□ Pin dependencies in requirements.txt with versions
□ Handle exceptions at the right level — not too early, not too late
```

---

## Official Python Documentation Reference

| Topic | URL |
|---|---|
| Python Documentation | https://docs.python.org/3/ |
| Python Tutorial | https://docs.python.org/3/tutorial/ |
| Python Standard Library | https://docs.python.org/3/library/ |
| PyPI Package Index | https://pypi.org/ |
| Real Python Tutorials | https://realpython.com/ |
| FastAPI Documentation | https://fastapi.tiangolo.com/ |
| PyTest Documentation | https://docs.pytest.org/ |
| PEP 8 Style Guide | https://pep8.org/ |
| asyncio Documentation | https://docs.python.org/3/library/asyncio.html |
| Python Type Hints | https://docs.python.org/3/library/typing.html |

---

## Learning Path

```
Week 1–2:   Lessons 1–4   Python setup, variables, strings, numbers, operators
Week 3–4:   Lessons 5–6   Lists, tuples, sets, dictionaries
Week 5–6:   Lessons 7–9   Conditionals, loops, functions
Week 7:     Lesson 10     Project: CLI Calculator
Week 8–9:   Lessons 11–12 Modules, packages, file handling
Week 10–11: Lessons 13–15 Exceptions, OOP classes, inheritance
Week 12–13: Lessons 16–17 Decorators, generators
Week 14:    Lesson 18     Project: Contact Book App
Week 15–16: Lessons 19–20 Threading, multiprocessing, async
Week 17–18: Lessons 21–22 Logging, testing with PyTest
Week 19–20: Lesson 23     REST API with FastAPI
Week 21–22: Lesson 24     Performance optimisation
Week 23:    Lesson 25     Project: REST API with Tests
Week 24–25: Lessons 26–27 Python internals, metaclasses
Week 26–27: Lessons 28–29 Design patterns, scalable architecture
Week 28:    Lessons 30–31 Debugging, interview preparation
```

**Build Something Real:**
Create a complete Python application:
- REST API with FastAPI (CRUD operations on a real domain)
- PostgreSQL database with SQLAlchemy ORM
- PyTest test suite with >80% coverage
- Docker containerisation
- Configuration via environment variables
- Structured logging
- Input validation with Pydantic

Put it on GitHub. This is your portfolio proof-of-work.

---

*Built on: Official Python Documentation — https://docs.python.org/3/ | Real Python — https://realpython.com/ | Python PEPs*
