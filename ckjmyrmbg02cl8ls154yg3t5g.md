---
title: "Big O Notation - Quick recap"
datePublished: Tue Jul 30 2024 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: ckjmyrmbg02cl8ls154yg3t5g
slug: big-o-notation-quick-recap
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1610610168870/qB6TY-Dxn.png
tags: python, data-structures, learning, python3, time-complexity, big-o-notation

---

[&lt;- Go Back to Index](https://carboncoffee.hashnode.dev/datastructures)

# Algorithmic Complexity

Refers to the measure of the amount of resources an algorithm requires to run, particularly in terms of time (time complexity) and space (space complexity).

### Time

This measures the amount of time an algorithm takes to complete as a function of the input size. Here are some common techniques for measuring time complexity:

1. **Counting Basic Operations**: Analyse the algorithm to count the number of fundamental operations it performs. This count is then expressed as a function of the input size, `n`. The focus is usually on the dominant term, which grows the fastest as `n` increases.
    
    1. Pros
        
        1. **Simplicity**: Counting operations is straightforward and helps in understanding how an algorithm works.
            
        2. **Precision**: It helps in identifying which parts of the algorithm are most time-consuming.
            
        3. **Comparative Analysis**: Counting operations allows for a direct comparison between different algorithms on the same problem.
            
        4. **Insight into Optimisation**: By identifying the number of operations, you can pinpoint inefficiencies and areas where the algorithm can be optimised.
            
    2. Cons
        
        1. **Scalability Issues**: For large and complex algorithms, counting individual operations can become impractical.
            
        2. **Lack of Generalisation**: This method focuses on specific operations, which may not provide a complete picture of the algorithm's overall time complexity.
            
        3. **Hardware and Implementation Variability**: The actual time taken by an operation can vary depending on the hardware and programming language, so counting operations doesn't always translate directly to real-world performance.
            
        4. **Ignores Constant Factors**: While counting operations provides a precise count, it doesn't account for constant factors that might affect the actual runtime. For instance, an algorithm with fewer operations might still be slower due to more complex individual operations.
            
2. **Order of Growth:** Order of Growth describes how the time complexity of an algorithm scales with the size of the input. It focuses on the dominant term of the complexity function, which grows the fastest as the input size increases.
    
    1. **Big O Notation (O)**: Represents the upper bound of the runtime or the <mark>worst-case scenario.</mark> It describes the maximum amount of time an algorithm could take relative to the input size. For example, O(n^2) indicates that the algorithm's runtime increases quadratically as the input size grows.
        
    2. **Big Omega Notation (Ω)**: Represents the lower bound or the <mark> best-case scenario.</mark> It describes the minimum time required for the algorithm to complete, although this is less commonly used for general analysis.
        
    3. **Big Theta Notation (Θ)**: Describes a tight bound, meaning that the algorithm's runtime is sandwiched between upper and lower bounds. This notation is used when the worst-case and best-case times are of the same order of growth.
        

# **Understanding Big O Notation:**

### **Q. What are we looking for?**

**A.**

1. We want to evaluate our code's efficiency when the input size becomes very large, typically in the <mark>worst-case scenario.</mark> Our focus is on understanding how the time required to run an algorithm changes as the size of the input data increases.
    
2. We're interested in understanding how the <mark>time required to run an algorithm changes as the size of the input data increases</mark>. Essentially, we're plotting a graph where the x-axis represents the input size and the y-axis represents the time (or resources) required. This allows us to compare the performance of different algorithms under varying input sizes.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1722441381107/d82ab6b4-7b18-4fdd-91f8-1053c27acbe6.png align="center")

3. It's important to note that we don't need the exact function describing the time complexity. Instead, we're looking for the most significant or dominant factor that affects the algorithm's growth rate. This is why <mark>we focus on the part of the program that takes the longest time to run</mark>, as it typically dominates the overall performance as input size grows.
    

### How to calculate this now ?

**Big O Notation** is used to describe the upper bound of the running time or space requirements of an algorithm as the input size grows. It provides a way to express the worst-case scenario for an algorithm's performance. The notation is represented as **O()**, where the expression inside the parentheses describes how the running time or space grows relative to the input size.

For example, **O(n)** indicates that the running time or space requirement grows linearly with the input size **n**.

### Rules for deriving the Big O

Let's take an example using python -

```python
def find_factors(n):
    factors = []
    for i in range(1, n + 1):
        if n % i == 0:
            factors.append(i)
    return factors
```

In the above code, let's first count the number of operations happening.

1. **Initialization**: The operation `factors = []` assigns an empty list to the variable `factors`. This is a constant-time operation, **O(1)**.
    
2. **For Loop**: The `for` loop iterates from **1** to **n**. Since we are considering the worst-case scenario, this loop will run **n**times.
    
    Inside the loop:
    
    * **Modulus Operation**: The `if n % i == 0` check is a constant-time operation, **O(1)**.
        
    * **Append Operation**: The `factors.append(i)` operation is also **O(1)** in the average case, although appending to a list could involve resizing, which can make it amortized **O(1)**.
        
    
    In the worst case, all **n** values are factors and will be appended to the list, resulting in **n** append operations.
    
3. **Return**: The `return factors` statement is a constant-time operation, **O(1)**.
    

**Total Operations**:

* Initialization: **1** operation
    
* Loop (with operations inside): **n \* (constant time operations)** ≈ **n**
    
* Return: **1** operation
    

**Total Time Complexity**: When we combine these, the dominant term is **n**. Hence, the time complexity is **O(n)**.

Here's a table that shows common <mark>time complexities from best to worst in terms of their growth rates:</mark>

| **Time Complexity** | **Description** | **Growth Rate** | **Example Algorithm** |
| --- | --- | --- | --- |
| **O(1)** | Constant time | Constant | Accessing an array element |
| **O(log n)** | Logarithmic time | Logarithmic | Binary search |
| **O(n)** | Linear time | Linear | Iterating through a list |
| **O(n log n)** | Linearithmic time | Linearithmic | Merge sort |
| **O(n^2)** | Quadratic time | Quadratic | Bubble sort, Selection sort |
| **O(2^n)** | Exponential time | Exponential | Recursive Fibonacci |
| **O(n!)** | Factorial time | Factorial | Traveling Salesman Problem |

### Explanation:

* **O(1)**: Constant time complexity. The execution time or space does not change with the input size.
    
* **O(log n)**: Logarithmic time complexity. The execution time grows logarithmically with the input size.
    
* **O(n)**: Linear time complexity. The execution time grows linearly with the input size.
    
* **O(n log n)**: Linearithmic time complexity. The execution time grows in proportion to **n log n**. This is typical for efficient sorting algorithms.
    
* **O(n^2)**: Quadratic time complexity. The execution time grows quadratically with the input size. This is common in algorithms with nested loops.
    
* **O(2^n)**: Exponential time complexity. The execution time grows exponentially with the input size. This is common in algorithms with many recursive calls.
    
* **O(n!)**: Factorial time complexity. The execution time grows factorially with the input size. This is common in problems involving permutations.
    

# Let's see More Examples.

### 1\. **O(1)** - Constant Time Complexity

**Example Code:**

```python
def get_last_element(lst):
    return lst[-1]

# Example usage
my_list = [10, 20, 30, 40, 50]
print(get_last_element(my_list))
```

**Explanation:**

* **Operation**: The function accesses the last element of a list using the index `-1`.
    
* **Time Complexity**: Accessing an element by index in a list is a direct lookup operation, which is performed in constant time, **O(1)**. It does not matter how large the list is; this operation always takes the same amount of time.
    

### 2\. **O(log n)** - Logarithmic Time Complexity

**Example Code:**

```python
def binary_search(arr, target):
    low, high = 0, len(arr) - 1
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1

# Example usage
sorted_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print(binary_search(sorted_list, 7))
```

**Explanation:**

* **Operation**: The function performs a binary search on a sorted list to find the target value.
    
* **Steps**:
    
    * It calculates the middle index.
        
    * It compares the middle element with the target.
        
    * It discards half of the search space (either the left or right half) based on the comparison.
        
* **Time Complexity**: Each iteration reduces the search space by half. This halving process continues until the search space is reduced to one element. The number of iterations required to reduce the search space to 1 is proportional to the logarithm of the input size **n**. Thus, the time complexity is **O(log n)**.
    

### 3\. **O(n)** - Linear Time Complexity

**Example Code:**

```python
def print_all_elements(lst):
    for element in lst:
        print(element)

# Example usage
my_list = [1, 2, 3, 4, 5]
print_all_elements(my_list)
```

**Explanation:**

* **Operation**: The function iterates over each element in the list and prints it.
    
* **Steps**:
    
    * The `for` loop runs once for each element in the list.
        
    * If the list has **n** elements, the loop runs **n** times.
        
* **Time Complexity**: The number of operations is directly proportional to the size of the input list. Therefore, the time complexity is **O(n)**.
    

### 4\. **O(n log n)** - Linearithmic Time Complexity

**Example Code:**

```python
def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2
        L = arr[:mid]
        R = arr[mid:]
        
        merge_sort(L)
        merge_sort(R)
        
        i = j = k = 0
        
        while i < len(L) and j < len(R):
            if L[i] < R[j]:
                arr[k] = L[i]
                i += 1
            else:
                arr[k] = R[j]
                j += 1
            k += 1
        
        while i < len(L):
            arr[k] = L[i]
            i += 1
            k += 1
        
        while j < len(R):
            arr[k] = R[j]
            j += 1
            k += 1

# Example usage
my_list = [38, 27, 43, 3, 9, 82, 10]
merge_sort(my_list)
print(my_list)
```

**Explanation:**

* **Operation**: The function sorts a list using the merge sort algorithm.
    
* **Steps**:
    
    * The list is recursively divided into two halves until single-element lists are obtained.
        
    * These lists are then merged back together in sorted order.
        
* **Time Complexity**:
    
    * **Divide step**: Each division splits the list into two halves, leading to **log n** divisions.
        
    * **Merge step**: Each merge operation takes **O(n)** time, as it involves combining the two halves.
        
    * Since the merge step occurs **log n** times, the overall time complexity is **O(n log n)**.
        

### 5\. **O(n^2)** - Quadratic Time Complexity

**Example Code:**

```python
def print_all_pairs(lst):
    for i in range(len(lst)):
        for j in range(len(lst)):
            print(f"({lst[i]}, {lst[j]})")

# Example usage
my_list = [1, 2, 3]
print_all_pairs(my_list)
```

**Explanation:**

* **Operation**: The function prints all possible pairs of elements from the list.
    
* **Steps**:
    
    * The outer loop runs **n** times (once for each element).
        
    * The inner loop also runs **n** times for each iteration of the outer loop.
        
    * Therefore, there are **n \* n = n^2** total iterations.
        
* **Time Complexity**: The number of operations is proportional to the square of the input size, so the time complexity is **O(n^2)**.
    

### 6\. **O(2^n)** - Exponential Time Complexity

**Example Code:**

```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

# Example usage
print(fibonacci(5))
```

**Explanation:**

* **Operation**: The function computes the nth Fibonacci number using a naive recursive approach.
    
* **Steps**:
    
    * Each call to `fibonacci` results in two additional recursive calls, except for the base cases.
        
    * This branching leads to a binary tree of function calls with height **n**.
        
* **Time Complexity**: The total number of calls doubles with each increase in **n**, leading to **O(2^n)** time complexity.
    

### 7\. **O(n!)** - Factorial Time Complexity

**Example Code:**

```python
def permute(lst):
    if len(lst) == 0:
        return [[]]
    result = []
    for i in range(len(lst)):
        elem = lst[i]
        remaining = lst[:i] + lst[i+1:]
        for p in permute(remaining):
            result.append([elem] + p)
    return result

# Example usage
my_list = [1, 2, 3]
print(permute(my_list))
```

**Explanation:**

* **Operation**: The function generates all permutations of a list.
    
* **Steps**:
    
    * For each element in the list, it recursively finds all permutations of the remaining elements and appends the current element to each permutation.
        
    * This results in a factorial number of permutations because each element can be at each position.
        
* **Time Complexity**: The number of permutations of a list of size **n** is **n!**, leading to **O(n!)** time complexity.
    

# Conclusion

Each example demonstrates how the time complexity is derived based on the number of operations relative to the input size. The key is to analyze how the number of operations grows as the input size increases.

## Thank-you!

I am glad you made it to the end of this article. I hope you got to learn something, if so please leave a **Like** which will encourage me for my upcoming write-ups.p

* [My GitHub Repos](https://github.com/akxat)
    
* Connect with me on [Linkedin](https://www.linkedin.com/in/sharma-akshat/)
    
* Start [your own blogs](https://hashnode.com/@AkshatSharma/joinme)
    

%%[wid-1]