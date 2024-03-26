# mongodb Tutorial
#### MongoDB Shell (mongosh)

```
Please enter a MongoDB connection string (Default: mongodb://localhost/): mongosh
```
#### clear screen
```
mongosh> cls
```
#### exit
```
mongosh> exit
```

## databases
#### show all databases
```
mongosh> show dbs
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/cc079d19-c36f-492c-94e9-187b21467c3d)

#### use database
```
mongosh> use admin
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/4f6bb777-53d0-4055-8bd5-43cee435f6f3)
#### use database that doesn't exist --> create a database
```
admin> use test_db001
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/a2ac3692-b9b7-4095-a906-8bdcf653a782)
#### add a collection to new database
```
test_db001> db.createCollection("people_test001")
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/02d82b59-d7a9-4f75-9b9d-a9529cb6071b)
```
test_db001> show dbs
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/bc98457e-28a4-4650-a679-78fd93ea272f)
#### drop database
```
test_db001> db.dropDatabase()
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/31e81c54-87b2-4d40-a178-ed09c66fcc8a)

## insert
#### insert data document into collection
```
test_db001> db.people_001.insertOne({name:"Sam" , age:30 , weight:100})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/16b5349a-3e0a-4c1a-8307-fb996e697a48)
#### return document within a collection
```
test_db001> db.people_001.find()
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/b39c7e23-a16c-41c6-9c35-8b99f2a45f72)
#### insertMany
```
test_db001> db.people_001.insertMany([{name:"Nancy" , age:90 , weight:70},{name:"Chicken" , age:40 , weight:60},{name:"Pig" , age:60 , weight:40}])
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/b0a0fadc-a130-495b-9b28-49a40dacd88b)
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/554e71c0-d579-4943-a2d2-35c76a64c774)

## data types
```
db.people_001.insertOne({name:"Sam Bmf" , age:33 , weight:100.88 , jail:true,registerDate:new Date(),exitDate: null,food:["pig","chicken"],address:{street:"123 pig St.",city:"bahamas",zip:1234}})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/f5ab8fdc-e60a-41dc-90ab-8f503bf9f001)
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/a08ab520-16cf-4ca5-8989-74a048543f49)

## sorting
```
test_db001> db.people_001.find().sort({name:1})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/9703a015-fa2e-45c5-998e-419ab6075ab9)
```
test_db001> db.people_001.find().sort({age:1})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/5e3d6c68-36db-427c-8eb4-a770f65dda05)
#### limit
```
test_db001> db.people_001.find().sort({age:-1}).limit(1)
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/461170fb-76f1-44d5-b025-1ecf7e6ae50d)

## query
```
test_db001> db.people_001.find({name:"Pig"})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/3fd111e6-57fb-4916-ba91-467ef1b9418b)
#### return every document only name
```
test_db001> db.people_001.find({},{name:true})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/2d26d6e1-68e7-4941-9eff-3054c6b26c75)
```
test_db001> db.people_001.find({},{_id:false,name:true})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/8927eca5-582b-429e-8d96-971eee8a91f2)
#### return every document name and age
```
test_db001> db.people_001.find({},{_id:false,name:true, age:true})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/698acc94-6aa8-48a1-8e4e-2d6b6283195d)
## update
#### .updateOne(filter,update)
```
test_db001> db.people_001.updateOne({name:"Sam"},{$set:{jail:true}})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/170a5c5a-8887-474d-af44-ea82a6fdd4aa)
```
test_db001> db.people_001.updateOne({_id: ObjectId('6602f075a4d04c0b66d14a0e')},{$set:{exitDate:null}})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/bd4d7a24-431d-4787-905e-69ff400974b6)
#### use unset operator --> remove a field
```
test_db001> db.people_001.updateOne({_id: ObjectId('6602f075a4d04c0b66d14a0e')},{$unset:{exitDate:""}})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/3dd0ef28-b0fb-4316-a150-54f7bf3de225)
#### updateMany
```
test_db001> db.people_001.updateMany({} , {$set:{jail:true}})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/6714410a-15a3-45d6-81d2-777c671abeed)
#### everybody that doesnt have exitDate set to null
```
test_db001> db.people_001.updateMany({exitDate:{$exists:false}} , {$set:{exitDate:null}})
```
![image](https://github.com/Kittisak008B/mongodb/assets/157298910/2ef32f47-0bd9-482b-a44f-5352edb239e4)
































