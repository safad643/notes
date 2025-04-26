
# MongoDB Regex Examples


## 1. Simple String Match

To match documents where the field `name` contains the string "John" anywhere in the value:

```javascript
db.collection.find({ name: /John/ })
```

This query will return documents where the `name` field has "John" anywhere in its value.

## 2. Case Insensitive Match

To match documents where the field `name` contains the string "john" (case-insensitive):

```javascript
db.collection.find({ name: /john/i })
```

Here, `/john/i` ensures the match is case-insensitive (`i` flag).

## 3. Anchoring with `^` (Start of String)

To match documents where the `name` field starts with "John":

```javascript
db.collection.find({ name: /^John/ })
```

This will match any value in the `name` field that begins with "John".

## 4. Anchoring with `$` (End of String)

To match documents where the `name` field ends with "Doe":

```javascript
db.collection.find({ name: /Doe$/ })
```

This query will return documents where the `name` field ends with "Doe".

## 5. Match Specific Characters (Character Classes)

To match documents where the `phone` field contains a valid US phone number (e.g., `(123) 456-7890`):

```javascript
db.collection.find({ phone: /\(\d{3}\) \d{3}-\d{4}/ })
```

This regex matches a pattern of three digits in parentheses, followed by a space, three digits, a hyphen, and four digits.

## 6. Match Any Character (`.`)

To match documents where the `username` field has any character after "user":

```javascript
db.collection.find({ username: /^user./ })
```

This query will return documents where the `username` field starts with "user" followed by any single character.

## 7. Match Multiple Occurrences (`+` and `{n,m}`)

To match documents where the `email` field contains one or more "a" characters:

```javascript
db.collection.find({ email: /a+/ })
```

The `+` matches one or more occurrences of the preceding character.

To match documents where the `email` field has between 5 and 10 characters:

```javascript
db.collection.find({ email: /^.{5,10}$/ })
```

This query will return documents where the `email` field is between 5 and 10 characters in length.

## 8. Using `|` (OR Condition)

To match documents where the `status` field is either "active" or "inactive":

```javascript
db.collection.find({ status: /active|inactive/ })
```

This query will match documents where the `status` field is either "active" or "inactive".

## 9. Matching with Word Boundaries (`\b`)

To match documents where the `description` field contains the word "hello" as a whole word:

```javascript
db.collection.find({ description: /\bhello\b/ })
```

The `\b` represents a word boundary, so "hello" will only be matched as a standalone word, not part of another word.

## 10. Exclude Documents with a Regex Match

To find documents where the `name` does not start with "John":

```javascript
db.collection.find({ name: { $not: /^John/ } })
```

This will return all documents where the `name` field does not start with "John".
