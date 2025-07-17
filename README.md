# MongoDB - Notes

`` MongoD -> It is the host process for the Database. `` <br/>
`` Mongo -> It is a command line shell that connects to specifics instance of MongoD. ``

-  SQL TERMS &emsp; MongoDB TERMS/CONCEPT <br/>
Database  &emsp;       -> &emsp; Database <br/>
Tables    &emsp;       -> &emsp; Collections <br/>
Rows      &emsp;       -> &emsp; Documents(BSON) <br/>
Columns   &emsp;       -> &emsp; Fields <br/>

## What is BSON in MongoDB?

BSON stands for "Binary JSON" and is the data format MongoDB uses to store and transfer data. Think of it as JSON's more powerful cousin - it includes all the features of JSON but adds some extra capabilities that make it perfect for databases.

When you work with MongoDB, even though you write your data in JSON-like format, MongoDB converts it to BSON behind the scenes for efficient storage and quick access.

## Key Characteristics of BSON

1. **Binary Format**: BSON is stored in binary (1s and 0s) which computers process much faster than text-based JSON.

2. **Lightweight**: Designed to be space-efficient while traveling over the network.

3. **Traversable**: BSON documents are easy to scan through quickly, which helps with query performance.

4. **Rich Data Types**: Supports more data types than JSON, including:
   - Date (JSON can't store dates natively)
   - Binary data (like images or files)
   - Special MongoDB types (like ObjectId)

5. **Efficient Encoding**: Uses a special system that makes encoding and decoding very fast.

## Top 5 Differences Between BSON and JSON

| Feature        | JSON                          | BSON                          |
|---------------|-----------------------------|-----------------------------|
| **Format**     | Text-based (human-readable)  | Binary (computer-optimized) |
| **Data Types** | Basic types only             | Extended types (Date, Binary, etc.) |
| **Size**       | Larger (verbose format)      | More compact                |
| **Speed**      | Slower to parse              | Faster to parse             |
| **Usage**      | General data interchange     | Optimized for databases     |

## Simple Example about JSON and BSON:

**JSON:**
```json
{
  "name": "Alice",
  "age": 30,
  "joined": "2023-01-15"
}
```

**BSON equivalent (conceptual - you'd actually see binary):**
```bson
{
  "name": "Alice" (as string),
  "age": 30 (as 32-bit integer),
  "joined": ISODate("2023-01-15") (as special date type)
}
```

``As a beginner, you don't need to worry much about BSON - MongoDB handles the conversion automatically when you insert or retrieve data!``

## MongoDB Commands : <br/> 

1. Database Commands In MySQL -> <br/>
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

2. Collection Commands In MongoDB -> <br/>
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
       ```
       db.comments.remove({name: 'Harry'})
       ```

    - Less than / Greater than / Less than or Eq / Greater than or Eq examples in below :
        ```
        db.comments.find({member_since: {$lt: 90}})
        ```
        ```
        db.comments.find({member_since: {$lte: 90}})
        ```
        ```
        db.comments.find({member_since: {$gt: 90}})
        ```
        ```
        db.comments.find({member_since: {$gte: 90}})
        ```


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
