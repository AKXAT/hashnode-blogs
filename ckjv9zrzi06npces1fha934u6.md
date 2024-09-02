---
title: "Implementing Stack in Python"
datePublished: Mon Jan 18 2021 10:23:03 GMT+0000 (Coordinated Universal Time)
cuid: ckjv9zrzi06npces1fha934u6
slug: implementing-stack-in-python
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1610529274626/KKuRdNSUZ.png
tags: python, data-structures, python3, stack, 2articles1week

---

[&lt;- Go Back to Index](https://carboncoffee.hashnode.dev/datastructures)

## **What is a Stack?**

A stack is an abstract data type that serves as a collection of elements, characterized by two principal operations: **Push** and **Pop**. The **Push** operation adds an element to the top of the stack, while the **Pop** operation removes the most recently added element that has not yet been removed. This behaviour is known as **Last In, First Out** (LIFO).

[Big O complexity](https://carboncoffee.hashnode.dev/big-o-notation-quick-recap) for Pushing and Popping is O(1) and Searching element by value is O(n).

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610524178403/onXDrQISU.png align="left")

### **Use Cases for a Stack**

1. **Function Calls Management**: When a function calls another function internally, the current function’s state is pushed onto a stack before control is passed to the called function. This allows the system to return to the previous function once the current one has finished executing. This process is managed by the call stack.
    
2. **Undo Operation in Editors**: The undo command in text editors or other software uses a stack to keep track of the most recent operations. Each action is pushed onto the stack, and when an undo is performed, the last action is popped off the stack and reversed.
    
3. **Browser History Navigation**: When navigating between web pages, the browser maintains a stack of pages. For example, if you visit website A, then navigate to page B, and finally to page C, the "Go Back" button will take you back from C to B, and another press will take you from B to A. This back navigation is implemented using a stack.
    

```python
s = []
s.append('https://carboncoffee.hashnode.dev/')
s.append('https://carboncoffee.hashnode.dev/introduction-to-arrays')
s.append('https://carboncoffee.hashnode.dev/big-o-notation-quick-recap')
print(s.pop())
#output - https://carboncoffee.hashnode.dev/big-o-notation-quick-recap
print(s.pop())
#output - https://carboncoffee.hashnode.dev/introduction-to-arrays
print(s.pop())
#output - https://carboncoffee.hashnode.dev/'
```

### **Implementing Stacks**

1. **Using Linked Lists**: A stack can be efficiently implemented using a linked list. In this approach, all operations (like push and pop) are performed at the head of the linked list. This allows for constant time operations, as adding or removing an element only involves updating the head pointer.
    
2. **Using Dynamic Arrays**: Stacks can also be implemented using dynamic arrays (e.g., Python lists). However, while dynamic arrays provide quick access to elements, they come with a caveat. When the array reaches its capacity, it needs to allocate a new, larger block of contiguous memory (usually double the size of the original), and then copy all existing elements to this new memory location. This reallocation and copying process can be inefficient, particularly for large data sets. Despite this, dynamic arrays are commonly used for stack implementation due to their simplicity and support in many programming languages.
    
3. **Using Deque in Python**: To overcome some of the limitations of dynamic arrays, especially with regard to reallocation and resizing, you can use a `deque` (double-ended queue) from Python’s `collections` module. A `deque` is optimized for fast append and pop operations from both ends, making it a more efficient choice for implementing stacks in scenarios where performance is critical.
    

# Using LinkedList

This implementation demonstrates a stack data structure using a linked list in Python. Let's break down how it works:

### 1\. **Node Class**

```python
class Node:
    def __init__(self, value=None, next=None) -> None:
        self.value = value
        self.next = next
```

* The `Node` class represents an individual element (or node) in the linked list.
    
* Each node contains:
    
    * `value`: The data stored in the node.
        
    * `next`: A pointer/reference to the next node in the list.
        

### 2\. **Stack Class**

```python
class Stack:
    def __init__(self) -> None:
        self.top = None
```

* The `Stack` class manages the linked list that represents the stack.
    
* The stack is initialized with [`self.top`](http://self.top) `= None`, indicating that the stack is empty.
    

### 3\. **String Representation (**`__str__` method)

```python
def __str__(self) -> str:
    mystr = "" 
    marker = self.top
    while marker != None:
        mystr = mystr + f"{marker.value}" + "-> "
        marker = marker.next
    return mystr[:-3]
```

* This method returns a string representation of the stack.
    
* It traverses the linked list from `top` to the end, appending each node's value to a string.
    
* The "-&gt;" symbol is used to denote the link between nodes.
    
* `mystr[:-3]` removes the trailing "-&gt;" from the final string.
    

### 4\. **Check if Stack is Empty (**`isempty` method)

```python
def isempty(self):
    return self.top == None
```

* This method checks whether the stack is empty by verifying if [`self.top`](http://self.top) is `None`.
    
* Returns `True` if the stack is empty, otherwise `False`.
    

### 5\. **Peek at the Top Element (**`peek` method)

```python
def peek(self):
    if self.isempty():
        return "Stack Empty"
    return self.top.value
```

* This method returns the value of the top element of the stack without removing it.
    
* If the stack is empty, it returns "Stack Empty".
    

### 6\. **Push an Element onto the Stack (**`push` method)

```python
def push(self, value):
    new_node = Node(value=value)
    if self.top != None:
        new_node.next = self.top
    self.top = new_node
    return
```

* This method adds a new element to the stack.
    
* A new `Node` is created with the given `value`.
    
* If the stack is not empty ([`self.top`](http://self.top) `!= None`), the new node’s `next` pointer is set to the current `top` node.
    
* The `top` pointer is then updated to point to the new node, making it the top of the stack.
    

### 7\. **Pop an Element from the Stack (**`pop` method)

```python
def pop(self):
    if self.isempty():
        return "Stack Empty"
    self.top = self.top.next 
```

* This method removes the top element from the stack.
    
* If the stack is empty, it returns "Stack Empty".
    
* Otherwise, it updates the `top` pointer to the next node in the stack, effectively removing the current top node.
    

### 8\. **Using the Stack**

```python
stack1 = Stack()
print(stack1.isempty())   # True
stack1.push(10)
stack1.push(20)
stack1.push(30)
stack1.push(40)
stack1.push(50)
stack1.push(60)
print(stack1.isempty())   # False
print(stack1)             # 60-> 50-> 40-> 30-> 20-> 10
print(stack1.peek())      # 60
stack1.pop()
print(stack1)             # 50-> 40-> 30-> 20-> 10
```

* The example code creates a stack and demonstrates its operations:
    
    * `stack1.isempty()` checks if the stack is empty initially and after pushing elements.
        
    * `stack1.push()` adds elements to the stack.
        
    * `stack1` (string representation) shows the stack’s current state.
        
    * `stack1.peek()` shows the top element without removing it.
        
    * `stack1.pop()` removes the top element and updates the stack.
        

Final Code

```python
class Node:
    def __init__(self, value=None, next=None) -> None:
        self.value = value
        self.next = next


class Stack:
    def __init__(self) -> None:
        self.top = None

    def __str__(self) -> str:
        mystr = "" 
        marker = self.top
        while marker != None:
            mystr = mystr + f"{marker.value}" + "-> "
            marker = marker.next
        return mystr[:-3]
    def isempty(self):
        return self.top == None

    def peek(self):
        if self.isempty():
            return "Stack Emtpty"
        return self.top.value
    def push(self, value):
        new_node = Node(value=value)
        if self.top != None:
            new_node.next = self.top
        self.top = new_node
        return
    def pop(self):
        if self.isempty():
            return "Stack Empty"
        self.top = self.top.next 


stack1 = Stack()
print(stack1.isempty())
stack1.push(10)
stack1.push(20)
stack1.push(30)
stack1.push(40)
stack1.push(50)
stack1.push(60)
print(stack1.isempty())
print(stack1)
print(stack1.peek())
stack1.pop()
print(stack1)
```

# Using Deque

A double-ended queue, or deque, has the feature of adding and removing elements from either end. The Deque module is a part of the collections library. It has the methods for adding and removing elements that can be invoked directly with arguments. In the below program we import the collections module and declare a deque. Without the need of any class, we use the in-built implement methods directly.

* Importing Deque
    

```python
from collections import deque
stack = deque()
```

* Now let's append the elements in the Stack
    

```python
from collections import deque
stack = deque()
stack.append('https://carboncoffee.hashnode.dev/')
stack.append('https://carboncoffee.hashnode.dev/introduction-to-arrays')
stack.append('https://carboncoffee.hashnode.dev/big-o-notation-quick-recap')
print(stack)
```

* Let's implement all these functions using a class STACK in Python
    

```python
from collections import deque
class Stack:
    def __init__(self):
        self.bucket = deque()
    def push(self,value):
        self.value = value 
        self.bucket.append(value)
    def pop(self): 
        #print(self.bucket.pop())
        return self.bucket.pop()
    def last_inserted_value(self):
        #print(self.bucket[-1])
        return self.bucket[-1]
    def is_empty(self):
        if len(self.bucket)==0:
            #print("True")
            return True 
        else :
            #print(len(self.bucket))
            return len(self.bucket)

if __name__ == '__main__':
    S = Stack()
    S.push(12)
    S.push(11)
    S.push(12)
    #S.pop()
    S.last_inserted_value()
    #S.is_empty()
```

## Thank-you!

I am glad you made it to the end of this article. I hope you got to learn something, if so please leave a **Like** which will encourage me for my upcoming write-ups.

* [My GitHub Repos](https://github.com/akxat)
    
* Connect with me on [Linkedin](https://www.linkedin.com/in/sharma-akshat/)
    
* Start [your own blogs](https://hashnode.com/@AkshatSharma/joinme)
    

%%[wid-1]