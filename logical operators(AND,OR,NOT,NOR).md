
# MongoDB Logical Operators Examples

## 🛢️ Sample Collection: `users`

```json
[
  { "_id": 1, "name": "Alice", "age": 25, "city": "New York", "verified": true },
  { "_id": 2, "name": "Bob", "age": 17, "city": "Los Angeles", "verified": false },
  { "_id": 3, "name": "Charlie", "age": 30, "city": "Chicago", "verified": true },
  { "_id": 4, "name": "David", "age": 22, "city": "New York", "verified": false }
]
```

---

## 1. `$and` Example

**Query:**

```javascript
db.users.find({
  $and: [
    { age: { $gte: 18 } },
    { verified: true }
  ]
})
```

**Meaning:**  
Find users who are **18 or older AND verified**.

**Output:**

```json
[
  { "_id": 1, "name": "Alice", "age": 25, "city": "New York", "verified": true },
  { "_id": 3, "name": "Charlie", "age": 30, "city": "Chicago", "verified": true }
]
```

---

## 2. `$or` Example

**Query:**

```javascript
db.users.find({
  $or: [
    { city: "New York" },
    { age: { $lt: 18 } }
  ]
})
```

**Meaning:**  
Find users who live in **New York OR are younger than 18**.

**Output:**

```json
[
  { "_id": 1, "name": "Alice", "age": 25, "city": "New York", "verified": true },
  { "_id": 2, "name": "Bob", "age": 17, "city": "Los Angeles", "verified": false },
  { "_id": 4, "name": "David", "age": 22, "city": "New York", "verified": false }
]
```

---

## 3. `$nor` Example

**Query:**

```javascript
db.users.find({
  $nor: [
    { city: "New York" },
    { verified: true }
  ]
})
```

**Meaning:**  
Find users who are **NOT living in New York AND NOT verified**.

**Output:**

```json
[
  { "_id": 2, "name": "Bob", "age": 17, "city": "Los Angeles", "verified": false }
]
```

---

## 4. `$not` Example

**Query:**

```javascript
db.users.find({
  age: { $not: { $gt: 25 } }
})
```

**Meaning:**  
Find users where **age is NOT greater than 25** (so age <= 25).

**Output:**

```json
[
  { "_id": 1, "name": "Alice", "age": 25, "city": "New York", "verified": true },
  { "_id": 2, "name": "Bob", "age": 17, "city": "Los Angeles", "verified": false },
  { "_id": 4, "name": "David", "age": 22, "city": "New York", "verified": false }
]
```

---

# ✅ Summary

|Operator|Description|Example|
|:--|:--|:--|
|`$and`|All conditions must match|Both `age >= 18` and `verified == true`|
|`$or`|At least one condition must match|`city == "New York"` or `age < 18`|
|`$nor`|None of the conditions must match|Neither `city == "New York"` nor `verified == true`|
|`$not`|Negates a single condition|Age **not** greater than 25|

---

