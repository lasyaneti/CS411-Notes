# NoSQL Overview
- Single server database is not enough to sustain the volume, variety, velocity, and veracity of big data
- NoSQL solutions scale across multiple servers

# MongoDB Basics
- Database <- collections <- documents <- keyval pairs

| RDMBS | MONGODB |
| ----- | ------- |
| Table | Collection |
| Row | JSON Document |
| Index | Index |
| Join | Embedding, Linking |
| Partition | Shard |
| Partition Key | Shart Key |

`show dbs` reveals all databases

`use <demo_db>`  

`show collections` show collections within demo_dbs

### CRUD & other commands
- Insert one `db.people.insert(mydoc)`
- Delete one `db.people.deleteOne({'key':'value'})`
- Delete many `db.people.deleteMany({'key':'value'})`
- Delete all in collection `db.people.deleteMany()`
- Remove collections (fast) `db.people.drop()`
- Update `db.people.updateMany({birthyear:1924}, {$set:{birthyear:2002}})`
- Find `db.people.find({}, {'key':'value'})`
- Find within range `db.people.find({birthyear}: {$gte: 2000: $lte: 2002})`
- Find not equal to `db.people.find({birthyear}: {$ne: 1999})`
- OR `$or: [...]`, IN `$in: [...]`
- Find embedded documents `db.people.find({'name.first':'John'})`