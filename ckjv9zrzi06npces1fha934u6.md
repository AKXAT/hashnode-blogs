## Implementing Stack in Python

> 
 [<- Go Back to Index ](https://carboncoffee.hashnode.dev/datastructures) 


## What are Stacks?
a stack is an abstract data type that serves as a collection of elements, with two main principal operations: **Push**, which adds an element to the collection, and **Pop**, which removes the most recently added element that was not yet removed. This is know as **Last In First Out** or **LIFO**.


 [Big O complexity](https://carboncoffee.hashnode.dev/big-o-notation-quick-recap)  for Pushing and Popping is O(1) and Searching element by value is O(n).


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610524178403/onXDrQISU.png)

### Use cases for STACK .
1. When we are calling a Function and then that Function calls another function internally then this is managed by **Stack**
2. The Undo command in any editor uses **Stack** to track down the last set of operations 
3. When you visit a website **A** and you open a page from **A** to **B** and then in **B** you open a certain page **C**. So the Go Back on Page **C** will take you back to **B** and then from **B** the back operation will take you to **A**. This is implemented using **Stack**. The Below code represents the same.

```
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
### Implementing Stacks 
1. We can implement **Stacks** using  [Dynamic Array](https://carboncoffee.hashnode.dev/introduction-to-arrays)  but there is a problem with this . When you are inserting in a Dynamic Array , first it will allocate a random continues memory location and when its gets filled it will again allocate double the size of memory location and then it will copy all old elements to the new location. Hence they are not recommended for implementing **Stacks**

2. To overcome this we make use of **DEQUE** in Python

### Using Deque 

A double-ended queue, or deque, has the feature of adding and removing elements from either end. The Deque module is a part of collections library. It has the methods for adding and removing elements which can be invoked directly with arguments. In the below program we import the collections module and declare a deque. Without need of any class we use the in-built implement methods directly.

- Importing Deque

```
from collections import deque
stack = deque()
``` 
- Now let's append the elements in the Stack 

```
from collections import deque
stack = deque()
stack.append('https://carboncoffee.hashnode.dev/')
stack.append('https://carboncoffee.hashnode.dev/introduction-to-arrays')
stack.append('https://carboncoffee.hashnode.dev/big-o-notation-quick-recap')
print(stack)
``` 


- Let's implement all these functions using a class STACK in Python


```
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

**So , This was the quick overview of Stacks in Python . I hope you liked the article . Follow back for the more upcoming article**


> Leave a like if you learned something today.








