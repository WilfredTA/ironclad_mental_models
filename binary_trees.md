
# Binary Trees
## Table of Contents
1. Introduction
2. Approaches to Binary Tree Problems
  a. Divide and Conquer
  b. Recursive Traversal
  c. Iterative Traversal
  d. Level order traversal
3. Binary Tree Problems


### Introduction

A binary tree is either empty, or a root node with a left and right subtree. The subtrees themselves are binary trees.

Here is a binary tree code for use in any of the problems:

```
class TreeNode
  attr_accessor :left, :right, :value
  
  def initialize(value)
    @value = value
    @left = nil
    @right = nil
  end
end

```

There are different types of binary trees:
*Full binary tree*: A binary tree in which every node other than the leaves have two child nodes.
*Perfect binary tree*: A full binary tree in which all the leaves are at the same depth.
*Complete binary tree*: A binary tree in which every level except possibly the last is filled and all nodes are as far left as possible.

Binary trees are inherently recursive structures which can be observed by its definition as a "root node with left and right subtrees". They are therefore amenable to recursive solutions, so let's talk about when a recursive solution is more appropriate than an iterative one:

A recursive solution is appropriate when an iterative solution would require deeply nested loops **or** would require a varying number of nested loops depending on the input.

A recursive solution is also appropriate if a problem demonstrates optimal substructure, which is observed when the solution to a problem can be derived entirely via its sub problems.

An iterative solution can simulate levels of a recursive stack by using an custom-made stack data structure to keep track of upcoming values to be passed into the iteration. We will see this when we discuss an iterative approach to traversing binary trees.

### Approaches to Binary Tree Problems

A binary tree problem can almost always be solved with either divide and conquer or one of the four traversal methods. First, let's go over Divide and Conquer.

Divide and conquer is a recursive paradigm that repeatedly decomposes a problem into two or more independent subproblems until it reaches an instance of the sub problem that is so trivial that the return value can be determined, and then returned, without further recursive calls. The return values are then compined on each level of the recursive call stack, "building up" a solution. These subproblems are the same structure of the original problem but with decreasingly simpler inputs.

Mergesort and quicksort are two examples of divide and conquer algorithms.

**Mental Model for DnC solutions to Binary Tree Problems:**

1. Determine the base case: what is the simplest solution to the problem? (usually involves hitting a leaf node)
2. Recursively hit the right and left branches and store the results of these recursive calls
3. Combine the simple solutions in such a way that the combinations to the simple solutions build up toward the complex solution

Think of divide and conquer as normal recursion (reducing the input into smaller and smaller inputs until the simplest input possible) + the process in reverse once the base case is hit (building up those simpler, smaller inputs into more complex ones).



