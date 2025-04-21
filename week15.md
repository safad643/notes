# Trees in DSA🌳

## **Types of Trees**

| **Tree Type**                          | **Description**                                                                                                                                                                        |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Binary Tree**                        | Each node has at most two children: left and right.                                                                                                                                    |
| **[Binary Search Tree (BST)](BST.md)** | A binary tree where the left child is smaller and the right child is larger than the parent.                                                                                           |
| **[[AVL Tree]]**                       | A self-balancing binary search tree. Balance factor keeps track of the difference in heights between the left and right subtrees.                                                      |
| **[[Heap]]**                           | A tree-based structure where the parent node’s value is either greater than (Max-Heap) or less than (Min-Heap) the value of its children.                                              |
| **[[Trie]]**                           | A tree for storing strings, often used for prefix searching.                                                                                                                           |
| **Segment Tree**                       | A binary tree used to store intervals or segments, useful for range queries.                                                                                                           |
| **B Tree**                             | A self-balancing tree data structure that maintains sorted data and allows searches, insertions, and deletions in logarithmic time. It is commonly used in databases and file systems. |
| **Red-Black Tree**                     | A self-balancing binary search tree where each node has an extra bit for determining the color (red or black), ensuring balance during insertions and deletions.                       |


## **Tree Traversal**

- **Inorder Traversal**  
  Visit the left subtree → Node → Right subtree.

- **Preorder Traversal**  
  Visit Node → Left subtree → Right subtree.

- **Postorder Traversal**  
  Visit Left subtree → Right subtree → Node.

- **Level-order Traversal**  
  Visit nodes level by level from left to right, typically implemented with a queue.


## **Time Complexities**

- **Searching**: O(log n) for balanced trees, O(n) for unbalanced trees.
- **Insertion/Deletion**: O(log n) for balanced trees, O(n) for unbalanced trees.
- **Traversal**: O(n), as each node is visited once.

## **Applications of Trees**

- **File Systems**  
  Used for organizing and storing files in a directory structure.

- **Database Indexing**  
  B-trees and B+ trees are used for indexing in databases to enable fast searches.

- **Routing Algorithms**  
  Used in network pathfinding to determine optimal routes.

- **Expression Parsing**  
  Syntax trees are used to parse mathematical expressions and evaluate them.

