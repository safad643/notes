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
insert(value, c = this.root) {
  let newNode = new node(value);

  if (!this.root) {
    this.root = newNode;
    return 'insert success';
  }

  if (value > c.value) {
    return c.right ? this.insert(value, c.right) : (c.right = newNode, 'insert success');
  } else if (value < c.value) {
    return c.left ? this.insert(value, c.left) : (c.left = newNode, 'insert success');
  } else {
    return 'duplicate elements not allowed';
  }
}
```


## **Contains**


```javascript
contains(value, c = this.root) {
  if (!c) return false;
  if (c.value === value) return true;
  if (value < c.value) return this.contains(value, c.left);
  return this.contains(value, c.right);
}
```


## **Delete**

- Deleting a node involves three cases:
  1. **No children**: Simply remove the node.
  2. **One child**: Remove the node and link its parent directly to its child.
  3. **Two children**: Replace the node with the smallest node in its right subtree (or largest in its left) and remove that node.


```javascript
delete(value, c = this.root, parent = null) {
  if (!c) return 'value doesnt exist in this bst';
  if (value > c.value) return this.delete(value, c.right, c);
  else if (value < c.value) return this.delete(value, c.left, c);
  else {
    if (parent === null) {
      this.root = child;
    }
    else if (c.left && c.right) {
      let minc = c.right;
      while (minc.left) {
        minc = minc.left;
      }
      if (minc.right) {
        minc.value = minc.right.value;
        minc.right = null;
      } else {
        this.delete(minc.value, c.right, c);
      }
      c.value = minc.value;
    } else {
      let child = c.left || c.right;
      parent.left === c ? parent.left = child : parent.right = child;  
    }
    return 'delete success';
  }
}
```

## **Inorder Traversal**

- **Inorder traversal** visits nodes in the order: **Left → Node → Right**.
- This traversal produces the nodes in **sorted** order in a BST.


```javascript
inorderPrint(c = this.root) {
  if (!c) return; // Early exit if current node is null
  this.inorderPrint(c.left); // Visit left subtree
  console.log(c.value); // Visit the current node
  this.inorderPrint(c.right); // Visit right subtree
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


