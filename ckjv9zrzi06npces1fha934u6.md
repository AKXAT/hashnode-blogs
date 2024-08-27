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
    

### Using LinkedList

This implementation demonstrates a stack data structure using a linked list in Python. Let's break down how it works:

### 1\. **Node Class**

The `Node` class is a basic building block for the linked list. Each `Node` object contains two attributes:

* `value`: This stores the data (or value) for the node.
    
* `next`: This is a reference (or pointer) to the next node in the linked list. If there is no next node, this will be `None`.
    

```python
class Node:
    def __init__(self, value=None, next=None) -> None:
        self.value = value
        self.next = next
```

### 2\. **Stack Class**

The `Stack` class manages the stack using the linked list, with several key methods:

* **Initialization (**`__init__`):
    
    * [`self.top`](http://self.top): This attribute points to the top of the stack. Initially, it's `None`, indicating the stack is empty.
        

```python
class Stack:
    def __init__(self) -> None:
        self.top = None
```

* **String Representation (**`__str__`):
    
    * This method returns a string representation of the stack. It traverses the linked list from the `top` node and builds a string with the values of each node, separated by arrows (`->`). The method omits the last arrow for a clean output.
        

```python
def __str__(self) -> str:
        mystr = "" 
        marker = self.top
        while marker != None:
            mystr = mystr + f"{marker.value}" + "-> "
            marker = marker.next
        return mystr[:-3]
```

* **Check if Stack is Empty (**`isempty`):
    
    * This method checks whether the stack is empty by verifying if [`self.top`](http://self.top) is `None`. If it is, the stack is empty and returns `True`; otherwise, it returns `False`.
        

```python
def isempty(self):
        return self.top == None
```

* **Push Method (**`push`):
    
    * This method adds a new element to the top of the stack.
        
    * A new `Node` is created with the given `value`.
        
    * If the stack is not empty ([`self.top`](http://self.top) is not `None`), the `next` attribute of this new node is set to the current `top`node.
        
    * The `top` of the stack is then updated to this new node.
        

```python
def push(self, value):
        new_node = Node(value=value)
        if self.top != None:
            new_node.next = self.top
        self.top = new_node
        return
```

### 3\. **Example Usage**

In the example usage:

* A new stack (`stack1`) is created.
    
* The `isempty` method is called, which returns `True` because the stack is initially empty.
    
* Several values (10, 20, 30, 40, 50, 60) are pushed onto the stack.
    
* After pushing these values, `isempty` is called again, which returns `False` because the stack now contains elements.
    
* The `print(stack1)` statement calls the `__str__` method, which prints the contents of the stack as `60-> 50-> 40-> 30-> 20-> 10`, showing that the most recently pushed element (60) is at the top of the stack.
    

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

    def push(self, value):
        new_node = Node(value=value)
        if self.top != None:
            new_node.next = self.top
        self.top = new_node
        return



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
```

### Using Deque

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