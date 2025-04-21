## 🌳 **AVL Tree (Adelson-Velsky and Landis Tree)**

### **What is an AVL Tree?**

- An **AVL Tree** is a **self-balancing binary search tree (BST)**, where the height difference between the left and right subtrees of any node (called the **balance factor**) is no more than 1.
- The goal of an AVL tree is to keep the tree balanced to maintain log(n) time complexity for insertions, deletions, and lookups.

## ✅ AVL Tree Insertion (with Rotations) – Explained

We insert a node into an **AVL Tree** just like a **Binary Search Tree (BST)**:

- If value is **less**, go **left**
- If **greater**, go **right**
- Insert at the **leaf**

---

### 🧠 Backtracking (Coming Up the Recursion Path):

As we return up the recursion:

1. Update height:  
   ```  
   height = 1 + max(height(left), height(right))  
   ```

2. Calculate balance factor:  
   ```  
   balance = height(left) - height(right)  
   ```

3. If balance is:
   - **Between -1 and 1** → No rotation needed
   - **Less than -1 or more than 1** → Rotation needed

---

## 🔄 Rotation Cases in AVL Tree (with Examples)

---

### **1. Left-Left (LL) Case**
- New node inserted into **left of left child**
- Balance becomes **> 1**
- ✅ **Fix**: Right Rotation

**Before Insertion of 10:**
```
        30
       /
     20
    /
  10
```

**After Right Rotation at 30:**
```
      20
     /  \
   10    30
```

**How to Identify this Rotation:**
- **Balance factor > 1** and **insertedValue < current.left.value**  
- This means the new node was inserted into the **left subtree of the left child** → **LL Case** → Perform **Right Rotation**

---

### **2. Right-Right (RR) Case**
- New node inserted into **right of right child**
- Balance becomes **< -1**
- ✅ **Fix**: Left Rotation

**Before Insertion of 40:**
```
    20
      \
      30
        \
        40
```

**After Left Rotation at 20:**
```
      30
     /  \
   20    40
```

**How to Identify this Rotation:**
- **Balance factor < -1** and **insertedValue > current.right.value**  
- This means the new node was inserted into the **right subtree of the right child** → **RR Case** → Perform **Left Rotation**

---

### **3. Left-Right (LR) Case**
- New node inserted into **right of left child**
- ✅ **Fix**:
  - Left rotate at left child
  - Then right rotate at current node

**Before Insertion of 25:**
```
      30
     /
   20
     \
     25
```

**Step 1 – Left Rotate at 20:**
```
      30
     /
   25
   /
 20
```

**Step 2 – Right Rotate at 30:**
```
     25
    /  \
  20    30
```

**How to Identify this Rotation:**
- **Balance factor > 1** and **insertedValue > current.left.value**  
- This means the new node was inserted into the **right subtree of the left child** → **LR Case** → Perform **Left Rotation at left child**, then **Right Rotation at current node**

---

### **4. Right-Left (RL) Case**
- New node inserted into **left of right child**
- ✅ **Fix**:
  - Right rotate at right child
  - Then left rotate at current node

**Before Insertion of 35:**
```
    30
      \
      40
     /
   35
```

**Step 1 – Right Rotate at 40:**
```
    30
      \
      35
        \
        40
```

**Step 2 – Left Rotate at 30:**
```
     35
    /  \
  30    40
```

**How to Identify this Rotation:**
- **Balance factor < -1** and **insertedValue < current.right.value**  
- This means the new node was inserted into the **left subtree of the right child** → **RL Case** → Perform **Right Rotation at right child**, then **Left Rotation at current node**

---





