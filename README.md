# MongoDB-Notes

MongoD -> It is the host process for the Database <br/>
Mongo -> It is a command line shell that connects to specifics instance of MongoD 

SQL TERMS &emsp; MongoDB TERMS/CONCEPT <br/>
Database         ->  Database <br/>
Tables           ->  Collections <br/>
Rows             ->  Documents(BSON) <br/>
Columns          ->  Fields <br/>

MongoDB commands  <br/> 

1. Database commands <br/>
View all databases <br/> 
show dbs <br/>

Create a new or switch databases <br/>
use dbName <br/>

View current Database <br/>
db <br/>

Delete Database <br/>
db.dropDatabase() <br/>

2. Collection Commands <br/>
Show Collections <br/>
show collections <br/>

Create a collection named 'comments' <br/>
db.createCollection('comments') <br/>

Drop a collection named 'comments' <br/>
db.comments.drop() <br/>

3. Row(Document) Commands <br/>
Show all Rows in a Collection <br/>
db.comments.find() <br/>

Show all Rows in a Collection (Prettified) <br/>
db.comments.find().pretty() <br/>

Find the first row matching the object <br/>
db.comments.findOne({name: 'Subham'}) <br/>

Insert One Row <br/>
db.comments.insert({ <br/>
    "name": 'Subham', <br/>
    'lang': 'JavaScript', <br/>
    'member_since': 5 <br/>
 }) <br/>

Insert many Rows <br/>
db.comments.insertMany([{ <br/>
    'name': 'Harry', <br/>
    'lang': 'JavaScript', <br/>
    'member_since': 5 <br/>
    },  <br/>
    {'name': 'Rohan', <br/>
    'lang': 'Python', <br/>
    'member_since': 3 <br/>
    }, <br/>
    {'name': 'Lovish', <br/>
    'lang': 'Java', <br/>
    'member_since': 4 <br/>
}]) <br/>

Search in a MongoDb Database <br/>
db.comments.find({lang:'Python'}) <br/>

Limit the number of rows in output <br/>
db.comments.find().limit(2) <br/>

Count the number of rows in the output <br/>
db.comments.find().count() <br/>

Update a row
db.comments.update({name: 'Shubham'}, <br/>
{'name': 'Harry', <br/>
    'lang': 'JavaScript', <br/>
    'member_since': 51 <br/>
}, {upsert: true}) <br/>

Mongodb Increment Operator <br/>
db.comments.update({name: 'Rohan'}, <br/>
{$inc:{ <br/>
    member_since: 2 <br/>
}}) <br/>

Mongodb Rename Operator <br/>
db.comments.update({name: 'Rohan'}, <br/>
{$rename:{ <br/>
    member_since: 'member' <br/>
}}) <br/>

Delete Row <br/>
db.comments.remove({name: 'Harry'}) <br/>

Less than/Greater than/ Less than or Eq/Greater than or Eq <br/>
db.comments.find({member_since: {$lt: 90}}) <br/>
db.comments.find({member_since: {$lte: 90}}) <br/>
db.comments.find({member_since: {$gt: 90}}) <br/>
db.comments.find({member_since: {$gte: 90}}) <br/>
