

---

# 📅 MongoDB Date Operations Cheatsheet

## 1. Convert Date to String

```javascript
db.collection.aggregate([
  {
    $addFields: {
      dateString: { $dateToString: { format: "%Y-%m-%d", date: "$yourDateField" } }
    }
  }
])
```

**Use case:**  
➡️ You want to **format a date** nicely for reports, export, or matching with external systems (like "2025-04-26").

  

```json
{
  "_id": 1,
  "yourDateField": ISODate("2025-04-26T00:00:00Z")
}
```

After running the aggregation, the result would look like:

```json
{
  "_id": 1,
  "yourDateField": ISODate("2025-04-26T00:00:00Z"),
  "formattedDate": "2025-04-26", // Formatted date (string)
  "unformattedDate": ISODate("2025-04-26T00:00:00Z") // Original date object (unformatted)
}
```



---

## 2. Extract Day of Month

```javascript
db.collection.aggregate([
  {
    $addFields: {
      dayOfMonth: { $dayOfMonth: "$yourDateField" }
    }
  }
])
```

**Use case:**  
➡️ You want to **filter** or **group** documents based on the **day part** of the date (e.g., "give me all events that happened on the 15th of any month").

---

## 3. Other Date Parts (Quick Reference)

|Operator|Purpose|
|:--|:--|
|`$year`|Extract year|
|`$month`|Extract month|
|`$dayOfMonth`|Extract day (1-31)|
|`$dayOfWeek`|Extract day (1 = Sunday)|
|`$hour`|Extract hour (0-23)|
|`$minute`|Extract minute|

Example:

```javascript
db.collection.aggregate([
  {
    $addFields: {
      month: { $month: "$yourDateField" },
      year: { $year: "$yourDateField" },
      weekday: { $dayOfWeek: "$yourDateField" }
    }
  }
])
```

---

# ⚡ Tip

- Use `$dateToString` if you want **custom formats** (like "DD-MM-YYYY").
    
- Use `$dayOfMonth`, `$month`, `$year` if you want to **filter, group, or sort**.
  
  
  
  
  
  
  
  
  
  
  


