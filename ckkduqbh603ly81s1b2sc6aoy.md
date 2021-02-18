## Implementing General Tree using Python

> 
 [<- Go Back to Index ](https://carboncoffee.hashnode.dev/datastructures) 


## What is a Tree?

- A tree is a widely used abstract data type that simulates a hierarchical tree structure, with a root value and subtrees of children with a parent node, represented as a set of linked nodes.

Let's Take an example to understand the structure of a **Tree**. 



![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610616979713/xpHv_Kd8a.png)

- You must have seen this type of implementation on any of the e-commerce websites that you visit. There will be a **Main Category ** (Electronics), then it might be linked to different **Sub Categories**(Such as - Laptop, cellphones) and then the final **Products**(such as MacBook, iPhone etc)   

- Now to represent this we can't use Linear Data Structures such as -->  Array, Linked List, Stacks or Queues. So we need a hierarchical representation for this hence we will use  **Tree**. There could be different Levels to a single **Tree**.

## General Tree 

- **Root Node** --> A root node is either the topmost or the bottom node in a tree data structure, depending on how the tree is represented visually.
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610616370780/53zbGwTxf.png)

- **Node** --> A tree is a collection of entities called nodes . Nodes are connected by edges. Each node contains a value or data, and it may or may not have a child node 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610616542590/k-m4BHJkO.png)

- **Parent and Children** --> Child is a node that has a parent node. The parent is a node that has an edge over a child node. The leaf is a node that does not have a child node in the tree. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610616815403/7zcYEVGE9.png)

### Let's Implement General Tree in Python
- Creating a Tree class and adding objects of a class (data, children and parent) 

```
class TreeNode:
    def __init__(self,data):
        self.data = data
        self.children = []
        self. parent = None
``` 
 - Now we can add an Add child method also pointing the parent of that added child to the instance of the class


```
    def add_child(self,child):
        self.child = child 
        child.parent = self
        self.children.append(child)
``` 

- We will now create a function for **finding the Level of the current child**

```
    def get_level(self):
        level = 0 
        p = self.parent
        while p :
            p = p.parent
            level += 1
        return level 
``` 
- Now in order to get the output in the form of a TREE we will make use of the above **get_level function **and create a **Print function **


```
    def print_tree(self):
        print('  '*self.get_level() + '|--', end = '')
        print(self.data)
        if self.children:
            for each in self.children:
                each.print_tree()
``` 

- The main RUN function which will create the class and add the child nodes to it 


```
def run():
    root = TreeNode('Eletronics')
    laptop = TreeNode('Laptop')
    root.add_child(laptop)

    laptop.add_child(TreeNode('Mac'))
    laptop.add_child(TreeNode('Windows'))
    laptop.add_child(TreeNode('Linux'))
    tv = TreeNode('TV')
    root.add_child(tv)
    tv.add_child(TreeNode('LG'))
    tv.add_child(TreeNode('Samsung'))
    tv.add_child(TreeNode('Apple'))
    root.print_tree()

    #return root
if __name__ == '__main__':
    run()
    pass
``` 

- Now let's sum up all the functions under one single program and try to execute it.

```
class TreeNode:
    def __init__(self,data):
        self.data = data
        self.children = []
        self. parent = None
    def add_child(self,child):
        self.child = child 
        child.parent = self
        self.children.append(child)
    def get_level(self):
        level = 0 
        p = self.parent
        while p :
            p = p.parent
            level += 1
        return level 
    def print_tree(self):
        print('  '*self.get_level() + '|--', end = '')
        print(self.data)
        if self.children:
            for each in self.children:
                each.print_tree()
        
def run():
    root = TreeNode('Eletronics')
    laptop = TreeNode('Laptop')
    root.add_child(laptop)

    laptop.add_child(TreeNode('Mac'))
    laptop.add_child(TreeNode('Windows'))
    laptop.add_child(TreeNode('Linux'))
    tv = TreeNode('TV')
    root.add_child(tv)
    tv.add_child(TreeNode('LG'))
    tv.add_child(TreeNode('Samsung'))
    tv.add_child(TreeNode('Apple'))
    root.print_tree()

    #return root
if __name__ == '__main__':
    run()
    pass
    
    
        

``` 
- The output of the above code will be 

```
|--Electronics
  |--Laptop
    |--Mac
    |--Windows
    |--Linux
  |--TV
    |--LG
    |--Samsung
    |--Apple
``` 

**
So, This was the quick overview of General Tree in Python. I hope you liked the article. Follow back for the more upcoming article**


> 
Leave a like if you learned something today.


