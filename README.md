# MongoDB - Notes

`` MongoD -> It is the host process for the Database. `` <br/>
`` Mongo -> It is a command line shell that connects to specifics instance of MongoD. ``

-  SQL TERMS &emsp; MongoDB TERMS/CONCEPT <br/>
Database  &emsp;       -> &emsp; Database <br/>
Tables    &emsp;       -> &emsp; Collections <br/>
Rows      &emsp;       -> &emsp; Documents(BSON) <br/>
Columns   &emsp;       -> &emsp; Fields <br/>

## MongoDB Commands : <br/> 

1. Database commands -> <br/>
    - View all databases :
        ```
        show dbs 
        ```

    - Create a new or switch databases :
      ```
      use dbName
      ```

    - View current Database :
      ```
      db
      ```

    - Delete Database : 
        ```
        db.dropDatabase()
        ```

2. Collection Commands -> <br/>
    - Show Collections : 
        ```
        show collections
        ```

    - Create a collection named 'comments' : 
        ```
        db.createCollection('comments')
        ```

    - Drop a collection named 'comments' :
        ```
        db.comments.drop()
        ```

3. Row(Document) Commands -> <br/>
    - Show all Rows in a Collection : 
        ```
        db.comments.find()
        ```

    - Show all Rows in a Collection (Prettified) : 
        ```
        db.comments.find().pretty() 
        ```

    - Find the first row matching the object : 
        ```
        db.comments.findOne({name: 'Subham'})
        ```

    - Insert One Row : <br/>
        ```
        db.comments.insert({ 
            "name": 'Subham',
            'lang': 'JavaScript',
            'member_since': 5
         })
        ```

    - Insert many Rows : <br/>
        ```
        db.comments.insertMany([{ 
            'name': 'Harry', 
            'lang': 'JavaScript', 
            'member_since': 5
            },  <br/>
            {'name': 'Rohan',
            'lang': 'Python', 
            'member_since': 3 
            }, <br/>
            {'name': 'Lovish', 
            'lang': 'Java', 
            'member_since': 4 
        }])
        ```

    - Search in a MongoDb Database : 
        ```
        db.comments.find({lang:'Python'}) 
        ```

    - Limit the number of rows in output : 
        ```
        db.comments.find().limit(2)
        ```

    - Count the number of rows in the output :
      ```
      db.comments.find().count() <br/>
      ```

    - Update a row :
        ```
        db.comments.update({name: 'Shubham'},
        {'name': 'Harry', 
            'lang': 'JavaScript', 
            'member_since': 51 
        }, {upsert: true}) 
        ```

    - Mongodb Increment Operator : <br/>
       ```
       db.comments.update({name: 'Rohan'},
        {$inc:{ 
            member_since: 2 
        }})
       ```

    - Mongodb Rename Operator : <br/>
        ```
        db.comments.update({name: 'Rohan'},
        {$rename:{ 
            member_since: 'member' 
        }})
        ```

    - Delete Row : <br/>
        ``` db.comments.remove({name: 'Harry'}) ``` <br/>

    - Less than/Greater than/ Less than or Eq/Greater than or Eq : <br/>
        ``` db.comments.find({member_since: {$lt: 90}}) ``` <br/>
        ``` db.comments.find({member_since: {$lte: 90}}) ``` <br/>
        ``` db.comments.find({member_since: {$gt: 90}}) ``` <br/>
        ``` db.comments.find({member_since: {$gte: 90}}) ``` <br/>


## MongoDB Aggregation:
  `Aggregation in MongoDB is a way to process a large number of documents in a collection by passing them through different stages called a pipeline. The stages can filter, sort, group, reshape, and modify documents. The aggregation pipeline runs in the MongoDB server and can be optimized before running.` <br/> <br/>

  `Aggregation allows for the transforming of data and results in a more powerful fashion than from using the find() command. Through the use of multiple stages and expressions, you are able to build a "pipeline" of operations on your data to perform analytic operations.` <br/><br/>

  - The aggregation pipeline consists of the following stages : <br/>
      Input, $match, $group, $sort, $skip, $limit, and $unwind. <br/><br/>

`Each stage uses operators to complete transformation. The order of the stages matters, and there are optimizations that can help your pipeline perform better.`


### Example of aggregation : <br/>
```
db.orders.aggregate( [

   // Stage 1: Filter pizza order documents by pizza size
   {
      $match: { size: "medium" }
   },

   // Stage 2: Group remaining documents by pizza name and calculate total quantity
   {
      $group: { _id: "$name", totalQuantity: { $sum: "$quantity" } }
   }

] )
```
