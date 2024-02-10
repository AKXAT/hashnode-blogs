---
title: "Implementing General Tree using Python"
datePublished: Fri Feb 09 2024 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: ckkduqbh603ly81s1b2sc6aoy
slug: implementing-general-tree-using-python
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1611656464312/ybkQCyKGL.png
tags: python, data-structures, python3, 2articles1week, python-beginner

---

> Implementing General Tree using Python

[&lt;- Go Back to Index](https://carboncoffee.hashnode.dev/datastructures)

## What is a Tree?

* A tree is a widely used abstract data type that simulates a hierarchical tree structure, with a root value and subtrees of children with a parent node, represented as a set of linked nodes.
    

Let's Take an example to understand the structure of a **Tree**.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610616979713/xpHv_Kd8a.png align="left")

* You must have seen this type of implementation on any of the e-commerce websites that you visit. There will be a \*\*Main Category \*\* (Electronics), then it might be linked to different **Sub Categories**(Such as - Laptop, cellphones) and then the final **Products**(such as MacBook, iPhone etc)
    
* Now to represent this we can't use Linear Data Structures such as --&gt; Array, Linked List, Stacks or Queues. So we need a hierarchical representation for this hence we will use **Tree**. There could be different Levels to a single **Tree**.
    

## General Tree

* **Root Node** --&gt; A root node is either the topmost or the bottom node in a tree data structure, depending on how the tree is represented visually.
    
* **Node** --&gt; A tree is a collection of entities called nodes . Nodes are connected by edges. Each node contains a value or data, and it may or may not have a child node
    

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610616542590/k-m4BHJkO.png align="left")

* **Parent and Children** --&gt; Child is a node that has a parent node. The parent is a node that has an edge over a child node. The leaf is a node that does not have a child node in the tree.
    

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610616815403/7zcYEVGE9.png align="left")

### Let's Implement General Tree in Python

* Creating a Tree class and adding objects of a class (data, children and parent)
    

```plaintext
class TreeNode:
    def __init__(self,data):
        self.data = data
        self.children = []
        self. parent = None
```

* Now we can add an Add child method also pointing the parent of that added child to the instance of the class
    

```plaintext
    def add_child(self,child):
        self.child = child 
        child.parent = self
        self.children.append(child)
```

> 1. `def add_child(self, child):`: This is a method within the `TreeNode` class that takes another `TreeNode` object (`child`) as a parameter. It's used to add a child node to the current node in the tree.
>     
> 2. `self.child = child`: This line incorrectly assigns the `child` node to `self.child`. However, this is a mistake because it overwrites the previous value of `self.child` with the new `child`. This should instead append the new child to the list of children. The correct line should be `self.children.append(child)`.
>     
> 3. `child.parent = self`: This line correctly sets the parent of the `child` node to be the current node (`self`). It establishes a bidirectional relationship between the parent and child nodes, allowing navigation up and down the tree.
>     

* We will now create a function for **finding the Level of the current child**
    

```plaintext
    def get_level(self):
        level = 0 
        p = self.parent
        while p :
            p = p.parent
            level += 1
        return level
```

> This `get_level` method is designed to determine the level of a node within the tree. The level of a node represents its distance from the root node. Here's a breakdown of how the method works:
> 
> 1. **Initialization**:
>     
>     * `level = 0`: This variable is initialized to keep track of the level of the current node. It starts at 0.
>         
>     * `p = self.parent`: The variable `p` is assigned to the parent node of the current node (`self`). This allows traversal up the tree starting from the current node.
>         
> 2. **Traversal Up the Tree**:
>     
>     * `while p:`: This initiates a loop that continues as long as there is a valid parent node (`p`) to traverse.
>         
>     * `p = p.parent`: Inside the loop, `p` is updated to point to the parent of the current `p`. This effectively moves up one level in the tree hierarchy.
>         
>     * `level += 1`: With each iteration of the loop, the `level` variable is incremented by 1. This keeps track of the number of levels traversed.
>         
> 3. **Return Level**:
>     
>     * After the loop terminates (when `p` becomes `None`, indicating that there are no more parent nodes), the method returns the value of `level`, which represents the level of the original node.
>         

* Now in order to get the output in the form of a TREE we will make use of the above \*\*get\_level function \*\*and create a \*\*Print function \*\*
    

```plaintext
    def print_tree(self):
        print('  '*self.get_level() + '|--', end = '')
        print(self.data)
        if self.children:
            for each in self.children:
                each.print_tree()
```

> This `print_tree` method is used to print the tree starting from the current node, following a depth-first traversal approach. Let's break down how it works:
> 
> 1. **Print Node Data with Indentation**:
>     
>     * `print(' '*self.get_level() + '|--', end='')`: This line prints an indentation that corresponds to the level of the current node in the tree. The amount of indentation is determined by multiplying two spaces (`' '`) by the level of the current node, which is obtained by calling the `get_level` method. Then, it prints `|--` to denote the node, without moving to the next line.
>         
>     * `print(`[`self.data`](http://self.data)`)`: This line prints the data stored in the current node.
>         
> 2. **Recursive Call for Children**:
>     
>     * `if self.children:`: This conditional statement checks if the current node has any children.
>         
>     * `for each in self.children:`: If the current node has children, it iterates over each child node.
>         
>     * `each.print_tree()`: For each child node, it recursively calls the `print_tree` method on that child node. This recursive call effectively prints the subtree rooted at the child node, allowing the entire tree to be printed recursively.
>         
> 
> By combining these steps, the `print_tree` method prints the entire tree rooted at the current node in a structured and visually informative manner, with appropriate indentation to represent the hierarchical structure of the tree. The use of recursion ensures that all nodes and subtrees are printed correctly, following a depth-first traversal pattern.

* The main RUN function will create the class and add the child nodes to it
    

```plaintext
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

* Now let's sum up all the functions under one single program and try to execute it.
    

```plaintext
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

* The output of the above code will be
    

```plaintext
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

## Thank-you!

I am glad you made it to the end of this article. I hope you got to learn something, if so please leave a **Like** which will encourage me for my upcoming write-ups.

* [My GitHub Repos](https://github.com/akxat)
    
* Connect with me on [Linkedin](https://www.linkedin.com/in/sharma-akshat/)
    
* Start [your own blogs](https://hashnode.com/@AkshatSharma/joinme)
    

%%[wid-1]