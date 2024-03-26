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







