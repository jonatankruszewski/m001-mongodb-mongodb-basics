# M001

## CHAPTER 01

### WELCOME TO M001

### Lecture: What is the mongoDB Database?

- It is a Database, meaning a structured way to store data.
- It is a NOSQL Database. It is organized, but not in row or columns.
- NOSQL Document database. Data are stored in documents, and documents are stored in collections.

### QUIZ: Why is MongoDB a NoSQL DataBase?

- [x] Because it does not utilize tables, rows and columns to organize data
- [x] Because it uses a structured waty to store and access data

### What is a Document?

- A way to organize and store data as a set of Field-Value pairs
- A collection would contain multiple documents.
- A DB would contain multiple collections.

### Quiz 1: What is the MongoDB Database?

- [x] The MongoDB database is an organized way to store and access data.
- [ ] MongoDB database organizes documents in rows and columns.
- [ ] MongoDB's database uses tables of related data.
- [x] MongoDB is a NoSQL database that uses documents to store data in an organized way.

### Quiz 2: What is a Document?

- [x] Collections are documents that are organized in rows and columns.
- [x] Documents are made up of collections.
- [x] Collections are tables of documents and other collections.
- [x] Collections consist of one or many documents.

### Quiz 3: What is a Document?

- [x] Each field has a value associated with it.
- [x] A field is a unique identifier for a specific datapoint.
- [ ] Values do not have to be attached to fields, and can be stand alone data points.

### Lecture: What is MongoDB Atlas?

- Atlas cloud database is the DAAS
- DB in the cloud
- MongoDb used as core of Atlas for data storage and retrieval.
- Can deploy clusters (groups of servers that sotre your data)
- Clusters: Groups of servers that store your data. This servers are configured as a replica set. A set of a few connected mongodb instances that stores the same data. If anything happens to any of the instances, the data will still be available by the remianing working members of the replica set. Redundancy.
- Atlas creates the clusters for you, simplyfing running and mantaining the DB.
- Atlas costs $$ but there is a free version with some limits.

### Quiz : What is Atlas?

- [x] Atlas has many tools and services within it that are built specifically for the MongoDB Database.
- [ ] MongoDB Database has the same functionality as Atlas, but without the friendly user interface.
- [ ] Atlas is a MongoDB service that can work with any database, but in this course it will be used with MongoDB.
- [x] They both are MongoDB products.

### Lab: Create and Deploy an Atlas Cluster

- Follow the steps to create a new cluster on mongodb Atlas.

### Lecture: Atlas User Interface Overview

- Connect: allows access from certain ips.
- Create a user
- Choose a connection method.
- Visualize the data from the Data Explorer
- Charm and Realm to be discussed afterwards.

### Lecture: Introducing the InBrowser IDE

- Top navigation panel: Access services like Charts and Realm.
- Left navigation panel: Cluster management itself: Security, DB Access, etc.
- Interaction with the cluster: Or with the shell, or with the Data Explorer (click on collections)

### Lab: Connect to your Atlas Cluster

- Create your cluster on Mongodb atlas.
- Add IP: 0.0.0.0
- Add User: m001-student. Password: m001-mongodb-basics
- Create the user
- Click on connect
- Click on connect with the mongo shell
- Grab the link. Should look like:

 `mongo "mongodb+srv://something.something.mongodb.net/myFirstDatabase" --username m001-student`

- Go back to the lab and paste it on the terminal
- Input your password
- Your terminal in the shell should look like something:

 ```MongoDB Enterprise atlas-4phot5-shard-0:PRIMARY>```

- Click on RUN TEST

## CHAPTER 02

### IMPORTING, EXPORTING AND QUERYING DATA

### Lecture: How does MongoDB store data?

- MongoDB uses Documents to store data.
- Documents are visualized as JSON Files.
- JSON: separated by commas, key value pairs, keys stringified. Starts and ends iwith {}. Keys-values are separated by colons. Can contain subdocuments nested.
- Problems: Text-based, space consuming, limit on data types.
- BSON: Binary JSON. Binary representation of JSON format.

| PROP         | JSON                           | BSON                                                                       |
| :----------- | :----------------------------- | :------------------------------------------------------------------------- |
| Encoding     | UTF-8                          | Binary                                                                     |
| Data Support | Strinb, boolean, number, array | String, Boolean, Number (Integer, Long, Float...), Array, Date, Raw Binary |
| Readability  | Human and machine              | Machine Only                                                               |

BSON provides additionaly speed and accesibility.

### Quiz: What is a JSON?

Which of the following documents is correct JSON?

- [ ] {name : "Devi", age: 19, major: "Computer Science"}
- [x] {"name" : "Devi", "age": 19, "major": "Computer Science"}
- [ ] ["name" : "Devi", "age": 19, "major": "Computer Science"]

### Quiz: JSON vs. BSON?

Write BSON or JSON in the numbered blanks in the following sentences to make them true:

- MongoDB stores data in **BSON**, and you can then view it in **JSON**
- **BSON** is faster to parse and lighter to store than **JSON**
- **JSON** supports fewer data types than **BSON**

### Lecture: Importing and Exporting Data

- You can export / import both as BSON or JSON. Choos BSON for speed if you don't need to visulize it. Choose JSON if so.

| PROP   | JSON        | BSON         |
| :----- | :---------- | :----------- |
| IMPORT | mongoimport | mongorestore |
| EXPORT | mongoexport | mongodump    |

Exporting:

- We will need a URI. URI: Uniform resource identifier.
- Usage: mongo*export/dump* --uri:<mongodb_uri>
- Mongodump by default will export to a dump folder. So, to see data, you will need to cd into dump, cd into the db name.
- Mongoexport: you can pass a collection flag (--collection=sales) and a file name (--out:sales.json)

Importing:

- You need also the uri
- You can also use the flag --drop

### Quiz: Import and Export?

Which of the following commands will add a collection that is stored in animals.json to an Atlas cluster?

- [ ] mongoexport
- [x] mongoimport
- [ ] mongorestore
- [ ] mongodump

### Lecture: Data Explorer

- Querying:
- A) From the data explorer. Go to collections. You can create a DB or a collection. A namespace is a concatenation of a DB name and a collection: sample_training.companies.
- B) Through the shell, Compass, or any other connection method.
- Queryes should follow the JSON format.

### Quiz: Data Explorer

Problem:

In the sample_training.trips collection a person with birth year 1961 took a trip that started at "Howard St & Centre St". What was the end station name for that trip?

Copy and paste your answer from the Atlas UI to the response text box. The station name should be in a single set double quotes, exactly as it is in the Data Explorer.

To solve:

- Go to collections
- Go to sample_training DB
- Go to trips collections
- In the filter input:

 ```{"birth year":1961, "start station name": "Howard St & Centre St"}```

- You should get a document which ending station is "South End Ave & Liberty St"

### Lecture: Find Command

- To connect to the atlas cluster run ```mongo <mongo_uri>```
- Admin: keeps track of users access to DBS.
- Once connected, *show dbs* shows the db
- You can use anyone of them by *use someDB*
- To view the collections: *show collections*
- To query a collection: db.*collectionName*.find({*query*})
- Shell limits the view to 20 documents. To keep on looking, type it (iterate), which iterates through the cursor object (which is a pointer to a result of a query)
- we can concatenate operations: db.collection.find().count()
- db.collection.find().pretty() helps visualizing it on the shell.
- An empty object in the find query would retrieve any document without a specific order.
- The mongoshell is fully javascript interpreter.

### Quiz: Find Command

What does it do in the mongo shell?

- [ ] Interferes with the task
- [ ] Warns about imminent termination
- [ ] it is not a mongo shell command
- [X] Iterates through the cursor results

### Quiz: The mongo shell

Which of the following statements are true about the mongo shell?

- [X] It allows you to interact with your MongoDB instance without using a Graphical User Interface
- [X] It is a fully functioning JavaScript interpreter
- [ ] mongo shell automatically returns an ordered list of results

### Your Chapter 2 IDE space

- Connection:
```mongo "mongodb+srv://something.somethingelse.mongodb.net/myFirstDatabase" --username m001-student```
- Input password: m001-mongodb-basics
- cls
- show dbs
- use sample_training

1. Using the sample_training.inspections collection find out how many inspections were conducted on Feb 20 2015.

 ```js
 db.inspections.find({"date":"Feb 20 2015"}).count()
 ```

Answer: 320 inspections

 1. Query the zips collection from the sample_training database to find all documents where the state is New York.

 ```js
 db.zips.find({"state": "NY"}).count()
 ```

 Answer: 1596

 2. Iterate through the query results.

 ```js
 it
 ```

 3. Find out how many ZIP codes there are in NY state.

 ```js
 db.zips.aggregate({$match: {"state":"NY"}},{$group:{_id:"$zip"}},{$count:"total_zip_codes"})
 ```

- Answer: 1596

 1. What about the ZIP codes that are in NY but also in the city of Albany?

 ```js
 db.zips.aggregate([ { '$match': { 'state': 'NY', 'city': 'ALBANY'}}, { '$count': 'Zip codes in Albany and NY'} ])
 ```

 Answer: 7

 5. Make the cursor look more readable.

 ```js
 .pretty()
 ```

## CHAPTER 3: CREATING AND UPDATING VALUES

### Inserting New Documents - ObjectID

- Create: both atlas, as well as as db.collection.insert/One()
- _id is enforced by default to have a 12 byte value.

### Quiz: Creating and manipulating data

How does the value of _id get assigned to a document?

- [ ] _id field values are sequential integer values.
- [X] You can select a non ObjectId type value when inserting a new document, as long as that value is unique to this document.
- [X] It is automatically generated as an ObjectId type value.
- [ ] When a document is inserted a random field is picked to serve as the _id field.

### Lecture: Inserting New Documents - insert() and errors

- Inserting documents: mongoimport, mongorestore, insert, insertMany, upsert
- .findOne(): good to understand the shape of the documents on a collection
- db.collection.insert({...})
- If we try to insert a document with an existing _id, it is going to throw an error (duplicate key error). nInserted: 0.
- You can check mongoDB validation Schema

### Quiz: Insert Error

Select all true statements from the following list:

- [ ] There is no way to ensure that duplicate records are not stored in MongoDB.
- [X] If a document is inserted without a provided **_id** value, then the **_id** field and value will be automatically generated for the inserted document before insertion.
- [ ] If a document is inserted without a provided _id value, then that document will fail to be inserted and cause a write error.
- [ ] MongoDB can always store duplicate documents in the same collection regardless of the _id value.
- [X] MongoDB can store duplicate documents in the same collection, as long as their _id values are different.

### Lecture: Inserting New Documents - insert() order

- Inserting documents: db.collection.insert([{},{},{}])
- Will treive:

```js
 bulkWriteResut({
 "writeErros":[],
 "nInserted": 3
 "nUpserted": 0,
 "nMatched": 0,
 "nModified": 0,
 "nRemoved": 0,
 "upserted": []
})
 ```

- When inserting many documents, if an error ocurrers, the documents afterwards wont be inserted.
- To change that add this option at the end: {"ordered": false}.
- Be carefull not to misstype the collection name. The default behaviour on MongoDB is to create it if it doesn't exist. Same for DBS.

### Quiz: Insert Order

Which of the following commands will successfully insert 3 new documents into an empty pets collection?

- [X] ```db.pets.insert([{ "pet": "cat"}, { "pet": "dog"},{ "pet": "fish"}])```

- [X] ```db.pets.insert([{ "_id": 1, "pet": "cat"},{ "_id": 1, "pet": "dog"},
 { "_id": 3, "pet": "fish"},
 { "_id": 4, "pet": "snake"}], { "ordered": false})```

- [X] ```db.pets.insert([{ "_id": 1, "pet": "cat"},
 { "_id": 2, "pet": "dog"},
 { "_id": 3, "pet": "fish"},
 { "_id": 3, "pet": "snake"}])```

- [ ] ```db.pets.insert([{ "_id": 1, "pet": "cat"},
 { "_id": 1, "pet": "dog"},
 { "_id": 3, "pet": "fish"},
 { "_id": 4, "pet": "snake"}], { "ordered": true})```

### Lecture: Updating Documents - Data Explorer

- Just use the UI. Beware of selecting the right data type.

### Quiz: Updating Documents

MongoDB has a flexible data model, which means that you can have fields that contain documents, or arrays as their values.

Select any invalid MongoDB documents from the given choices:

- [ ] ```{ "_id": 1,
 "pet": "cat",
 "attributes": [{ "coat": "fur",
 "type": "soft"},
 { "defense": "claws",
 "location": "paws",
 "nickname": "murder mittens"}],
 "name": "Furball"}```

- [ ] ```{ "_id": 1,
 "pet": "cat",
 "fur": "soft",
 "claws": "sharp",
 "name": "Furball"}```

- [ ] ```{ "_id": 1,
 "pet": "cat",
 "attributes": { "coat": "soft fur",
 "paws": "cute but deadly"},
 "name": "Furball"}```

- [X] None of the Above

### Lecture: Updating Documents - mongo shell

- Using MQL (mongo query language)
- updateOne, updateMany.
- With updateOne, the first document that matches will be updated.
- updateMany will match ALL the documents that match that given query.
- $set: updates a field or creates it if it doesn't exist.
- $inc, $push

### Quiz: Updating Documents in the shell

Given a pets collection where each document has the following structure and fields:

```js
{
 "_id": ObjectId("5ec414e5e722bb1f65a25451"),
 "pet": "wolf",
 "domestic?": false,
 "diet": "carnivorous",
 "climate": ["polar", "equatorial", "continental", "mountain"]
}

```

Which of the following commands will add new fields to the updated documents?

- [X] ``` db.pets.updateMany({ "pet": "cat"}, { "$push": { "climate": "continental","look": "adorable"}}) ```
- [ ] ``` db.pets.updateMany({ "pet": "cat"}, { "$set": { "domestic?": true, "diet": "mice"}}) ```
- [X] ``` db.pets.updateMany({ "pet": "cat"}, { "$set": { "type": "dangerous", "look": "adorable"}}) ```
- [ ] ``` db.pets.updateMany({ "pet": "cat"}, { "$set": { "climate": "continental"}})``

### Lecture: Deleting Documents and Collections

- deleteOne, deleteMany.
- Deleteone only to be used with _id, since it is the only way to guarantee that you are taking the right one.
- db.collection.drop() will drop the collection

### Quiz 1: Deleting Documents

The sample dataset contains a few databases that we will not use in this course. Clean up your Atlas cluster and get rid of all the collections in these databases:

sample_analytics
sample_geospatial
sample_weatherdata

Does removing all collections in a database also remove the database?

- [X] Yes
- [ ] No

### Quiz 2: Deleting Documents

Which of the following commands will delete a collection named villains?

- [X] db.villains.drop()
- [ ] db.villains.dropAll()
- [ ] db.villains.delete()

### IDE

1. Get a random document from a collection

 ```js
 db.collection.findOne()
 ```

2. Copy this random document, and insert it back to the collection. Do you get a "Duplicate Key" error?

    - Answer: yes.

3. Insert that document into the collection without the _id field to get a
 successfull insert. Did it work?

    - Answer: yes.

Practice Question:

People often confuse New York City as the capital of New York state, when in
reality the capital of New York state is Albany.

In the sample_training.zips collection add a boolean field "capital?" to all
documents pertaining to Albany NY, and New York, NY. The value of the field
should be true for all Albany documents and false for all New York documents.

```js
use sample_training
db.zips.updateMany({"city":"Albany"},{$set:{"capital": true}})

db.zips.updateMany({"city":"New York"},{$set:{"capital": false}})
```

## CHAPTER 04

### Lecture: Query Operators - Comparison

- Update operators: $inc, $set, $unset
- Enable to modify data in the DB.
- $eq
- $gt
- $gte
- $ne
- $lt
- $lte

### LAB

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

How many documents in the sample_training.zips collection have fewer than 1000 people listed in the pop field?

Copy/paste the exact numeric value of the result that you get into the response field.

```js
const pipeline = [ { '$match': { 'pop': { '$lt': 1000 }}}, { '$count': 'amount'}];
use sample_training
db.zips.aggregate(pipeline)
```

### LAB 2: COMPARISON OPERATORS

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

How many documents in the sample_training.zips collection have fewer than 1000 people listed in the pop field?

Copy/paste the exact numeric value of the result that you get into the response field.

```js
const pipeline = [{ '$match': { 'pop': { '$lt': 1000}}}, { '$count': 'amount'}];
use sample_training
db.zips.aggregate(pipeline)
```

### LAB 2: Comparison Operators

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

What is the difference between the number of people born in 1998 and the number of people born after 1998 in the sample_training.trips collection?

Enter the exact numeric value of the result that you get into the response field.

```js
const pipeline = [ { '$match': { 'birth year': { '$gte': 1998}}}, { '$group': { '_id': { '$cond': { 'if': { '$gt': [ '$birth year', 1998 ]}, 'then': 'greater than 1998', 'else': '1998'}}, 'count': { '$sum': 1}}}]
use sample_training
db.trips.aggregate(pipeline)
```

You will get 2 documents with the amount of them. The difference is **6**

### LAB 3

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

Using the sample_training.routes collection find out which of the following statements will return all routes that have at least one stop in them?

- [ ] ```db.routes.find({ "stops": { "$lt": 0}}).pretty()```
- [X] ```db.routes.find({ "stops": { "$ne": 0}}).pretty()```
- [X] ```db.routes.find({ "stops": { "$gt": 0}}).pretty()```
- [ ] ```db.routes.find({ "stops": { "$gte": 0}}).pretty()```

### Lecture: Query Operator - Logic

 $and: All of the query clauses - present on queries by default.
 $or: any of the query clauses
 $nor: fails to match both clauses (not and or together)
 $not: Negates the query requirements.

Explicit $and operator when we need to use it more than once in a query.

### Quiz 1: Logic Operators

```js
use sample_training
db.inspections.find({result: "Out of Business", sector:"Home Improvement Contractor - 100"})
```

Will return 4.

### Quiz 2: Logic Operators

Which is the most succinct query to return all documents from the sample_training.inspections collection where the inspection date is either "Feb 20 2015", or "Feb 21 2015" and the company is not part of the "Cigarette Retail Dealer - 127" sector?

- [X] ```db.inspections.find( { "$or": [{ "date": "Feb 20 2015"}, { "date": "Feb 21 2015"}], "sector": { "$ne": "Cigarette Retail Dealer - 127"}}).pretty()```
- [ ] ```db.inspections.find( { "$or": [{ "date": "Feb 20 2015"}, { "date": "Feb 21 2015"}], "$not": { "sector": "Cigarette Retail Dealer - 127"}}).pretty()```
- [ ] ```db.inspections.find( { "$and": [{ "$or": [{ "date": "Feb 20 2015"}, { "date": "Feb 21 2015"}]}, {"s ector": { "$ne":"Cigarette Retail Dealer - 127"}}]}).pretty()```

$not operator on this one is not used properly.

### Lab 1: Logic Operators

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

Before solving this exercise, make sure to undo some of the changes that we made to the zips collection ea rlier in the course by running the following command:

```js
db.zips.updateMany({ "city": "HUDSON"}, { "$inc": { "pop": -10}})
```

How many zips in the sample_training.zips dataset are neither over-populated nor under-populated?

In this case, we consider population of more than 1,000,000 to be over- populated and less than 5,000 to be under-populated.

Copy/paste the exact numeric value of the result that you get into the response field.

```js
db.zips.find({$nor:[{'pop':{$lt:5000}},{'pop':{$gt:1000000}}]}).count()
```

Another way:

```js
const pipeline = [ { '$group': { '_id': { '$switch': { 'branches': [ { 'case': { '$or': [ { '$lt': [ '$pop', 5000 }, { '$gt': '$pop', 1000000 ] } ] }, 'then': 'over and under Populated' } ], 'default': 'well populated' } }, 'amount': { '$sum': 1 } }]
db.zips.aggregate(pipeline)
```

Should retrieve back **11193**.

### Lab 2: Logic Operators

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

How many companies in the sample_training.companies dataset were

either founded in 2004

[ and ] either have the social category_code [ or ] web category_code,
[ or ] were founded in the month of October

[ and ] also either have the social category_code [ or ] web category_code?
Copy/paste the exact numeric value of the result that you get into the response field.

```js
db.companies.find({$and: [{"$or": [{"founded_year":2004}, {"founded_month":10}]}, {"category_code": {"$in":["social", "web"]}}]}).count()
```

Without the $and:

```js
db.companies.find({"$or": [{"founded_year":2004}, {"founded_month":10}], "category_code": {"$in":["social", "web"]}}).count()
```

### Lecture: Expressive Query Operator

Allows to compare fields within the same documents.without specyfing its value.

{$expr:{expression}}

- Dolar sign is used to indicate the value of a field $pop, is the value at pop.

### Quiz 1: $expr

What are some of the uses for the $ sign in MQL?

- [ ] $ makes the world go round.
- [X] $ signifies that you are looking at the value of that field rather than the field name.
- [X] $ denotes an operator.
- [ ] $ changes the data type of the given value to a monetary denomination.

### Quiz 2: $expr

Which of the following statements will find all the companies that have more employees than the year in which they were founded?

- [x] ``` db.companies.find( { "$expr": { "$gt": [ "$number_of_employees", "$founded_year" ]} } ).count() ```
- [ ] ``` db.companies.find( { "$expr": { "$gt": [ "$founded_year", "number_of_employees" ] } }).count() ```
- [X] ``` db.companies.find( { "$expr": { "$lt": [ "$founded_year","$number_of_employees" ] } } ).count() ```
- [ ] ``` db.companies.find({ "number_of_employees": { "$gt": "$founded_year" } }).count() ```

Without the $expr, the last query doesn't know on which document look for $founded_year, so it will return 0.

### Lab: $expr

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

How many companies in the sample_training.companies collection have the same permalink as their twitter_username?

```js
db.companies.find({$expr:{$eq:['$permalink', '$twitter_username']}}).count()
```

Answer: **1299**

### Lecture: Array Operators

- $push. Adds an element to array or turns a field into an array if it has a different type.

{"amenities":"shampoo"} // will retrieve also the elements that amenities is an array and contains the word shampoo.

{"amenities":[ "shampoo" ]} // will retrieve all documents that matches EXACTLY that array (order of elements also important)

That is why we have the $all, $in operators.

$size: matches the size of an array.

### Lab 1: Array Operators

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

What is the name of the listing in the sample_airbnb.listingsAndReviews dataset that accommodates more than 6 people and has exactly 50 reviews?

Copy/Paste the value of the "name" field into the response field without quotation marks.

```js
db.listingsAndReviews.find({reviews:{$size:50}, accommodates:{$gt:6}}, {_id:0, name:1})
```

### LAB 2: Array Operators

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

Using the sample_airbnb.listingsAndReviews collection find out how many documents have the "property_type" "House", and include "Changing table" as one of the "amenities"?

Enter the number of results to the response field.

```js
db.listingsAndReviews.find({"property_type":"House", "amenities":{$in:['Changing table']}}).count()
```

Answer: **11**

### Quiz: Array Operators

Which of the following queries will return all listings that have "Free parking on premises", "Air conditioning", and "Wifi" as part of their amenities, and have at least 2 bedrooms in the sample_airbnb.listingsAndReviews collection?

- [ ] ``` db.listingsAndReviews.find( { "amenities": "Free parking on premises", "amenities": "Wifi", "amenities": "Air conditioning", "bedrooms": { "$gte": 2 } }).pretty() ```
- [ ] ``` db.listingsAndReviews.find( { "amenities": { "$all": [ "Free parking on premises", "Wifi", "Air conditioning" ] }, "bedrooms": { "$lte": 2 } }).pretty() ```
- [X] ``` db.listingsAndReviews.find( { "amenities": { "$all": [ "Free parking on premises", "Wifi", "Air conditioning" ] }, "bedrooms": { "$gte": 2 } } ).pretty() ```
- [ ] ``` db.listingsAndReviews.find( { "amenities": [ "Free parking on premises", "Wifi", "Air conditioning" ]}, "bedrooms": { "$gte": 2 } } ).pretty() ```

### Lecture: Array Operators and Projection

- Projection: allows to look only into fields that we are interested on.
- Fields you want, 1. Fields you don't want: 0.
- _id is added by default.
- Projecting with 0 a key, will trhow an error, since we can't mix inclusion and exclusion
 $elemMatch can be used in the projetion part of the query.
 matches documents that contain an array field with at leas one element that meets the conditions.

### Lab: Array Operators and Projection

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

How many companies in the sample_training.companies collection have offices in the city of Seattle?

Copy/paste your answer to the response field.

``` js
db.companies.find({offices: {$elemMatch: {"city":"Seattle"}}}).count()
```

Answer: **117**

### Quiz: Array Operators and Projection

Which of the following queries will return only the names of companies from the sample_training.companies collection that had exactly 8 funding rounds?

- [ ] ``` db.companies.find({ "funding_rounds": { "$size": 8 } }, { "name": 0, "_id": 1 }) ```
- [ ] ``` db.companies.find({ "funding_rounds": { "$size": 8 } }, { "name": 1 }) ```
- [X] ``` db.companies.find({ "funding_rounds": { "$size": 8 } }, { "name": 1, "_id": 0 }) ```

### Lecture: Array Operators and Sub-Documents

- Querying subdocuments.
- Dot notation.
- {"something.something": "lookedvalue"}
- Also can access arrays by index

### Lab 1: Querying Arrays and Sub-Documents

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

Longitude decreases in value as you move west.

How many trips in the sample_training.trips collection started at stations that are to the west of the -74 longitude coordinate?

```js
db.trips.find({"start station location.coordinates.0": {$lt:-74}}).count()
```

Answer: **1928**

### Lab 2: Querying Arrays and Sub-Documents

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

How many inspections from the sample_training.inspections collection were conducted in the city of NEW YORK?

```js
db.inspections.find({"address.city":"NEW YORK"}).count()
```

Answer: **18279**

### Quiz: Querying Arrays and Sub-documents

Which of the following queries will return the names and addresses of all listings from the sample_airbnb.listingsAndReviews collection where the first amenity in the list is "Internet"?

- [ ] ``` db.listingsAndReviews.find({ "amenities.[0]": Internet" , { "name": 1, "address": 1 }).pretty() ```
- [X] ``` db.listingsAndReviews.find({ "amenities.0": "Internet" }, { "name": 1, "address": 1 }).pretty() ```
- [ ] ``` db.listingsAndReviews.find({ "amenities.$0": "Internet" },{ "name": 1, "address": 1 }).pretty() ```

### CHAPTER 4 IDE

Query Operators - Comparison

1. How many documents in the sample_training.zips collection have fewer than
 1000 people listed in the pop field?

 ```js
 db.zips.find({"pop":{$lt: 1000}}).count()
 ```

2. What is the difference between the number of people born in 1998 and the
 number of people born after 1998 in the sample_training.trips collection?

```js
 db.trips.find({"birth year":1998}).count() // 12
 db.trips.find({"birth year": {$gt:1998}}).count() // 18
 ```

3. Using the sample_training.routes collection find out which of the
 following statements will return all routes that have at least one stop
 in them?

- [X] ```db.routes.find({ "stops": { "$gt": 0 }}).pretty()```
- [ ] ```db.routes.find({ "stops": { "$gte": 0 }}).pretty()```
- [x] ```db.routes.find({ "stops": { "$ne": 0 }}).pretty()```
- [ ] ```db.routes.find({ "stops": { "$lt": 10 }}).pretty()```

Query Operators - Logic

1. How many businesses in the sample_training.inspections dataset have the
 inspection result "Out of Business" and belong to the Home Improvement
 Contractor - 100 sector?

``` js
db.inspections.find({result: "Out of Business", sector:"Home Improvement Contractor - 100"}).count()
```

Answer: **4**

2. How many zips in the sample_training.zips dataset are neither over-
 populated nor under-populated?In this case, we consider population over 1,000,000 to be over-populated and under 5,000 to be under-populated.

 ```js
 db.zips.find({pop:{$gte:5000, $lt:1000000}}).count()
 ```

Answer: **11193**

3. How many companies in the sample_training.companies dataset were either
 founded in 2004, or in the month of October and either have the social
 category_code or web category_code?

``` js
db.companies.find({$or:[{founded_year: 2004}, {founded_month: 10}], $or:[{category_code:"social"}, {category_code: "web"}]}).count()
```

Answer: **1981**

Expressive Query Operator

How many companies in the sample_training.companies collection have the same
permalink as their twitter_username?

```js
db.companies.find({$expr:{$eq:["$twitter_username", "$permalink"]}}).count()
```

Answer: **1299**

Array Operators

1. What is the name of the listing in the sample_airbnb.listingsAndReviews
 dataset accommodate more than 6 people and has exactly 50 reviews?

 ```js
 db.listingsAndReviews.find({accommodates:{$gt:6}, reviews:{$size:50}}, {name:1, _id:0})
 ```

Answer: **Sunset Beach Lodge Retreat**

2. How many documents have the property_type House, and include Changing
 table as one of the amenities?

Array Operators and Projection

How many companies in the sample_training.companies collection have offices
in the city of Seattle?

Array Operators and Sub-Documents

1. Latitude decreases in value as you move west.

 How many trips in the sample_training.trips collection started at
 stations that are to the west of the -74 latitude coordinate?
2. How many inspections from the sample_training.inspections collection were
 conducted in the city of New York?

## CHAPTER 5

### Lecture: Aggregation framework

- Another way to query data
- We use aggregate instead of find.
- In pipelines, the order is important.
- Each stage of the pipeline works as a filter. Each filter should be finest than the previous one.
- We can reshape the data
- $group
- Compute, reshape and reorganize data
- In form of a pipeline

### Lab: Aggregation Framework

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

What room types are present in the sample_airbnb.listingsAndReviews collection?

```js
db.listingsAndReviews.aggregate({$group: {_id: "$room_type", count: {$sum: 1}}})
```

- [X] Shared room
- [ ] Living room
- [ ] Apartment
- [ ] Kitchen
- [X] Private room
- [X] Entire home/apt
- [ ] House

### Quiz: Aggregation Framework

What are the differences between using aggregate() and find()?

- [X] aggregate() allows us to compute and reshape data in the cursor.
- [ ] find() can do what the aggregate() can do and more.
- [ ] find() allows us to compute and reshape data in the cursor.
- [X] aggregate() can do what find() can and more.

### Lecture: sort() and limit()

- sort: 1 is ascending, -1 deschending.
- sort and limit are cursor methods as well as pretty and count
- limit without sort doesn't guarantee any order
- mongo asummes that you meant to sort before limit.

### Quiz 1: sort() and limit()

Which of the following commands will return the name and founding year for the 5 oldest companies in the sample_training.companies collection?

Check all answers that apply:

- [X] ``` db.companies.find({ "founded_year": { "$ne": null }}, { "name": 1, "founded_year": 1 } ).limit(5).sort({ "founded_year": 1 }) ```
- [ ] ``` db.companies.find({ },{ "name": 1, "founded_year": 1 } ).sort({ "founded_year": 1 }).limit(5) ```
- [X] ``` db.companies.find({ "founded_year": { "$ne": null }}, { "name": 1, "founded_year": 1 } ).sort({ "founded_year": 1 }).limit(5) ```
- [ ] ``` db.companies.find({ "name": 1, "founded_year": 1 } ).sort({ "founded_year": 1 }).limit(5) ```

Number 2 is not right because is not filtering null values (which this collection has)

### QUIZ N2

Problem:

To complete this exercise connect to your Atlas cluster using the in-browser IDE space at the end of this chapter.

In what year was the youngest bike rider from the sample_training.trips collection born?

```js
db.trips.find({"birth year": {$ne: ""}}, {"birth year": 1, _id: 0 }).sort({"birth year": -1}).limit(1)
```

- [ ] 1885
- [X] 1999
- [ ] 2000
- [ ] 1998

### Lecture: Introduction to Indexes

- Indexes should be built to support the queries
- db.col.createIndex( {field: 1/-1} )
- Single field index.
- Compound index.

### Quiz: Introduction to Indexes

Problem:
Jameela often queries the sample_training.routes collection by the src_airport field like this:

```js
db.routes.find({ "src_airport": "MUC" }).pretty()
```

Which command will create an index that will support this query?

- [ ] db.routes.generateIndex({ "src_airport": -1 })
- [ ] db.routes.addIndex({ "src_airport": 1 })
- [X] db.routes.createIndex({ "src_airport": -1 })
- [ ] db.routes.makeIndex({ "src_airport": 1 })

### Lecture: Introduction to Data Modeling

- way to organize fields in a document to support your application performance and querying capabilities
- Data is stored in the way that is used
- How data is going to be queried?

### QUIZ: Introduction to data modeling

- [ ] a way to decide whether to store your data in the cloud or locally
- [ ] a way to show off your amazing data to everyone using graphs and illustrations
- [x] a way to organize fields in a document to support your application performance and querying capabilities
- [ ] a way to build your application based on how your data is stored

### Lecture: Upsert - Update or insert

- db.collection.updateOne({query},{update}, {upsert: true})
- Update(if exists) or insert (if no documents matches)
- Case of use: sensor that writes info in a document
  
### QUIZ: Upsert

How does the upsert option work?

- [X] By default upsert is set to false.
- [X] When upsert is set to false and the query predicate returns an empty cursor then there will be no updated documents as a result of this operation.
- [X] When upsert is set to true and the query predicate returns an empty cursor, the update operation creates a new document using the directive from the query predicate and the update predicate.
- [ ] It is used with the update operator, and needs to have its value specified every time that the update operator is called.

### Chapter 5 IDE

Aggregation Framework

1. Using the aggregation framework find all documents that have Wifi as one
   of the amenities. Only include price and address in the resulting cursor.

2. Which countries have listings in the sample_airbnb database?
3. How many countries have listings in the sample_airbnb database?

sort() and limit()

1. Find the least populated ZIP code in the zips collection.
2. Find the most populated ZIP code in the zips collection.
3. Find the top ten most populated ZIP codes.
4. Get results sorted in increasing order by population, and decreasing
   order by city name.

Introduction to Indexes

Create two separate indxes to support the following queries:

db.trips.find({"birth year": 1989})

db.trips.find({"start station id": 476}).sort("birth year": 1)