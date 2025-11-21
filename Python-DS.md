# Python Data Structures

This document will serve as a comprehensive guide and note-taking space for various data structures in Python.

## Python Lists

Lists are ordered, mutable (changeable) sequences of items. They are one of the most versatile data structures in Python and can hold items of different data types.

**Characteristics:**
- Ordered: Items have a defined order, and that order will not change.
- Changeable (Mutable): You can change, add, and remove items after the list has been created.
- Allows Duplicates: Lists can have items with the same value.

**Creating a List:**
```python
# Using square brackets
my_list = [1, 2, 3, "apple", "banana"]

# Using the list() constructor
another_list = list(("cherry", "date", 5))
```

### Common List Methods

Here are some frequently used methods for Python lists:

- **`append(item)`**: Adds an item to the end of the list.
  ```python
  my_list.append("orange") # my_list becomes [1, 2, 3, "apple", "banana", "orange"]
  ```

- **`extend(iterable)`**: Adds all the items of an iterable (like another list, tuple, set, or dictionary) to the end of the current list.
  ```python
  list1 = [1, 2]
  list2 = [3, 4]
  list1.extend(list2) # list1 becomes [1, 2, 3, 4]
  ```

  **Extending a List with Another List**

  **`extend([list_to_add])`**: Adds the entire `list_to_add` as a single element to the end of the original list. This results in a nested list.
  ```python
  list_a = [1, 2, 3]
  list_b = [4, 5]
  list_a.extend([list_b])
  Or 
  print(f"List after append: {list_a}")
  ```
  **Output:**
  ```
  List after append: [1, 2, 3, [4, 5]]
  ```


- **`insert(index, item)`**: Inserts an item at a specified index.
  ```python
  my_list.insert(1, "grape") # my_list becomes [1, "grape", 2, 3, "apple", "banana", "orange"]
  ```

- **`remove(item)`**: Removes the first occurrence of a specified item.
  ```python
  my_list.remove(2) # Removes 2 from the list
  ```

- **`pop(index)`**: Removes and returns the item at a specified index. If no index is provided, it removes and returns the last item.
  ```python
  popped_item = my_list.pop() # Removes and returns "orange"
  popped_item_at_index = my_list.pop(0) # Removes and returns 1
  ```

- **`del` statement**: The `del` statement is not a method, but a Python statement that can be used to remove an item at a specific index or to remove a slice of items.
  ```python
  my_list = ['a', 'b', 'c', 'd', 'e', 'f']
  
  # Remove the item at index 2
  del my_list[2] 
  # my_list is now ['a', 'b', 'd', 'e', 'f']
  
  # Remove the slice from index 1 to 3
  del my_list[1:3]
  # my_list is now ['a', 'e', 'f']
  ```

- **`clear()`**: Removes all items from the list, making it empty.
  ```python
  my_list.clear() # my_list becomes []
  ```

- **`index(item)`**: Returns the index of the first occurrence of a specified item. Raises a `ValueError` if the item is not found.
  ```python
  index_of_apple = my_list.index("apple") # Returns the index of "apple"
  ```

- **`count(item)`**: Returns the number of times a specified item appears in the list.
  ```python
  my_list = [1, 2, 2, 3, 2]
  count_of_2 = my_list.count(2) # Returns 3
  ```

- **`sort(key=None, reverse=False)`**: Sorts the list in ascending order by default.
  ```python
  numbers = [3, 1, 4, 1, 5, 9, 2]
  numbers.sort() # numbers becomes [1, 1, 2, 3, 4, 5, 9]
  numbers.sort(reverse=True) # numbers becomes [9, 5, 4, 3, 2, 1, 1]
  ```

- **`reverse()`**: Reverses the order of the elements in the list.
  ```python
  my_list = [1, 2, 3, 4]
  my_list.reverse() # my_list becomes [4, 3, 2, 1]
  ```

- **`copy()`**: Returns a shallow copy of the list.

  **Example with no nested items:**
  When a list contains only simple data types like numbers and strings (no nested lists or other objects), a shallow copy created by `copy()` behaves like a full, independent copy.
  ```python
  original_list = [1, 2, 3, 4, 5]
  copied_list = original_list.copy()

  print(f"Original list: {original_list}")
  print(f"Copied list: {copied_list}")

  # Modify the copied list
  copied_list[0] = 99

  print(f"Original list after modification: {original_list}")
  print(f"Copied list after modification: {copied_list}")

  # The original list remains unchanged.
  ```

  **Output:**
  ```
  Original list: [1, 2, 3, 4, 5]
  Copied list: [1, 2, 3, 4, 5]
  Original list after modification: [1, 2, 3, 4, 5]
  Copied list after modification: [99, 2, 3, 4, 5]
  ```

  **Example with nested items (Shallow Copy):**
  The `copy()` method creates a *shallow copy*. This means that for a list containing other objects (like nested lists), the `copy()` method does not create copies of those nested objects. Instead, it copies references to them.

  Consider a list of lists representing a matrix.

  ```python
  original_matrix = [[1, 2], [3, 4]]
  shallow_copied_matrix = original_matrix.copy()

  print(f"Original matrix: {original_matrix}")
  print(f"Shallow copied matrix: {shallow_copied_matrix}")

  # Modify an element in a nested list of the shallow copy
  shallow_copied_matrix[0][0] = 99

  print(f"Original matrix after shallow copy modification: {original_matrix}")
  print(f"Shallow copied matrix after modification: {shallow_copied_matrix}")

  # Notice that modifying the nested list in the shallow copy also affects the original!
  # This is because both lists refer to the same nested list objects.
  ```

  **Output:**
  ```
  Original matrix: [[1, 2], [3, 4]]
  Shallow copied matrix: [[1, 2], [3, 4]]
  Original matrix after shallow copy modification: [[99, 2], [3, 4]]
  Shallow copied matrix after modification: [[99, 2], [3, 4]]
  ```

  **Example with a mix of simple and nested items (Shallow Copy):**
  When a list contains both simple immutable types and mutable nested objects (like another list), a shallow copy will duplicate the simple types but only copy references to the nested objects.

  ```python
  original_mixed_list = [1, 'a', [10, 20]]
  shallow_copied_mixed_list = original_mixed_list.copy()

  print(f"Original mixed list: {original_mixed_list}")
  print(f"Shallow copied mixed list: {shallow_copied_mixed_list}")

  # Modify a simple item in the shallow copy
  shallow_copied_mixed_list[0] = 5

  # Modify a nested item in the shallow copy
  shallow_copied_mixed_list[2][0] = 100

  print(f"Original mixed list after modification: {original_mixed_list}")
  print(f"Shallow copied mixed list after modification: {shallow_copied_list}")

  # Observe that the simple item in the original list is unchanged,
  # but the nested list in the original is affected because it's a shared reference.
  ```

  **Output:**
  ```
  Original mixed list: [1, 'a', [10, 20]]
  Shallow copied mixed list: [1, 'a', [10, 20]]
  Original mixed list after modification: [1, 'a', [100, 20]]
  Shallow copied mixed list after modification: [5, 'a', [100, 20]]
  ```

### Deep Copy Example

To create a completely independent copy (deep copy), use the `copy` module's `deepcopy()` function:

```python
import copy

original_matrix = [[1, 2], [3, 4]]
deep_copied_matrix = copy.deepcopy(original_matrix)

print(f"Original matrix before deep copy modification: {original_matrix}")
print(f"Deep copied matrix before modification: {deep_copied_matrix}")

deep_copied_matrix[0][0] = 100

print(f"Original matrix after deep copy modification: {original_matrix}")
print(f"Deep copied matrix after modification: {deep_copied_matrix}")

# With deep copy, modifying the nested list in the copy does NOT affect the original.
```

**Output:**
```
Original matrix before deep copy modification: [[1, 2], [3, 4]]
Deep copied matrix before modification: [[1, 2], [3, 4]]
Original matrix after deep copy modification: [[1, 2], [3, 4]]
Deep copied matrix after modification: [[100, 2], [3, 4]]
```

## Python Lists vs. Arrays

While Python lists are often used to store collections of items, they are not the same as arrays found in other languages (like C++ or Java) or specialized array types in Python libraries (like NumPy arrays).

Here's a comparison:

| Feature            | Python List                                   | Traditional Array (e.g., C++, Java, or NumPy) |
| :----------------- | :-------------------------------------------- | :---------------------------------------------- |
| **Data Type**      | Can store items of different data types.      | Typically stores items of a single, uniform data type. |
| **Homogeneity**    | Heterogeneous (can mix types).                | Homogeneous (elements are of the same type).    |
| **Size**           | Dynamic; can grow and shrink in size.         | Static or fixed size (once declared, size is fixed, though some languages offer dynamic arrays). |
| **Memory Usage**   | Can be less memory-efficient due to storing type information for each element. | More memory-efficient as elements are stored contiguously and uniformly. |
| **Performance**    | Slower for numerical operations due to type checking and non-contiguous memory. | Faster for numerical operations, especially large datasets, due to contiguous memory and optimized operations. |
| **Functionality**  | General-purpose, rich set of built-in methods for various operations. | Often optimized for specific numerical or scientific computing tasks. |
| **Common Use**     | General-purpose collections, flexible data storage. | Numerical computing, image processing, scientific data. |

**When to use which:**

- **Use Python Lists** when you need a flexible, general-purpose collection that can store mixed data types and whose size can change dynamically. They are excellent for most common programming tasks.

- **Use `array.array` (from Python's `array` module)** when you need a list-like structure that stores items of a single, basic C-type (e.g., integers, floats) and you are concerned about memory efficiency or performance for large sequences of homogeneous data.

- **Use NumPy Arrays** (from the `numpy` library) when performing advanced numerical and scientific computing tasks. NumPy arrays are highly optimized for mathematical operations on large datasets and are the de facto standard for numerical work in Python.

**Example of `array.array`:**

```python
import array

# Create an array of integers ('i' type code for signed int)
my_array = array.array('i', [1, 2, 3, 4, 5])
print(f"Array: {my_array}")
print(f"Type code: {my_array.typecode}")

# Arrays are mutable
my_array[0] = 10
print(f"Modified Array: {my_array}")

# Trying to add a different type will raise a TypeError
try:
    my_array.append(3.14)
except TypeError as e:
    print(f"Error appending float to int array: {e}")

# Example of a list with mixed types
my_list = [1, 'hello', 3.14]
print(f"List with mixed types: {my_list}")
```

**Output:**
```
Array: array('i', [1, 2, 3, 4, 5])
Type code: i
Modified Array: array('i', [10, 2, 3, 4, 5])
Error appending float to int array: an integer is required (got type float)
List with mixed types: [1, 'hello', 3.14]
```

## NumPy Arrays

NumPy (Numerical Python) is a fundamental library for scientific computing in Python. Its main object is the powerful N-dimensional array (`ndarray`), which is a grid of values of the same type.

**Installation:**
To use NumPy, you first need to install it:
```bash
pip install numpy
```

**Creating NumPy Arrays:**
You can create NumPy arrays from Python lists or by using built-in NumPy functions.

```python
import numpy as np

# From a Python list
my_list = [1, 2, 3, 4, 5]
numpy_array = np.array(my_list)
print(f"NumPy array from list: {numpy_array}")

# Using built-in functions
zeros_array = np.zeros(5) # Creates an array of five zeros
print(f"Array of zeros: {zeros_array}")

ones_array = np.ones(5) # Creates an array of five ones
print(f"Array of ones: {ones_array}")

range_array = np.arange(0, 10, 2) # Like Python's range(), but returns an array
print(f"Array from arange: {range_array}")
```

**Key Characteristics:**
- **Homogeneous:** All elements must be of the same data type.
- **Fixed Size:** The size of a NumPy array is fixed at creation. You cannot change it dynamically like a Python list.
- **Performance:** NumPy arrays are stored in a contiguous block of memory, which makes them very fast for mathematical operations.

**Common Attributes:**
- **`ndim`**: The number of dimensions (or axes) of the array.
- **`shape`**: A tuple of integers indicating the size of the array in each dimension.
- **`size`**: The total number of elements in the array.
- **`dtype`**: An object describing the data type of the array's elements.

```python
import numpy as np

# A 2D array (matrix)
matrix = np.array([[1, 2, 3], [4, 5, 6]])

print(f"Matrix:\n{matrix}")
print(f"Number of dimensions: {matrix.ndim}")
print(f"Shape of the matrix: {matrix.shape}")
print(f"Total number of elements: {matrix.size}")
print(f"Data type of elements: {matrix.dtype}")
```

**Basic Operations:**
NumPy arrays support element-wise operations, which are much faster than iterating over a Python list.

```python
import numpy as np

a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

# Element-wise addition
c = a + b
print(f"Element-wise sum: {c}")

# Element-wise multiplication
d = a * 2
print(f"Element-wise multiplication: {d}")
```

**Indexing and Slicing:**
Indexing and slicing work similarly to Python lists, but you can also use them for multi-dimensional arrays.

```python
import numpy as np

# 1D array
arr1d = np.array([10, 20, 30, 40, 50])
print(f"Element at index 2: {arr1d[2]}")
print(f"Slice from index 1 to 3: {arr1d[1:4]}")

# 2D array
arr2d = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
print(f"Element at row 1, column 2: {arr2d[1, 2]}") # Accessing a single element
print(f"First two rows:\n{arr2d[:2]}")
print(f"Second column:\n{arr2d[:, 1]}")
```

### Slicing and Indexing

Python lists support both positive and negative indexing, and powerful slicing capabilities to access elements or sub-sequences.

**1. Indexing (Accessing Single Elements):**
- **Positive Indexing:** Starts from `0` for the first element, `1` for the second, and so on.
- **Negative Indexing:** Starts from `-1` for the last element, `-2` for the second to last, and so on.

```python
my_list = ['a', 'b', 'c', 'd', 'e']

# Positive indexing
print(f"First element: {my_list[0]}")     # Output: a
print(f"Third element: {my_list[2]}")     # Output: c

# Negative indexing
print(f"Last element: {my_list[-1]}")      # Output: e
print(f"Second to last: {my_list[-2]}")  # Output: d
```

**2. Slicing (Accessing Sub-sequences):**
Slicing allows you to get a portion of a list. The syntax is `list[start:stop:step]`.

- `start`: The index where the slice begins (inclusive). If omitted, defaults to `0`.
- `stop`: The index where the slice ends (exclusive). If omitted, defaults to the end of the list.
- `step`: The increment between elements (optional). If omitted, defaults to `1`.

```python
my_list = [10, 20, 30, 40, 50, 60, 70, 80, 90]

# Basic slicing
print(f"Elements from index 2 to 5 (exclusive): {my_list[2:5]}")   # Output: [30, 40, 50]
print(f"Elements from beginning to index 4 (exclusive): {my_list[:4]}") # Output: [10, 20, 30, 40]
print(f"Elements from index 3 to end: {my_list[3:]}")           # Output: [40, 50, 60, 70, 80, 90]
print(f"All elements (a copy): {my_list[:]}")                   # Output: [10, 20, 30, 40, 50, 60, 70, 80, 90]

# Slicing with a step
print(f"Every other element from beginning: {my_list[::2]}")  # Output: [10, 30, 50, 70, 90]
print(f"Elements from index 1 to 7, with step 2: {my_list[1:8:2]}") # Output: [20, 40, 60, 80]

# Negative slicing
print(f"Last three elements: {my_list[-3:]}")              # Output: [70, 80, 90]
print(f"All elements in reverse order: {my_list[::-1]}") # Output: [90, 80, 70, 60, 50, 40, 30, 20, 10]
print(f"Elements from second to last, backwards: {my_list[-2::-1]}") # Output: [80, 70, 60, 50, 40, 30, 20, 10]
```

**Modifying Lists Using Indexing and Slicing:**

```python
my_list = [1, 2, 3, 4, 5]

# Modify a single element
my_list[0] = 100
print(f"List after modifying element: {my_list}") # Output: [100, 2, 3, 4, 5]

# Modify a slice (replacement can be of different length)
my_list[1:3] = ['a', 'b', 'c']
print(f"List after modifying slice: {my_list}") # Output: [100, 'a', 'b', 'c', 4, 5]

# Remove elements using slicing
my_list[2:4] = []
print(f"List after removing elements with slice: {my_list}") # Output: [100, 'a', 4, 5]
```

## List Comprehension

List comprehension offers a concise way to create lists. It is often more readable and performant than using a standard `for` loop.

**Basic Syntax:**
The simplest form of list comprehension is:
`[expression for item in iterable]`

**Example: Squaring numbers**

```python
# Using a for loop
squares = []
for x in range(10):
    squares.append(x**2)
print(f"Squares (with for loop): {squares}")

# Using list comprehension
squares_comp = [x**2 for x in range(10)]
print(f"Squares (with comprehension): {squares_comp}")
```
**Output:**
```
Squares (with for loop): [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
Squares (with comprehension): [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

**Syntax with a Condition:**
You can add a condition to filter the items from the iterable:
`[expression for item in iterable if condition]`

**Example: Filtering even numbers**
```python
# Using a for loop
evens = []
for x in range(10):
    if x % 2 == 0:
        evens.append(x)
print(f"Evens (with for loop): {evens}")

# Using list comprehension
evens_comp = [x for x in range(10) if x % 2 == 0]
print(f"Evens (with comprehension): {evens_comp}")
```
**Output:**
```
Evens (with for loop): [0, 2, 4, 6, 8]
Evens (with comprehension): [0, 2, 4, 6, 8]
```

**Conditional Expression (if/else):**
You can also use a conditional expression for the output expression itself.
`[expression_if_true if condition else expression_if_false for item in iterable]`

**Example: Categorizing numbers**
```python
# Using a for loop
num_types = []
for x in range(10):
    if x % 2 == 0:
        num_types.append("Even")
    else:
        num_types.append("Odd")
print(f"Number types (with for loop): {num_types}")

# Using list comprehension
num_types_comp = ["Even" if x % 2 == 0 else "Odd" for x in range(10)]
print(f"Number types (with comprehension): {num_types_comp}")
```
**Output:**
```
Number types (with for loop): ['Even', 'Odd', 'Even', 'Odd', 'Even', 'Odd', 'Even', 'Odd', 'Even', 'Odd']
Number types (with comprehension): ['Even', 'Odd', 'Even', 'Odd', 'Even', 'Odd', 'Even', 'Odd', 'Even', 'Odd']
```

**Nested List Comprehension:**
You can nest list comprehensions to work with nested lists, like a matrix. The order of the `for` clauses is the same as the order you would use in a standard nested `for` loop.

**Example: Flattening a matrix**
```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# Using a for loop
flattened = []
for row in matrix:
    for item in row:
        flattened.append(item)
print(f"Flattened (with for loop): {flattened}")

# Using nested list comprehension
flattened_comp = [item for row in matrix for item in row]
print(f"Flattened (with comprehension): {flattened_comp}")
```
**Output:**
```
Flattened (with for loop): [1, 2, 3, 4, 5, 6, 7, 8, 9]
Flattened (with comprehension): [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## Python Tuples

Tuples are ordered, immutable (unchangeable) sequences of items. They are similar to lists, but their contents cannot be modified after creation, which makes them faster and more memory-efficient.

**Characteristics:**
- **Ordered**: Items have a defined order, and that order will not change.
- **Unchangeable (Immutable)**: You cannot change, add, or remove items after the tuple has been created.
- **Allows Duplicates**: Tuples can have items with the same value.

**Creating a Tuple:**
```python
# Using parentheses
my_tuple = (1, 2, 3, "apple", "banana")

# Using the tuple() constructor
another_tuple = tuple(("cherry", "date", 5))

# Creating a tuple with one item (note the trailing comma)
single_item_tuple = ("apple",)
not_a_tuple = ("apple") # This is just a string
```

### Tuple Packing and Unpacking

**Tuple Packing:**
This is the process of "packing" a sequence of values into a tuple without needing to use parentheses. It's a common and idiomatic way to create tuples.

```python
# Packing multiple items
packed_tuple = 1, "hello", True 
print(packed_tuple)  # Output: (1, 'hello', True)

# Packing a single item (trailing comma is required)
single_packed = "world",
print(single_packed) # Output: ('world',)
```

**Tuple Unpacking:**
This is the reverse process, where you assign the elements of a tuple to a sequence of variables.

```python
my_tuple = ("apple", "banana", "cherry")

# Unpack the tuple into variables
(fruit1, fruit2, fruit3) = my_tuple
print(fruit1) # Output: apple
print(fruit2) # Output: banana

# Using an asterisk (*) to capture multiple items
numbers = (1, 2, 3, 4, 5, 6)
(first, *middle, last) = numbers
print(first)  # Output: 1
print(middle) # Output: [2, 3, 4, 5] (as a list)
print(last)   # Output: 6
```

### Common Tuple Methods

Because tuples are immutable, they have very few methods. The main ones are:

- **`count(item)`**: Returns the number of times a specified item appears in the tuple.
  ```python
  my_tuple = (1, 2, 2, 3, 2, 'a')
  count_of_2 = my_tuple.count(2) # Returns 3
  ```

- **`index(item)`**: Returns the index of the first occurrence of a specified item. Raises a `ValueError` if the item is not found.
  ```python
  my_tuple = ('a', 'b', 'c', 'd', 'e')
  index_of_c = my_tuple.index('c') # Returns 2
  ```

**Accessing Tuple Items:**
You can access tuple items by referring to the index number, inside square brackets, just like with lists.
```python
my_tuple = ("apple", "banana", "cherry")
print(my_tuple[1]) # Output: banana
```

## Python Sets

Sets are unordered, mutable collections of unique items. They are useful when you need to store a collection of elements where duplicates are not allowed and the order does not matter.

**Characteristics:**
- **Unordered**: Items in a set do not have a defined order. You cannot refer to items by index.
- **Mutable**: Sets are changeable; you can add or remove items from them.
- **No Duplicates**: A set cannot have two items with the same value.

**Creating a Set:**
```python
# Using curly braces
my_set = {1, 2, 3, "apple", "banana"}

# Using the set() constructor
another_set = set(("cherry", "date", 5))

# Creating an empty set (must use set(), not {})
empty_set = set()
empty_dict = {} # This creates an empty dictionary

# Important: When set() is called with a string, it creates a set of individual characters
char_set = set("hello")
print(f"Set from string 'hello': {char_set}") # Output: {'o', 'e', 'l', 'h'} (order may vary)
```

### Common Set Methods

- **`add(item)`**: Adds a single item to the set. If the item is already present, the set remains unchanged.
  ```python
  my_set = {"apple", "banana"}
  my_set.add("cherry") # my_set becomes {"apple", "banana", "cherry"}
  my_set.add("apple")  # my_set remains {"apple", "banana", "cherry"}
  ```

- **`update(iterable)`**: Adds all the items from an iterable (like a list, tuple, or another set) to the set.
  ```python
  my_set = {"apple", "banana"}
  my_list = ["cherry", "date"]
  my_set.update(my_list) # my_set becomes {"apple", "banana", "cherry", "date"}
  ```

- **`remove(item)`**: Removes a specified item. Raises a `KeyError` if the item is not found.
  ```python
  my_set = {"apple", "banana", "cherry"}
  my_set.remove("banana")
  ```

- **`discard(item)`**: Removes a specified item. If the item is not found, it does nothing.
  ```python
  my_set = {"apple", "banana", "cherry"}
  my_set.discard("date") # No error is raised
  ```

- **`pop()`**: Removes and returns an arbitrary item from the set. Raises a `KeyError` if the set is empty.
  ```python
  my_set = {"apple", "banana", "cherry"}
  popped_item = my_set.pop()
  ```

- **`clear()`**: Removes all items from the set.
  ```python
  my_set.clear() # my_set becomes set()
  ```

### Set Operations

Sets are powerful for performing mathematical set operations.

- **`union(other_set)`** or `|`: Returns a new set containing all items from both sets.
  ```python
  set1 = {1, 2, 3}
  set2 = {3, 4, 5}
  union_set = set1.union(set2) # or set1 | set2
  # union_set is {1, 2, 3, 4, 5}
  ```

- **`intersection(other_set)`** or `&`: Returns a new set containing only the items present in both sets.
  ```python
  set1 = {1, 2, 3}
  set2 = {3, 4, 5}
  intersection_set = set1.intersection(set2) # or set1 & set2
  # intersection_set is {3}
  ```

- **`difference(other_set)`** or `-`: Returns a new set containing items that are in the first set but not in the second set.
  ```python
  set1 = {1, 2, 3}
  set2 = {3, 4, 5}
  difference_set = set1.difference(set2) # or set1 - set2
  # difference_set is {1, 2}
  ```

- **`symmetric_difference(other_set)`** or `^`: Returns a new set with items that are in exactly one of the sets.
  ```python
  set1 = {1, 2, 3}
  set2 = {3, 4, 5}
  sym_diff_set = set1.symmetric_difference(set2) # or set1 ^ set2
  # sym_diff_set is {1, 2, 4, 5}
  ```

## Python Dictionaries

Dictionaries are unordered, mutable collections of key-value pairs. Each key must be unique and immutable (e.g., strings, numbers, tuples), while values can be of any data type and can be duplicated.

**Characteristics:**
- **Unordered** (in Python versions before 3.7, ordered in 3.7+): Items do not have a defined order.
- **Mutable**: Dictionaries are changeable; you can add, remove, and modify key-value pairs.
- **Keys are Unique**: Each key must be distinct. If you assign a value to an existing key, the old value is overwritten.
- **Keys are Immutable**: Keys must be of an immutable type (strings, numbers, tuples). Values can be mutable or immutable.

**Creating a Dictionary:**
```python
# Using curly braces
my_dict = {"name": "Alice", "age": 30, "city": "New York"}

# Using the dict() constructor
another_dict = dict(brand="Ford", model="Mustang", year=1964)

# Creating an empty dictionary
empty_dict = {}
```

### Accessing Dictionary Items

You can access dictionary values by referring to their key name inside square brackets or by using the `get()` method.

```python
my_dict = {"name": "Alice", "age": 30, "city": "New York"}

# Accessing using square brackets
print(f"Name: {my_dict['name']}") # Output: Alice

# Accessing using get() method
print(f"Age: {my_dict.get('age')}") # Output: 30

# Using get() with a default value if key is not found
print(f"Country: {my_dict.get('country', 'USA')}") # Output: USA
print(f"City: {my_dict.get('city', 'London')}")   # Output: New York
```

### Changing and Adding Items

```python
my_dict = {"name": "Alice", "age": 30, "city": "New York"}

# Changing a value
my_dict["age"] = 31
print(f"Modified age: {my_dict}") # Output: {'name': 'Alice', 'age': 31, 'city': 'New York'}

# Adding a new item
my_dict["email"] = "alice@example.com"
print(f"Added email: {my_dict}") # Output: {'name': 'Alice', 'age': 31, 'city': 'New York', 'email': 'alice@example.com'}
```

### Common Dictionary Methods

- **`keys()`**: Returns a view object that displays a list of all the keys in the dictionary.
  ```python
  my_dict = {"name": "Alice", "age": 30}
  print(f"Keys: {my_dict.keys()}") # Output: dict_keys(['name', 'age'])
  ```

- **`values()`**: Returns a view object that displays a list of all the values in the dictionary.
  ```python
  my_dict = {"name": "Alice", "age": 30}
  print(f"Values: {my_dict.values()}") # Output: dict_values(['Alice', 30])
  ```

- **`items()`**: Returns a view object that displays a list of a dictionary's key-value tuple pairs.
  ```python
  my_dict = {"name": "Alice", "age": 30}
  print(f"Items: {my_dict.items()}") # Output: dict_items([('name', 'Alice'), ('age', 30)])
  ```

- **`update(iterable)`**: Inserts the specified items to the dictionary. If the key already exists, the value gets updated.
  ```python
  my_dict = {"brand": "Ford", "model": "Mustang"}
  my_dict.update({"year": 1964, "color": "red"})
  print(f"Updated dictionary: {my_dict}") # Output: {'brand': 'Ford', 'model': 'Mustang', 'year': 1964, 'color': 'red'}
  ```

- **`pop(key, default)`**: Removes the item with the specified key and returns its value. If the key is not found, it returns `default` if provided, otherwise raises a `KeyError`.
  ```python
  my_dict = {"name": "Alice", "age": 30}
  age = my_dict.pop("age")
  print(f"Popped age: {age}") # Output: 30
  print(f"Dictionary after pop: {my_dict}") # Output: {'name': 'Alice'}

  city = my_dict.pop("city", "Unknown")
  print(f"Popped city (with default): {city}") # Output: Unknown
  ```

- **`popitem()`**: Removes and returns the last inserted key-value pair as a tuple. (In Python versions before 3.7, it removes and returns an arbitrary item).
  ```python
  my_dict = {"name": "Alice", "age": 30}
  last_item = my_dict.popitem()
  print(f"Last item: {last_item}") # Output: ('age', 30) (or similar)
  print(f"Dictionary after popitem: {my_dict}") # Output: {'name': 'Alice'}
  ```

- **`clear()`**: Removes all items from the dictionary.
  ```python
  my_dict = {"name": "Alice", "age": 30}
  my_dict.clear()
  print(f"Cleared dictionary: {my_dict}") # Output: {}
  ```

- **`setdefault(key, default)`**: Returns the value of the specified key. If the key does not exist, it inserts the key with the specified default value and returns the default value.
  ```python
  my_dict = {"name": "Alice", "age": 30}
  
  # Key exists, returns the value
  age = my_dict.setdefault("age", 31)
  print(f"Age: {age}") # Output: 30
  print(f"Dictionary: {my_dict}") # Output: {'name': 'Alice', 'age': 30}

  # Key does not exist, inserts the key with the default value
  city = my_dict.setdefault("city", "New York")
  print(f"City: {city}") # Output: New York
  print(f"Dictionary: {my_dict}") # Output: {'name': 'Alice', 'age': 30, 'city': 'New York'}
  ```

### Looping Through Dictionaries

You can loop through a dictionary in several ways.

**Looping through keys:**
```python
my_dict = {"name": "Alice", "age": 30}
for key in my_dict.keys():
    print(key)
# Output:
# name
# age
```

**Looping through values:**
```python
my_dict = {"name": "Alice", "age": 30}
for value in my_dict.values():
    print(value)
# Output:
# Alice
# 30
```

**Looping through key-value pairs:**
```python
my_dict = {"name": "Alice", "age": 30}
for key, value in my_dict.items():
    print(f"{key}: {value}")
# Output:
# name: Alice
# age: 30
```

### Nested Dictionaries

A dictionary can contain other dictionaries. This is a common way to represent complex data structures.

```python
users = {
    "user1": {
        "name": "Alice",
        "email": "alice@example.com"
    },
    "user2": {
        "name": "Bob",
        "email": "bob@example.com"
    }
}

# Accessing nested dictionary items
print(f"User1 name: {users['user1']['name']}") # Output: User1 name: Alice

# Looping through nested dictionaries
for user_id, user_info in users.items():
    print(f"\nUser ID: {user_id}")
    for key, value in user_info.items():
        print(f"  {key}: {value}")
```

### Dictionary Comprehension

Similar to list comprehension, dictionary comprehension provides a concise way to create dictionaries.

**Basic Syntax:**
`{key_expression: value_expression for item in iterable}`

**Example: Creating a dictionary of squares**
```python
squares_dict = {x: x**2 for x in range(5)}
print(f"Squares dictionary: {squares_dict}") # Output: {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

**Syntax with a Condition:**
`{key_expression: value_expression for item in iterable if condition}`

**Example: Filtering even numbers and their squares**
```python
even_squares = {x: x**2 for x in range(10) if x % 2 == 0}
print(f"Even squares dictionary: {even_squares}") # Output: {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}
```

**Conditional Expression (if/else):**
`{key_expression: value_expression_if_true if condition else value_expression_if_false for item in iterable}`

**Example: Categorizing numbers as even/odd**
```python
num_category = {x: "Even" if x % 2 == 0 else "Odd" for x in range(5)}
print(f"Number category dictionary: {num_category}") # Output: {0: 'Even', 1: 'Odd', 2: 'Even', 3: 'Odd', 4: 'Even'}
```

### Sorting Dictionaries

While dictionaries in Python 3.7+ maintain insertion order, you often need to sort them based on their keys or values. Sorting a dictionary doesn't change the original dictionary but instead provides a sorted representation, typically as a list of tuples.

**1. Sorting by Keys**

You can sort a dictionary by its keys by iterating over the sorted keys.

```python
my_dict = {'c': 3, 'a': 1, 'd': 4, 'b': 2}

# Sort keys and create a new dictionary (if you need a sorted dictionary)
sorted_by_key = {k: my_dict[k] for k in sorted(my_dict.keys())}
print(f"Sorted by key (new dict): {sorted_by_key}")

# Or loop through sorted keys to access values in order
print("Looping through sorted keys:")
for key in sorted(my_dict):
    print(f"  {key}: {my_dict[key]}")
```

**Output:**
```
Sorted by key (new dict): {'a': 1, 'b': 2, 'c': 3, 'd': 4}
Looping through sorted keys:
  a: 1
  b: 2
  c: 3
  d: 4
```

**2. Sorting by Values**

To sort by values, you need to use the `sorted()` function on the dictionary's `items()` and provide a `lambda` function to the `key` argument to specify that the sorting should be based on the value (the second element of the item tuple).

```python
my_dict = {'c': 3, 'a': 1, 'd': 4, 'b': 2}

# Sort items by value (the second element of the tuple, index 1)
sorted_items = sorted(my_dict.items(), key=lambda item: item[1])
print(f"Sorted by value (list of tuples): {sorted_items}")

# To get a new dictionary sorted by value
sorted_by_value_dict = {k: v for k, v in sorted_items}
print(f"Sorted by value (new dict): {sorted_by_value_dict}")

# For descending order
sorted_items_desc = sorted(my_dict.items(), key=lambda item: item[1], reverse=True)
print(f"Sorted by value descending: {sorted_items_desc}")
```

**Output:**
```
Sorted by value (list of tuples): [('a', 1), ('b', 2), ('c', 3), ('d', 4)]
Sorted by value (new dict): {'a': 1, 'b': 2, 'c': 3, 'd': 4}
Sorted by value descending: [('d', 4), ('c', 3), ('b', 2), ('a', 1)]
```

## Python Strings

Strings are immutable sequences of characters. They are one of the most commonly used data types in Python.

**Characteristics:**
- **Immutable**: Once a string is created, it cannot be changed.
- **Ordered**: Characters in a string have a defined order.

**Creating a String:**
```python
# Using single quotes
my_string = 'Hello, World!'

# Using double quotes
another_string = "Python is fun."

# Multiline strings
multiline_string = """This is a
multiline
string."""
```

### Accessing Characters and Slicing

You can access individual characters using indexing and a range of characters using slicing.

```python
my_string = "Hello, World!"

# Accessing a single character
print(f"First character: {my_string[0]}") # Output: H

# Slicing
print(f"Slice from index 7 to 12: {my_string[7:12]}") # Output: World
```

### Common String Methods

- **`upper()`**: Returns a new string with all characters in uppercase.
  ```python
  my_string = "Hello, World!"
  print(f"Uppercase: {my_string.upper()}") # Output: HELLO, WORLD!
  ```

- **`lower()`**: Returns a new string with all characters in lowercase.
  ```python
  my_string = "Hello, World!"
  print(f"Lowercase: {my_string.lower()}") # Output: hello, world!
  ```

- **`strip()`**: Returns a new string with leading and trailing whitespace removed.
  ```python
  my_string = "  Hello, World!  "
  print(f"Stripped: '{my_string.strip()}'") # Output: 'Hello, World!'
  ```

- **`replace(old, new)`**: Returns a new string where all occurrences of `old` are replaced with `new`.
  ```python
  my_string = "Hello, World!"
  print(f"Replaced: {my_string.replace('World', 'Python')}") # Output: Hello, Python!
  ```

- **`split(separator)`**: Returns a list of substrings separated by the `separator`. If no separator is provided, it splits by whitespace.
  ```python
  my_string = "apple,banana,cherry"
  print(f"Split: {my_string.split(',')}") # Output: ['apple', 'banana', 'cherry']
  ```

- **`join(iterable)`**: Joins the elements of an iterable into a single string, with the string as the separator.
  ```python
  my_list = ['apple', 'banana', 'cherry']
  print(f"Joined: {','.join(my_list)}") # Output: apple,banana,cherry
  ```

- **`startswith(prefix)`**: Returns `True` if the string starts with the specified prefix, otherwise `False`.
  ```python
  my_string = "Hello, World!"
  print(f"Starts with 'Hello': {my_string.startswith('Hello')}") # Output: True
  ```

- **`endswith(suffix)`**: Returns `True` if the string ends with the specified suffix, otherwise `False`.
  ```python
  my_string = "Hello, World!"
  print(f"Ends with 'World!': {my_string.endswith('World!')}") # Output: True
  ```

- **`find(substring)`**: Returns the lowest index of the substring if it is found in the string. If it is not found, it returns -1.
  ```python
  my_string = "Hello, World!"
  print(f"Find 'World': {my_string.find('World')}") # Output: 7
  ```

- **`count(substring)`**: Returns the number of non-overlapping occurrences of a substring in the string.
  ```python
  my_string = "hello, hello, hello"
  print(f"Count 'hello': {my_string.count('hello')}") # Output: 3
  ```



### String Formatting

There are several ways to format strings in Python.

**1. f-Strings (Formatted String Literals)**
Introduced in Python 3.6, f-strings are the most modern and preferred way to format strings. They are concise and readable.

```python
name = "Alice"
age = 30
print(f"My name is {name} and I am {age} years old.")
# Output: My name is Alice and I am 30 years old.

# Formatting floating-point numbers
pi = 3.1415926535
print(f"Pi to 2 decimal places: {pi:.2f}") # Output: Pi to 2 decimal places: 3.14
print(f"Pi to 5 decimal places: {pi:.5f}") # Output: Pi to 5 decimal places: 3.14159
```

**2. `str.format()` Method**
This method is more versatile than the old `%` formatting and was the standard before f-strings.

```python
name = "Bob"
age = 25

# Using positional arguments
print("My name is {} and I am {} years old.".format(name, age))

# Using keyword arguments
print("My name is {name} and I am {age} years old.".format(name="Charlie", age=35))

# Formatting floating-point numbers
pi = 3.1415926535
print("Pi to 2 decimal places: {:.2f}".format(pi)) # Output: Pi to 2 decimal places: 3.14
print("Pi to 5 decimal places: {:.5f}".format(pi)) # Output: Pi to 5 decimal places: 3.14159
```

**3. `%` Operator (Old Style)**
This is the original way of formatting strings in Python, similar to `printf` in C. It is less flexible and can be error-prone, so it is generally not recommended for new code.

```python
name = "David"
age = 40
print("My name is %s and I am %d years old." % (name, age))

# Formatting floating-point numbers
pi = 3.1415926535
print("Pi to 2 decimal places: %.2f" % pi) # Output: Pi to 2 decimal places: 3.14
print("Pi to 5 decimal places: %.5f" % pi) # Output: Pi to 5 decimal places: 3.14159
```



### String Concatenation and Repetition

You can combine strings using the `+` operator and repeat them using the `*` operator.

```python
# Concatenation
str1 = "Hello"
str2 = "World"
result = str1 + ", " + str2 + "!"
print(result) # Output: Hello, World!

# Repetition
str1 = "abc"
result = str1 * 3
print(result) # Output: abcabcabc
```



### More String Methods

Here are a few more useful string methods for checking the content of a string.

- **`isalnum()`**: Returns `True` if all characters in the string are alphanumeric (letters or numbers).
  ```python
  print("abc123".isalnum()) # Output: True
  print("abc 123".isalnum()) # Output: False
  ```

- **`isalpha()`**: Returns `True` if all characters in the string are alphabetic.
  ```python
  print("abc".isalpha()) # Output: True
  print("abc1".isalpha()) # Output: False
  ```

- **`isdigit()`**: Returns `True` if all characters in the string are digits.
  ```python
  print("123".isdigit()) # Output: True
  print("123a".isdigit()) # Output: False
  ```

- **`islower()`**: Returns `True` if all cased characters in the string are lowercase.
  ```python
  print("hello".islower()) # Output: True
  print("Hello".islower()) # Output: False
  ```

- **`isupper()`**: Returns `True` if all cased characters in the string are uppercase.
  ```python
  print("HELLO".isupper()) # Output: True
  print("Hello".isupper()) # Output: False
  ```

- **`isspace()`**: Returns `True` if all characters in the string are whitespace characters.
  ```python
  print("   ".isspace()) # Output: True
  print(" a ".isspace()) # Output: False
  ```

- **`title()`**: Returns a titlecased version of the string, where words start with an uppercase character and the remaining characters are lowercase.
  ```python
  print("hello world".title()) # Output: Hello World
  ```


