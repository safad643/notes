
---

## MongoDB Array-based Operators

### Sample Data

```json
db.users.insertMany([
    {
        "_id": 1,
        "name": "Alice",
        "tags": ["mongodb", "database", "nosql"],
        "scores": [95, 80, 75],
        "friends": [
            { "name": "Bob", "age": 25 },
            { "name": "Charlie", "age": 30 }
        ]
    },
    {
        "_id": 2,
        "name": "Bob",
        "tags": ["python", "data science"],
        "scores": [90, 85, 92],
        "friends": [
            { "name": "Alice", "age": 25 },
            { "name": "David", "age": 28 }
        ]
    },
    {
        "_id": 3,
        "name": "Charlie",
        "tags": ["javascript", "react"],
        "scores": [88, 77, 94],
        "friends": [
            { "name": "Alice", "age": 30 },
            { "name": "Bob", "age": 28 }
        ]
    }
])
```

---

### 1. **`$all`**

The `$all` operator matches arrays that contain all the specified elements.

```javascript
db.users.find({
    "tags": { $all: ["mongodb", "database"] }
})
```

**Output**:

```json
[
    { "_id": 1, "name": "Alice", "tags": ["mongodb", "database", "nosql"], ... }
]
```

---

### 2. **`$elemMatch`**

The `$elemMatch` operator matches array elements that meet the query condition.

```javascript
db.users.find({
    "friends": { $elemMatch: { "age": { $gt: 28 } } }
})
```

**Output**:

```json
[
    { "_id": 2, "name": "Bob", "friends": [{ "name": "Alice", "age": 25 }, { "name": "David", "age": 28 }] },
    { "_id": 3, "name": "Charlie", "friends": [{ "name": "Alice", "age": 30 }, { "name": "Bob", "age": 28 }] }
]
```

---

### 3. **`$size`**

The `$size` operator matches arrays with a specific number of elements.

```javascript
db.users.find({
    "tags": { $size: 3 }
})
```

**Output**:

```json
[
    { "_id": 1, "name": "Alice", "tags": ["mongodb", "database", "nosql"], ... },
    { "_id": 2, "name": "Bob", "tags": ["python", "data science"], ... }
]
```

---

### 4. **`$push`**

The `$push` operator adds an element to an array.

```javascript
db.users.updateOne(
    { "_id": 1 },
    { $push: { "tags": "developer" } }
)
```

**Output**:

```json
{
    "_id": 1,
    "name": "Alice",
    "tags": ["mongodb", "database", "nosql", "developer"],
    ...
}
```

---

### 5. **`$addToSet`**

The `$addToSet` operator adds an element to an array only if it doesn't already exist.

```javascript
db.users.updateOne(
    { "_id": 1 },
    { $addToSet: { "tags": "mongodb" } }
)
```

**Output**:

```json
{
    "_id": 1,
    "name": "Alice",
    "tags": ["mongodb", "database", "nosql", "developer"], 
    ...
}
```

---

### 6. **`$pop`**

The `$pop` operator removes the first or last element of an array.

```javascript
db.users.updateOne(
    { "_id": 1 },
    { $pop: { "scores": 1 } }
)
```

**Output**:

```json
{
    "_id": 1,
    "name": "Alice",
    "tags": ["mongodb", "database", "nosql", "developer"],
    "scores": [95, 80] 
}
```

---

### 7. **`$pull`**

The `$pull` operator removes all occurrences of a value from an array.

```javascript
db.users.updateOne(
    { "_id": 1 },
    { $pull: { "tags": "nosql" } }
)
```

**Output**:

```json
{
    "_id": 1,
    "name": "Alice",
    "tags": ["mongodb", "database", "developer"],
    ...
}
```

---

### 8. **`$pullAll`**

The `$pullAll` operator removes all occurrences of each value in a list from an array.

```javascript
db.users.updateOne(
    { "_id": 1 },
    { $pullAll: { "tags": ["mongodb", "database"] } }
)
```

**Output**:

```json
{
    "_id": 1,
    "name": "Alice",
    "tags": ["developer"],
    ...
}
```

---

### 9. **`$unset`**

The `$unset` operator removes the array field entirely.

```javascript
db.users.updateOne(
    { "_id": 1 },
    { $unset: { "tags": "" } }
)
```

**Output**:

```json
{
    "_id": 1,
    "name": "Alice",
    "scores": [95, 80, 75],
    "friends": [ ... ]
}
```

---

### 10. **`$arrayElemAt`**

The `$arrayElemAt` operator returns the element at the specified index in an array.

```javascript
db.users.aggregate([
    { $project: { firstTag: { $arrayElemAt: ["$tags", 0] } } }
])
```

**Output**:

```json
[
    { "_id": 1, "firstTag": "mongodb" },
    { "_id": 2, "firstTag": "python" },
    { "_id": 3, "firstTag": "javascript" }
]
```

---

### 11. **`$arrayToObject`**

The `$arrayToObject` operator converts an array of key-value pairs into an object.

```javascript
db.users.aggregate([
    { $project: { tagsObject: { $arrayToObject: [{ "k": "$tags", "v": "$scores" }] } } }
])
```

**Output**:

```json
[
    { "_id": 1, "tagsObject": { "mongodb": [95, 80, 75], "database": [95, 80, 75], "nosql": [95, 80, 75] } },
    { "_id": 2, "tagsObject": { "python": [90, 85, 92], "data science": [90, 85, 92] } },
    { "_id": 3, "tagsObject": { "javascript": [88, 77, 94], "react": [88, 77, 94] } }
]
```

---

### 12. **`$concatArrays`**

The `$concatArrays` operator combines multiple arrays into one.

```javascript
db.users.aggregate([
    { $project: { combinedTags: { $concatArrays: ["$tags", ["frontend", "backend"]] } } }
])
```

**Output**:

```json
[
    { "_id": 1, "combinedTags": ["mongodb", "database", "nosql", "frontend", "backend"] },
    { "_id": 2, "combinedTags": ["python", "data science", "frontend", "backend"] },
    { "_id": 3, "combinedTags": ["javascript", "react", "frontend", "backend"] }
]
```

---

### 13. **`$filter`**

The `$filter` operator filters the elements of an array based on a condition.

```javascript
db.users.aggregate([
    { $project: { highScores: { $filter: { input: "$scores", as: "score", cond: { $gt: ["$$score", 80] } } } } }
])
```

**Output**:

```json
[
    { "_id": 1, "highScores": [95] },
    { "_id": 2, "highScores": [90, 85, 92] },
    { "_id": 3, "highScores": [88, 94] }
]
```

---

### 14. **`$in`**

The `$in` operator checks if an element exists within an array.

```javascript
db.users.find({
    "tags": { $in: ["mongodb", "python"] }
})
```

**Output**:

```json
[
    { "_id": 1, "name": "Alice", "tags": ["mongodb", "database", "nosql"], ... },
    { "_id": 2, "name": "Bob", "tags": ["python", "data science"], ... }
]
```

---

### 15. **`$map`**

The `$map` operator applies an expression to each element in an array and returns a new array.

```javascript
db.users.aggregate([
    { $project: { increasedScores: { $map: { input: "$scores", as: "score", in: { $add: ["$$score", 5] } } } } }
])
```

**Output**:

```json
[
    { "_id": 1, "increasedScores": [100, 85, 80] },
    { "_id": 2, "increasedScores": [95, 90, 97] },
    { "_id": 3, "increasedScores": [93, 82, 99] }
]
```

---

### 16. **`$reduce`**

The `$reduce` operator performs a rolling computation on an array and returns a single value.

```javascript
db.users.aggregate([
    { $project: { totalScore: { $reduce: { input: "$scores", initialValue: 0, in: { $add: ["$$value", "$$this"] } } } } }
])
```

**Output**:

```json
[
    { "_id": 1, "totalScore": 250 },
    { "_id": 2, "totalScore": 267 },
    { "_id": 3, "totalScore": 259 }
]
```

---

### 17. **`$size`** (Aggregation)

The `$size` operator returns the size of an array.

```javascript
db.users.aggregate([
    { $project: { numberOfTags: { $size: "$tags" } } }
])
```

**Output**:

```json
[
    { "_id": 1, "numberOfTags": 3 },
    { "_id": 2, "numberOfTags": 2 },
    { "_id": 3, "numberOfTags": 2 }
]
```

---

### 18. **`$exists`**

The `$exists` operator checks if an array field exists in a document.

```javascript
db.users.find({
    "friends": { $exists: true }
})
```

**Output**:

```json
[
    { "_id": 1, "name": "Alice", "friends": [...] },
    { "_id": 2, "name": "Bob", "friends": [...] },
    { "_id": 3, "name": "Charlie", "friends": [...] }
]
```

---

### 19. **`$type`**

The `$type` operator checks the type of array field (e.g., if it’s an array).

```javascript
db.users.find({
    "tags": { $type: "array" }
})
```

**Output**:

```json
[
    { "_id": 1, "name": "Alice", "tags": ["mongodb", "database", "nosql"] },
    { "_id": 2, "name": "Bob", "tags": ["python", "data science"] },
    { "_id": 3, "name": "Charlie", "tags": ["javascript", "react"] }
]
```

---

This concludes the examples and expected outputs for MongoDB's **19 array-based operators**! Let me know if you need any further details or explanations!