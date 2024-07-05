#### **1. Start Mongo Shell** (Skip while using MongoDB Compass)

```bash
mongo
```
- Opens the Mongo Shell where you can run MongoDB commands.

#### **2. Select a Database**

- **Command**:
  ```javascript
  use <database_name>
  ```
- **Example**:
  ```javascript
  use myDatabase
  ```
- **Details**: **If the database doesn’t exist, MongoDB will create it when you add data.**

#### **3. Create a Collection**

- **Command**:
  ```javascript
  db.createCollection("<collection_name>")
  ```
- **Example**:
  ```javascript
  db.createCollection("movies")
  ```
- **Details**: Collections are created automatically when you first insert data, but you can create them manually if needed.

#### **4. Insert Documents**

- **Command**:
  ```javascript
  db.<collection_name>.insertOne(<document>)
  db.<collection_name>.insertMany([<document1>, <document2>])
  ```
- **Examples**:
  ```javascript
  db.movies.insertOne({ title: "Inception", year: 2010, genre: "Sci-Fi" })
  db.movies.insertMany([
    { title: "The Matrix", year: 1999, genre: "Sci-Fi" },
    { title: "Interstellar", year: 2014, genre: "Sci-Fi" }
  ])
  ```
- **Details**: `insertOne()` adds a single document, `insertMany()` adds multiple documents.

#### **5. Find Documents**

- **Command**:
  ```javascript
  db.<collection_name>.find(<query>)
  db.<collection_name>.findOne(<query>)
  ```
- **Examples**:
  ```javascript
  db.movies.find() // Retrieve all documents in the collection
  db.movies.find({ genre: "Sci-Fi" }) // Find all Sci-Fi movies
  db.movies.findOne({ title: "Inception" }) // Find a single document matching the query
  ```
- **Details**: 
	- `find()` retrieves multiple documents
	- `findOne()` retrieves a single document

#### **6. Update Documents**

- **Command**:
  ```javascript
  db.<collection_name>.updateOne(<query>, <update>)
  db.<collection_name>.updateMany(<query>, <update>)
  ```
- **Examples**:
  ```javascript
  db.movies.updateOne({ title: "Inception" }, { $set: { year: 2011 } }) // Update a single document
  db.movies.updateMany({ genre: "Sci-Fi" }, { $set: { genre: "Science Fiction" } }) // Update multiple documents
  ```
- **Details**: 
	- `$set` updates the specified fields. 
	- Other update operators include:
		- `$inc` for incrementing
		- `$push` for adding items to arrays

#### **7. Delete Documents**

- **Command**:
  ```javascript
  db.<collection_name>.deleteOne(<query>)
  db.<collection_name>.deleteMany(<query>)
  ```
- **Examples**:
  ```javascript
  db.movies.deleteOne({ title: "Inception" }) // Delete a single document
  db.movies.deleteMany({ genre: "Sci-Fi" }) // Delete multiple documents
  ```
- **Details**: 
	- `deleteOne()` removes one document
	- `deleteMany()` removes all documents matching the query.

#### **8. Drop a Collection (DANGER)**

- **Command**:
  ```javascript
  db.<collection_name>.drop()
  ```
- **Example**:
  ```javascript
  db.movies.drop()
  ```
- **Details**: Removes the entire collection and all its documents.

#### **9. List All Databases**

- **Command**:
  ```javascript
  show dbs
  ```
- **Details**: Lists all databases on the server.

#### **10. List Collections in a Database**

- **Command**:
  ```javascript
  show collections
  ```
- **Details**: Lists all collections in the currently selected database.

#### **11. Count Documents**

- **Command**:
  ```javascript
  db.<collection_name>.countDocuments(<query>)
  ```
- **Example**:
  ```javascript
  db.movies.countDocuments({ genre: "Sci-Fi" })
  ```
- **Details**: Counts the number of documents matching the query. (If query isnt provided, it returns count of all documents)

#### **12. Basic Aggregation**

- **Command**:
  ```javascript
  db.<collection_name>.aggregate([<pipeline_stage1>, <pipeline_stage2>])
  ```
- **Example**:
  ```javascript
  db.movies.aggregate([
    { $match: { genre: "Sci-Fi" } },
    { $group: { _id: "$year", count: { $sum: 1 } } }
  ])
  ```
- **Details**: Performs complex queries involving multiple stages like `$match`, `$group`, and `$sort`.

### Summary Table

| Operation               | Command Example                                                         | Description                                        |
| ----------------------- | ----------------------------------------------------------------------- | -------------------------------------------------- |
| **Start Mongo Shell**   | `mongo`                                                                 | Opens the MongoDB Shell.                           |
| **Select a Database**   | `use myDatabase`                                                        | Switches to the specified database.                |
| **Create a Collection** | `db.createCollection("movies")`                                         | Creates a new collection.                          |
| **Insert Documents**    | `db.movies.insertOne({ title: "Inception", year: 2010 })`               | Adds new documents to a collection.                |
| **Find Documents**      | `db.movies.find({ genre: "Sci-Fi" })`                                   | Retrieves documents from a collection.             |
| **Update Documents**    | `db.movies.updateOne({ title: "Inception" }, { $set: { year: 2011 } })` | Updates existing documents.                        |
| **Delete Documents**    | `db.movies.deleteOne({ title: "Inception" })`                           | Deletes documents from a collection.               |
| **Drop a Collection**   | `db.movies.drop()`                                                      | Deletes the entire collection.                     |
| **List All Databases**  | `show dbs`                                                              | Lists all databases.                               |
| **List Collections**    | `show collections`                                                      | Lists all collections in the current database.     |
| **Count Documents**     | `db.movies.countDocuments({ genre: "Sci-Fi" })`                         | Counts documents matching a query.                 |
| **Basic Aggregation**   | `db.movies.aggregate([ { $match: { genre: "Sci-Fi" } } ])`              | Performs advanced queries with aggregation stages. |

### Additional Resources
- [MongoDB Documentation](https://www.mongodb.com/docs/manual/)
- [MongoDB Shell Commands](https://www.mongodb.com/docs/manual/mongo/)
- [MongoDB Aggregation Framework](https://www.mongodb.com/docs/manual/aggregation/