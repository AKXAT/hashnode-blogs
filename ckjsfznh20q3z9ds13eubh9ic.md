## Linked List using Python

### What is the issue with Arrays ?

If you want to insert or delete an element in an array at a given location then swap every element by one address space and hence the Big O complexity is O(n) .  [Click here to view the article on Arrays](https://carboncoffee.hashnode.dev/introduction-to-arrays) 

# What is Linked List?

A **linked list ** is a linear collection of data elements , in which each element points to the next. The first element contains the address of the second element and the second element contains the address of the third element and so on till the last element contains null. 
It is a data structure consisting of a collection of nodes which together represent a sequence.

The below image is the pictorial representation of a **Linked List.**


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610350489513/IoPDSDUXV.png)

### Insertion in the Linked List 

The below image represents a typical insertion in the Linked List

So in case you want to **insert 284 at index 1** , then this is how it will be done?

All you need to do is change the address pointer at the element 298 - which is currently  **0x00A1**  (of the second element) to the element that you want to do - which is **0xC702** **( element 284 )
**
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610350669689/pwEg4Rh2r.png)

The insertion becomes very easy because now you are just modifying the links unlike arrays in which you had to shift each element by a index.

The  [Big O complexity](https://carboncoffee.hashnode.dev/big-o-notation-quick-recap)  for  
 
1.  Inserting Element at beginning is - O(1)
2. Deleting Element at beginning is - O(1)
3. Inserting/Deleting Element at end is - O(n) - because you need to traverse through all the elements via their address to reach the end.
4. Accessing Element by Value - O(n) 

### What is Doubly Linked List ?

A doubly linked list is a linked data structure that consists of a set of sequentially linked records called nodes. Each node contains three fields: 
1. Two link fields(the first contains the address of previous element and the other contains the address of the next element) 
2. One data field/element field.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610352881820/hA2IH7Nrv.png)

This way the backward traversal becomes very easy.

# Let's implement Linked List in Python

- **Creating a class for Node , so we can create or change node functionality whenever we feel like  
**


```
class Node:
    #Class for creating a Node which contains the data and the next address 
    #If this is the first node hence the next value will be none
    def __init__(self,data=None,next=None):
        self.data = data
        self.next = next
``` 
 

- **Creating a class for Linked List to add functions 
**

```
class LinkedList:
    #Creating a class for LinkedList which contains various functions 
    def __init__(self):
        #head of the Linked List
        self.head = None
``` 
 

- **Function for adding element at the start **
    
    
```
def insert_at_start(self,data):
        #Function for inserting at the starting 
        new_node = Node(data,self.head) #creating a new node 
        self.head = new_node #now head will point to newly created node
``` 
- **Function for inserting element at the end 
**

```
def insert_at_end(self,data):
        if self.head is None: #which means there is nothing in the Linked List
            new_node = Node(data,self.head) #creating a new node 
            self.head = new_node #now head will point to newly created node
            return
        temp = self.head
        while temp.next:
            temp = temp.next
        temp.next = Node(data,None)
``` 


- **Function for finding length of the Linked List **

```
    def find_length(self):
        temp = self.head
        count = 0
        while temp:
            count += 1
            temp = temp.next
        #print(count)
        return count
``` 

- **Function for deleting element at any index **

```
def delete_at_index(self,index):
        if index < 0 or index >= self.find_length():
            raise Exception("Invalid Index")
        if index == 0 :
            self.head = self.head.next
            return
        count = 0 
        temp = self.head
        while temp:
            if count == index - 1:
                temp.next = temp.next.next
                break
            temp = temp.next
            count += 1    
``` 

- **Function for printing the Nodes**
    
    
```
def print(self): #funtion for prinitng the nodes and the datas
        element = ''
        if self.head is None:
            element += 'Null'
        temp = self.head
        while temp: #looping through the head to check the next element 
            element += str(temp.data)+ '--->'
            temp = temp.next
        print(element)
``` 


- **Main function for creating the Linked List **

```
if __name__ == '__main__':
    ll = LinkedList()  
    ll.insert_at_start(2)
    ll.insert_at_start(3)
    ll.insert_at_start(4)
    ll.insert_at_end(5)
    ll.insert_at_end(9)
    ll.find_length()
    #ll.delete_at_index(9)
    ll.delete_at_index(2)
    ll.print()

``` 



### Well , here is the whole code for you ,  try running yourself and add new features.


```
class Node:
    #Class for creating a Node which contains the data and the next address 
    #If this is the first node hence the next value will be none
    def __init__(self,data=None,next=None):
        self.data = data
        self.next = next
class LinkedList:
    #Creating a class for LinkedList which contains various functions 
    def __init__(self):
        #head of the Linked List
        self.head = None

    def insert_at_start(self,data):
        #Function for inserting at the starting 
        new_node = Node(data,self.head) #creating a new node 
        self.head = new_node #now head will point to newly created node
    def insert_at_end(self,data):
        if self.head is None: #which means there is nothing in the Linked List
            new_node = Node(data,self.head) #creating a new node 
            self.head = new_node #now head will point to newly created node
            return
        temp = self.head
        while temp.next:
            temp = temp.next
        temp.next = Node(data,None)

    def find_length(self):
        temp = self.head
        count = 0
        while temp:
            count += 1
            temp = temp.next
        #print(count)
        return count

    def delete_at_index(self,index):
        if index < 0 or index >= self.find_length():
            raise Exception("Invalid Index")
        if index == 0 :
            self.head = self.head.next
            return
        count = 0 
        temp = self.head
        while temp:
            if count == index - 1:
                temp.next = temp.next.next
                break
            temp = temp.next
            count += 1          

    def print(self): #funtion for prinitng the nodes and the datas
        element = ''
        if self.head is None:
            element += 'Null'
        temp = self.head
        while temp: #looping through the head to check the next element 
            element += str(temp.data)+ '--->'
            temp = temp.next
        print(element)


if __name__ == '__main__':
    ll = LinkedList()  
    ll.insert_at_start(2)
    ll.insert_at_start(3)
    ll.insert_at_start(4)
    ll.insert_at_end(5)
    ll.insert_at_end(9)
    ll.find_length()
    #ll.delete_at_index(9)
    ll.delete_at_index(2)
    ll.print()

``` 





You Just saw creating a new Linked List using Python and adding some functionality such as Add and Delete . Now you can go ahead and make few more functions such as inserting at a given index . Even you can try creating a Doubly Linked List.

*Hope you liked the content , leave a like you learned something today and follow back for more of the Data Structure! *


