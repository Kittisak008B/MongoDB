## comparison operators
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/4aea0000-35be-449a-8461-d4681b6622a8)
#### find every document that name field not equal Pig
```
test_db001> db.people_001.find({name:{$ne:"Pig"}})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/305b2c84-3a82-4681-a1a4-3e16163253e3)

#### find every doc that age field is less than 35
```
test_db001> db.people_001.find({age:{$lt:35}})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/f420e964-ad3e-42f5-9998-1ffa7d2a7f43)
```
Equality:
$eq: Matches values that are equal to a specified value.
$ne: Matches values that are not equal to a specified value.

ex. Find documents where the "name" field is equal to "Sam"
{ name: { $eq: "Sam" } }

Comparison:
$gt: Matches values that are greater than a specified value.
$gte: Matches values that are greater than or equal to a specified value.
$lt: Matches values that are less than a specified value.
$lte: Matches values that are less than or equal to a specified value.

ex: Find documents where the "age" field is greater than 30
{ age: { $gt: 30 } }

Existence:
$exists: Matches documents that have the specified field.

ex: { field: { $exists: true } } matches documents where the field exists.
ex: { field: { $exists: false } } matches documents where the field does not exist.
ex: Find documents where the "comments" field exists and is of type array:
{ comments: { $exists: true, $type: "array" } }


Type:
$type: Matches documents where the value of a field is of a specified type.

ex: { field: { $type: "string" } } matches documents where the field is of type string.

Regex:
$regex: Provides regular expression matching.

ex: { field: { $regex: /pattern/ } } matches documents where the field matches the specified pattern.
ex: Find documents where the "username" field starts with "user":
{ username: { $regex: /^user/ } }

Array:
$in: Matches any of the values specified in an array.
$nin: Matches none of the values specified in an array.

ex. Find documents where the "tags" field is an array containing "mongodb" or "database"
{ tags: { $in: ["mongodb", "database"] } }
ex. Find documents where the "tags" field contains both "mongodb" and "db":
{ tags: { $all: ["mongodb", "db"] } }
ex. Find documents where the "colors" field does not contain "red":
{ colors: { $nin: ["red"] } }

```
## logical operators
#### find doc where age>=35 and jail=true
```
test_db001> db.people_001.find({$and:[{age:{$gte:35}},{jail:true}]})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/5468b333-d141-4e57-98e3-b1dfe327ab6f)
```
{ $and: [ { condition1 }, { condition2 }, ... ] }

{ $or: [ { condition1 }, { condition2 }, ... ] }

{ $nor: [ { condition1 }, { condition2 }, ... ] }
Note: nor: returns when all conditions are false.

{ field: { $not: { $gt: 5 } } }

```
#### find doc where age not less than 65
```
test_db001> db.people_001.find({age:{$not:{$lt:65}}})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/089140a9-e855-4510-b929-845c3573da2f)

```
#Explain a Query
# sql
EXPLAIN SELECT city, state, pop 
            FROM zips 
WHERE state = 'NY' AND pop BETWEEN 100 AND 400 
ORDER BY pop DESC 
LIMIT 10;

# MongoDB
db.zips.explain().find(
    { state: "NY", pop: { $gte: 100, $lte: 400 }}, 
    {_id: 0, state: 1, city: 1, pop: 1}
    ).sort({pop: -1})
    .limit(10)
```

```
#SQL JOINs In MongoDB
SELECT t.*, a.account_id, a.account_holder
FROM transfers t
INNER JOIN account_holder a
ON t.transfer_id = a.transfers_complete

This SQL JOIN query does the following:
            -Joins the records of the transfers table with the records of the accounts table.
            -Uses the transfers_complete field from the accounts table and the transfer_id field from the transfers table.
            -Projects the account_holder and account_id fields from the accounts table into the transfers table.

in MongoDB, we use the $lookup operator from the aggregation framework. Inside the $lookup stage, we define the following:
            -accounts is the collection to join.
            -transfer_id as localField is the field to use in the equality match from the input documents.
            -transfers_complete as foreignField is the field to use in the equality match from the transfers collection.
            -account_id and account_holder are the projected fields in the resulting documents while suppressing the _id field.
            -account_holder is the name of the new array field to add to the input documents.
db.transfers.aggregate( [
    {
      $lookup:
        {
          from: "accounts",
          localField: "transfer_id",
          foreignField: "transfers_complete",
          pipeline: [
 
             { $project: { _id: 0, account_id: 1, account_holder: 1 } }
          ],
          as: "account_holder"
      }
  }] )
```







