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
Original matrix before deep copy modification: [[99, 2], [3, 4]]
Deep copied matrix before modification: [[99, 2], [3, 4]]
Original matrix after deep copy modification: [[99, 2], [3, 4]]
Deep copied matrix after modification: [[100, 2], [3, 4]]
```