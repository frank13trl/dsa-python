# Foundation

## Big O Notation

[NeetCode - Big-O Notation](https://www.youtube.com/watch?v=BgLTDT03QtU)

### What is Big O Notation?
Big O Notation is a mathematical notation that describes the limiting behavior of a function when the argument tends towards a particular value or infinity. In computer science, it's used to classify algorithms according to how their running time or space requirements grow as the input size grows. It's a way to talk about how quickly runtime or space requirements grow relative to the input size.

### Why is it important?
- **Performance Comparison**: It allows us to compare the efficiency of different algorithms without implementing them or running them on specific hardware.
- **Scalability**: It helps predict how an algorithm will behave as the input size increases, which is crucial for designing scalable systems.
- **Optimization**: Understanding Big O helps in identifying bottlenecks and optimizing code for better performance.

### Common Big O Complexities
Here are some of the most common Big O complexities, from most efficient to least efficient:

1.  **O(1) - Constant Time**: The execution time or space required does not change with the size of the input data. E.g., accessing an array element by index.
    ```python
    def get_first_element(arr):
        return arr[0]
    ```

2.  **O(log n) - Logarithmic Time**: The execution time or space required grows logarithmically with the input size. This often occurs in algorithms that divide the problem in half with each step. E.g., binary search.
    ```python
    def binary_search(arr, target):
        left, right = 0, len(arr) - 1
        while left <= right:
            mid = (left + right) // 2
            if arr[mid] == target:
                return mid
            elif arr[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
        return -1
    ```

3.  **O(sqrt(n)) - Square Root Time**: The execution time or space required grows proportionally to the square root of the input size. This is more efficient than linear time but less efficient than logarithmic time. E.g., checking for primality by iterating up to the square root of the number.
    ```python
    import math

    def is_prime_sqrt(n):
        if n < 2:
            return False
        for i in range(2, int(math.sqrt(n)) + 1):
            if n % i == 0:
                return False
        return True
    ```

4.  **O(n) - Linear Time**: The execution time or space required grows linearly with the input size. E.g., iterating through a list.
    ```python
    def sum_array(arr):
        total = 0
        for x in arr:
            total += x
        return total
    ```

4.  **O(n log n) - Linearithmic Time**: The execution time or space required grows proportionally to n log n. This is common in efficient sorting algorithms. E.g., merge sort, quick sort.
    ```python
    # Conceptual example for merge sort
    def merge_sort(arr):
        if len(arr) <= 1:
            return arr
        mid = len(arr) // 2
        left_half = arr[:mid]
        right_half = arr[mid:]

        left_half = merge_sort(left_half)
        right_half = merge_sort(right_half)

        return merge(left_half, right_half)

    def merge(left, right):
        # Merging logic here
        pass
    ```

5.  **O(n^2) - Quadratic Time**: The execution time or space required grows quadratically with the input size. Often seen in algorithms with nested loops. E.g., bubble sort, selection sort.
    ```python
    def bubble_sort(arr):
        n = len(arr)
        for i in range(n):
            for j in range(0, n - i - 1):
                if arr[j] > arr[j + 1]:
                    arr[j], arr[j + 1] = arr[j + 1], arr[j]
        return arr
    ```

6.  **O(2^n) - Exponential Time**: The execution time or space required doubles with each addition to the input data set. These algorithms are often characterized by exploring all possible subsets or combinations. E.g.,
    -   Recursive calculation of Fibonacci numbers without memoization.
    ```python
    def fibonacci_recursive(n):
        if n <= 1:
            return n
        return fibonacci_recursive(n - 1) + fibonacci_recursive(n - 2)
    ```
    -   **Generating all subsets (Power Set)**: For a set of `n` elements, there are `2^n` subsets.
    ```python
    def generate_subsets(nums):
        subsets = []
        n = len(nums)
        for i in range(1 << n): # 1 << n is equivalent to 2^n
            current_subset = []
            for j in range(n):
                if (i >> j) & 1: # Check if j-th bit is set in i
                    current_subset.append(nums[j])
            subsets.append(current_subset)
        return subsets
    ```
    -   **Brute-force solutions for NP-hard problems**: Many problems like the Traveling Salesperson Problem (TSP) or the Subset Sum Problem, when solved with naive recursive or exhaustive search approaches, exhibit O(2^n) complexity.

7.  **O(n!) - Factorial Time**: The execution time or space required grows factorially with the input size. This is extremely slow and usually indicates a very inefficient algorithm. E.g., solving the traveling salesman problem with a brute-force approach.

### How to Analyze Big O
When analyzing an algorithm's Big O complexity, consider these rules:

-   **Drop Constants**: O(2n) becomes O(n), O(n/2) becomes O(n).
-   **Drop Non-Dominant Terms**: O(n^2 + n) becomes O(n^2). The term that grows fastest dominates the complexity.
-   **Different Inputs, Different Variables**: If an algorithm takes two different inputs, say `a` and `b`, and their sizes affect the runtime independently, the complexity might be O(a + b) or O(a * b).
-   **Worst Case**: Big O typically describes the worst-case scenario, as this provides an upper bound on the algorithm's performance.

Understanding Big O Notation is fundamental to becoming a proficient software engineer, as it guides you in writing efficient and scalable code.

### Example: Analyzing Complexity

Let's analyze the Big O complexity of a function that checks if a given list contains duplicate elements.

```python
def contains_duplicates(arr):
    n = len(arr)
    for i in range(n):
        for j in range(i + 1, n):
            if arr[i] == arr[j]:
                return True
    return False
```

**Analysis:**

1.  **Outer Loop**: The first `for` loop iterates `n` times (from `i = 0` to `n-1`).
2.  **Inner Loop**: The second `for` loop iterates `n - 1 - i` times.
    *   When `i = 0`, it runs `n - 1` times.
    *   When `i = 1`, it runs `n - 2` times.
    *   ...
    *   When `i = n - 2`, it runs `1` time.
3.  **Total Operations**: The total number of comparisons is approximately `(n-1) + (n-2) + ... + 1`, which is the sum of an arithmetic series. This sum is `n * (n - 1) / 2`.
4.  **Simplification**: `n * (n - 1) / 2 = (n^2 - n) / 2 = 0.5n^2 - 0.5n`.
5.  **Drop Constants and Non-Dominant Terms**: Following the rules of Big O, we drop the constant `0.5` and the non-dominant term `0.5n`.

Therefore, the time complexity of the `contains_duplicates` function is **O(n^2)**.

### Other Asymptotic Notations
While Big O Notation describes the **upper bound** (worst-case scenario) of an algorithm's performance, there are two other important notations:

-   **Big Omega (Ω) Notation**: Describes the **lower bound** (best-case scenario) of an algorithm's running time. If an algorithm is Ω(f(n)), it means its running time will be at least proportional to f(n) for large enough n.

-   **Big Theta (Θ) Notation**: Describes the **tight bound** (average-case scenario) of an algorithm's running time. If an algorithm is Θ(f(n)), it means its running time is bounded both above and below by f(n) for large enough n. This implies that the best-case and worst-case complexities are the same, or at least of the same order.

## Special Cases: O(n) with Nested Loops (Amortized Analysis)



Sometimes, algorithms appear to have a higher time complexity due to nested loops, but upon closer inspection using **amortized analysis**, they reveal a more efficient O(n) complexity. This happens when operations that seem costly individually are infrequent enough that their average cost over a sequence of operations is low.

### Sliding Window Technique

The sliding window technique often involves a `for` loop (outer loop) and a `while` loop (inner loop), giving the impression of O(n^2) complexity. However, it's typically O(n).

**Why O(n)?**
-   A sliding window usually maintains two pointers, `start` and `end`, defining the current window.
-   The `end` pointer iterates through the array from left to right, visiting each element exactly once. This contributes O(n) to the complexity.
-   The `start` pointer also moves from left to right, but it never moves backward. In the worst case, it also visits each element at most once over the *entire* execution of the algorithm.
-   Since both pointers traverse the array at most once, the total number of operations is proportional to `n + n = 2n`, which simplifies to **O(n)**. Each element enters and leaves the window at most once.

**Example (Conceptual):**
```python
def sliding_window_example(arr, target_sum):
    start = 0
    current_sum = 0
    for end in range(len(arr)):  # Outer loop: 'end' pointer moves O(n) times
        current_sum += arr[end]
        while current_sum >= target_sum and start <= end: # Inner loop: 'start' pointer moves
            # Perform operations on the window
            current_sum -= arr[start]
            start += 1 # 'start' pointer only moves forward
    return # result
```

### Monotonic Stack

A monotonic stack (either strictly increasing or strictly decreasing) is another data structure that can achieve O(n) complexity even with nested loops.

**Why O(n)?**
-   The algorithm typically involves an outer `for` loop that iterates through each element of the input array once. This is O(n).
-   Inside this `for` loop, there's often a `while` loop that pops elements from the stack based on the monotonic condition.
-   The crucial observation is that each element is pushed onto the stack exactly once.
-   An element, once pushed, can be popped from the stack at most once.
-   Therefore, the total number of push and pop operations across the entire algorithm's execution is proportional to `n`.
-   The sum of operations (outer loop iterations + total stack operations) is `O(n) + O(n) = O(2n)`, which simplifies to **O(n)**.

**Example (Conceptual - Next Greater Element):**
```python
def monotonic_stack_example(arr):
    stack = [] # Monotonic decreasing stack
    result = [-1] * len(arr)
    for i in range(len(arr)): # Outer loop: O(n) iterations
        while stack and arr[i] > arr[stack[-1]]: # Inner loop: pops elements
            # An element is popped at most once
            popped_index = stack.pop()
            result[popped_index] = arr[i]
        stack.append(i) # Each element is pushed once
    return result
```

## Time Complexity Examples

[Abdul Bari - Time Comlexity 1](https://www.youtube.com/watch?v=9TlHvipP5yA)

[Abdul Bari - Time Comlexity 2](https://www.youtube.com/watch?v=9SgLBjXqwd4)

## Space Complexity

Space complexity is a measure of the amount of working storage an algorithm needs. This includes the space taken by the inputs, auxiliary space used by the algorithm during its execution, and the space for the output. When we talk about space complexity, we usually focus on the **auxiliary space**, which is the extra space or temporary space used by the algorithm during its execution, not including the space taken by the input.

### How to Analyze Space Complexity

Similar to time complexity, space complexity is expressed using Big O notation. Here are key considerations:

-   **Input Space**: The space required to store the input data. This is often considered separately or as part of the overall space if it grows with the input size.
-   **Auxiliary Space**: The temporary space used by the algorithm. This is what we typically analyze with Big O.
-   **Data Structures**: The space taken by data structures like arrays, lists, hash maps, stacks, queues, etc., that are created within the algorithm.
-   **Recursion Stack Space**: For recursive algorithms, the space taken by the call stack can contribute significantly to space complexity. Each recursive call adds a new frame to the stack.



### Common Space Complexities

1.  **O(1) - Constant Space**: The amount of memory used does not change with the input size. E.g., storing a few variables.
    ```python
    def multiply_by_two(n):
        result = n * 2  # Only a few variables are used, regardless of n
        return result
    ```

2.  **O(log n) - Logarithmic Space**: The space required grows logarithmically with the input size. This is rare for auxiliary space but can occur in some recursive algorithms or algorithms that reduce the problem size by a constant factor.

3.  **O(n) - Linear Space**: The space required grows linearly with the input size. E.g., creating a new array or list to store results that is proportional to the input size.
    ```python
    def copy_array(arr):
        new_arr = []
        for x in arr:
            new_arr.append(x)
        return new_arr # new_arr takes O(n) space
    ```

4.  **O(n^2) - Quadratic Space**: The space required grows quadratically with the input size. E.g., creating a 2D array (matrix) where dimensions are proportional to the input size.
    ```python
    def create_matrix(n):
        matrix = []
        for i in range(n):
            row = [0] * n # Each row takes O(n) space
            matrix.append(row)
        return matrix # The matrix takes O(n*n) = O(n^2) space
    ```

#### Space Complexity of Recursive Functions

For recursive functions, the space complexity is often determined by the maximum depth of the recursion, as each recursive call adds a new frame to the call stack. The space for each call frame includes parameters, local variables, and the return address.

**Example: Factorial Function**

Let's analyze the space complexity of a recursive factorial function:

```python
def factorial_recursive(n):
    if n <= 1:
        return 1
    return n * factorial_recursive(n - 1)
```

**Analysis:**

1.  **Base Case**: The recursion stops when `n <= 1`.
2.  **Recursive Step**: For `n > 1`, the function calls itself with `n - 1`.
3.  **Call Stack**: To calculate `factorial_recursive(n)`, the following calls are made and stored on the call stack:
    *   `factorial_recursive(n)`
    *   `factorial_recursive(n - 1)`
    *   `factorial_recursive(n - 2)`
    *   ...
    *   `factorial_recursive(1)`
4.  **Maximum Depth**: The maximum depth of the recursion is `n`. At its peak, the call stack will hold `n` frames.

Therefore, the space complexity of the `factorial_recursive` function is **O(n)**, as the space used by the call stack grows linearly with the input `n`.

**Example: Recursive Sum of an Array**

When an array is passed to a recursive function, the space complexity depends on how the array is passed. In Python, lists (arrays) are passed by reference, meaning that a reference to the original array is passed, not a copy.

Let's analyze the space complexity of a recursive function that calculates the sum of an array:

```python
def recursive_sum(arr, index):
    if index >= len(arr):
        return 0
    return arr[index] + recursive_sum(arr, index + 1)
```

**Analysis:**

1.  **Base Case**: The recursion stops when the `index` is out of bounds.
2.  **Recursive Step**: The function calls itself with the same array but an incremented `index`.
3.  **Call Stack**: To calculate the sum of an array of size `n`, the following calls are made:
    *   `recursive_sum(arr, 0)`
    *   `recursive_sum(arr, 1)`
    *   ...
    *   `recursive_sum(arr, n)`
4.  **Array Passing**: Since the array is passed by reference, no new copies of the array are made. The space for the array itself is O(n) but is part of the input space, not the auxiliary space.
5.  **Maximum Depth**: The maximum depth of the recursion is `n + 1`. At its peak, the call stack will hold `n + 1` frames. Each frame contains a reference to the array and the current index, which takes constant space.

Therefore, the auxiliary space complexity of the `recursive_sum` function is **O(n)**, as the space used by the call stack grows linearly with the size of the input array.