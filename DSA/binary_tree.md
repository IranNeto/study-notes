# Tree

Tree is a data structure that holds data that conforms in some kind of hierarchy. For example, the file system on a computer.

```
      tree
      ----
       j    <-- root
     /   \
    f      k  
  /   \      \
 a     h      z    <-- leaves
```

1. Trees provide moderate access/search (quicker than **Linked List** and slower than **arrays**)
2. Trees provide moderate insertion/deletion (quicker than **Arrays** and slower than **Unordered Linked List**s). 
3. Like Linked Lists and unlike Arrays, Trees don’t have an upper limit on number of nodes as nodes are linked using pointers.

Good examples that a tree fits in the problem:

1. Manipulate hierarchical data. 
2. Make information easy to search (see tree traversal). 
3. Manipulate sorted lists of data. 
4. As a workflow for compositing digital images for visual effects. 
5. Router algorithms 
6. Form of a multi-stage decision-making (see business chess). 

# Binary tree

Binary Tree is a tree whose elements have at most 2 children is called a binary tree. They have 2 nodes o 0 nodes.
Since each element in a binary tree can have only 2 children, we typically name them the left and right child.

## Properties

MAX NUMBER OF LEAVES IN A LEVEL 'L: 2ˆL

MAX NUMBER OF LEAVES IN A BINARY TREE: 2ˆ(h+1) - 1, where 'h' is the heigth [0...]

MIN POSSIBLE TREE LEVEL GIVEN THE NUMBER OF LEAVES: |Log2(N + 1)| - 1, where N is the number of leaves

A BINARY TREE WITH N LEAVES HAS AT LEAST |Log2(N)| + 1 LEVELS;

THE NUMBER OF LEAVES NODES (0 LEAVES) IS ALWAYS ONE MORE THE NUMBER OF INTERNAL LEAVES (2 LEAVES): L = T + 1 where 'L' is the number of leaves and 'T' is the number
of internal leaves

L = (number of leaves in the last level) 2^(h + 1)
T = (total leaves) - (number of leaves in the last level) = 2^(h+1) - 1 - 2ˆ(h) = 2 * 2^h - 1 - 2^(h) = 2ˆh - 1 = L - 1
L = T + 1

## Subtypes and more properties

* Full Binary Tree A Binary Tree is a full binary tree if every node has 0 or 2 children.

* Complete Binary Tree: A Binary Tree is a Complete Binary Tree if all the levels are completely
filled except possibly the last level and the last level has all keys as left as possible 

* Perfect Binary Tree A Binary tree is a Perfect Binary Tree in which all the internal nodes have two children and all leaf nodes are at the same level. 

* A binary tree is balanced if the height of the tree is O(Log n) where n is the number of nodes.

* A degenerate (or pathological) tree A Tree where every internal node has one child. Such trees are performance-wise same as linked list. 
