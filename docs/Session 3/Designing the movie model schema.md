## Introduction to Data Modeling
   - **Concept**: Data modeling defines how data is stored and organized in a database.
   - **Importance**: Enhances data retrieval efficiency, maintains data integrity, and simplifies application maintenance.

## Understanding Document-Oriented Databases
   - **MongoDB Documents**: Stores data in JSON-like documents (BSON format) that are flexible and schema-less.
   - **Collections**: Documents are grouped into collections, similar to tables in relational databases.

## Identifying Entities and Relationships
   - **Primary Entities**: `Movies`, `cast`, and `reviews`.
   - **Relationships**: `Movies` have `cast`s and `review`s.

## Defining the Movie Schema
   - **Fields**: 
     - **Title**: The name of the movie (string, required).
     - **Year**: The release year of the movie (number, required).
     - **Genre**: The genre of the movie (string, required).
     - **Director**: The director of the movie (string, optional).
     - **Cast**: An array of objects containing cast member references and their roles.
     - **Reviews**: An array of embedded review documents.

## Example Movie Document
   ```json
   {
     "_id": ObjectId("60c72b2f9b1d8b3f0c6e6a2e"),
     "title": "Inception",
     "year": 2010,
     "genre": "Sci-Fi",
     "director": "Christopher Nolan",
     "cast": [
       { "_id": ObjectId("60c72b2f9b1d8b3f0c6e6a2f"), "role": "Dom Cobb" },
       { "_id": ObjectId("60c72b2f9b1d8b3f0c6e6a30"), "role": "Arthur" }
     ],
     "reviews": [
       {
         "_id": ObjectId("60c72b2f9b1d8b3f0c6e6a31"),
         "user": "John Doe",
         "rating": 5,
         "comment": "Excellent movie!"
       },
       {
         "_id": ObjectId("60c72b2f9b1d8b3f0c6e6a32"),
         "user": "Jane Smith",
         "rating": 4,
         "comment": "Great visuals and story."
       }
     ]
   }
   ```

## Designing the Cast Schema
   - **Fields**:
     - **Name**: The name of the cast member (string, required).
     - **Date of Birth**: The date of birth of the cast member (date, optional).
   - **Example Cast Document**:
     ```json
     {
       "_id": ObjectId("60c72b2f9b1d8b3f0c6e6a2f"),
       "name": "Leonardo DiCaprio",
       "date_of_birth": ISODate("1974-11-11")
     }
     ```
## Embedding vs. Referencing
   - **Embedding**: Storing related data directly within a single document. Best for data that is often read together.
   - **Referencing**: Storing related data in separate documents and linking them via ObjectId. Best for data that is shared across multiple documents.
   - **Choice**: Using embedding for reviews to keep them closely tied to their respective movies, and references for cast members to allow for reuse and maintain normalization.

## Querying with References and Embedding
   - **Basic Queries**:
     - **Find Movies by Genre**:
       ```javascript
       db.movies.find({ genre: "Sci-Fi" })
       ```
     - **Find Movies by Year**:
       ```javascript
       db.movies.find({ year: 2010 })
       ```

   - **Advanced Queries**:
     - **Find Movies by Cast Member**:
       ```javascript
       // Assuming the cast member's ObjectId is known
       var castId = ObjectId("60c72b2f9b1d8b3f0c6e6a2f");
       db.movies.find({ "cast._id": castId })
       ```
     - **Find Movies by Reviewer**:
       ```javascript
       // Assuming the reviewer's user name is known
       var userName = "John Doe";
       db.movies.find({ "reviews.user": userName })
       ```

   - **Using Aggregation for Joins**:
     - **Populate Cast Information**:
       ```javascript
       db.movies.aggregate([
         { $match: { title: "Inception" } },
         {
           $lookup: {
             from: "cast",
             localField: "cast._id",
             foreignField: "_id",
             as: "castDetails"
           }
         }
       ])
       ```

## Benefits of Using References and Embedding
- **Data Normalization**: Avoids data duplication by storing shared data (like cast members) separately.
- **Scalability**: Embedding reviews within movies simplifies data retrieval and makes it easier to scale the database as related data grows.
- **Flexibility**: Allows for more complex queries and relationships between different entities.
