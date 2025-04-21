## **What is a Binary Search Tree (BST)?**

- A **Binary Search Tree (BST)** is a tree data structure where each node has at most two children (left and right).
- For every node:
  - The left child’s value is **less** than the node’s value.
  - The right child’s value is **greater** than the node’s value.
- The BST property makes searching for values efficient, with average time complexity of **O(log n)** for balanced trees.


| **Operation**              | **Explanation**                                                                 |
|----------------------------|---------------------------------------------------------------------------------|
| **Insert**                  | Inserts a new value into the Binary Search Tree.                                 |
| **Delete**                  | Deletes a node from the Binary Search Tree.                                     |
| **Find Closest Value**      | Finds the closest value to a given target number in the BST.                    |
| **Validate BST**            | Validates whether a tree is a valid Binary Search Tree by checking the rules.  |
| **Contains**                | Checks if a value is present in the Binary Search Tree.                         |


---

## 🛠️ **Create a Binary Search Tree**

- Define the Node and BST class.
- `insert()` adds values in the correct position following BST rules.

```javascript
// Node class
class Node {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

// BST class
class BST {
  constructor() {
    this.root = null;
  }
}

```

## **Insertion**

- Inserting a new value into a BST follows the rule of comparison:
  - If the value is smaller than the current node,go to left node.
  - If the value is larger, go to right node.
  - until leaf node

```javascript
insert(value) {
  const newNode = new TreeNode(value);
  if (this.root === null) {
    this.root = newNode;
  } else {
    let currentNode = this.root;
    while (true) {
      if (value < currentNode.value) {
        if (currentNode.left === null) {
          currentNode.left = newNode;
          break;
        } else {
          currentNode = currentNode.left;
        }
      } else {
        if (currentNode.right === null) {
          currentNode.right = newNode;
          break;
        } else {
          currentNode = currentNode.right;
        }
      }
    }
  }
}

```

## **Contains**

- This operation checks if a value is present in the BST by recursively comparing it with each node, following the same rules as insertion.

```javascript
// Check if a value exists in the BST
contains(value) {
  return this.containsNode(this.root, value);
}

containsNode(node, value) {
  if (node === null) {
    return false;
  }
  if (value < node.value) {
    return this.containsNode(node.left, value);
  } else if (value > node.value) {
    return this.containsNode(node.right, value);
  }
  return true;
}
```

## **Delete**

- Deleting a node involves three cases:
  1. **No children**: Simply remove the node.
  2. **One child**: Remove the node and link its parent directly to its child.
  3. **Two children**: Replace the node with the smallest node in its right subtree (or largest in its left) and remove that node.

```javascript
// Delete a value from the BST
delete(value) {
  this.root = this.deleteNode(this.root, value);
}

deleteNode(node, value) {
  if (node === null) {
    return null;
  }

  if (value < node.value) {
    node.left = this.deleteNode(node.left, value);
  } else if (value > node.value) {
    node.right = this.deleteNode(node.right, value);
  } else {
    // Node to be deleted
    if (node.left === null && node.right === null) {
      return null;
    } else if (node.left === null) {
      return node.right;
    } else if (node.right === null) {
      return node.left;
    }

    // Node with two children: Get the inorder successor
    let minNode = this.findMinNode(node.right);
    node.value = minNode.value;
    node.right = this.deleteNode(node.right, minNode.value);
  }
  return node;
}

findMinNode(node) {
  while (node.left !== null) {
    node = node.left;
  }
  return node;
}
```

## **Inorder Traversal**

- **Inorder traversal** visits nodes in the order: **Left → Node → Right**.
- This traversal produces the nodes in **sorted** order in a BST.

```javascript
// Inorder traversal (Left → Node → Right)
inorderTraversal(node = this.root) {
  if (node !== null) {
    this.inorderTraversal(node.left);
    console.log(node.value);
    this.inorderTraversal(node.right);
  }
}
```




## **Find Closest Value**

- This operation finds the closest value to a given target number in the BST.

```javascript
// Find the closest value to a given target
findClosestValue(target) {
  return this.findClosest(this.root, target, Infinity);
}

findClosest(node, target, closest) {
  if (node === null) return closest;

  if (Math.abs(target - node.value) < Math.abs(target - closest)) {
    closest = node.value;
  }

  if (target < node.value) {
    return this.findClosest(node.left, target, closest);
  } else if (target > node.value) {
    return this.findClosest(node.right, target, closest);
  }
  return closest;
}
```

## **Validate BST**

- This operation checks whether a given tree is a valid Binary Search Tree or not by ensuring that all nodes follow the BST property.

```javascript
// Validate if the tree is a valid BST
validateBST(node = this.root, min = null, max = null) {
  if (node === null) return true;

  if ((min !== null && node.value <= min) || (max !== null && node.value >= max)) {
    return false;
  }

  return this.validateBST(node.left, min, node.value) && this.validateBST(node.right, node.value, max);
}

```


## 📝 **Additional Things**


