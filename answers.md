## 2. Database and Collection Creation
use library
db.createCollection("books")

## 3. Insert Data
db.books.insertMany([
  { title: "Book One", author: "Author A", publishedYear: 1999, genre: "Fiction", ISBN: "111" },
  { title: "Book Two", author: "Author B", publishedYear: 2005, genre: "Sci-Fi", ISBN: "222" },
  { title: "Book Three", author: "Author A", publishedYear: 2010, genre: "Mystery", ISBN: "333" },
  { title: "Book Four", author: "Author C", publishedYear: 2020, genre: "Romance", ISBN: "444" },
  { title: "Book Five", author: "Author D", publishedYear: 2018, genre: "Non-fiction", ISBN: "555" }
])

## 4. Retrieve Data
db.books.find()
db.books.find({ author: "Author A" })
db.books.find({ publishedYear: { $gt: 2000 } })

## 5. Update Data
db.books.updateOne({ ISBN: "111" }, { $set: { publishedYear: 2001 } })
db.books.updateMany({}, { $set: { rating: 5 } })

## 6. Delete Data
db.books.deleteOne({ ISBN: "222" })
db.books.deleteMany({ genre: "Non-fiction" })

## 7. Data Modeling for E-Commerce
# Users Collection Example
{
  "_id": ObjectId("..."),
  "name": "John Doe",
  "email": "johndoe@example.com",
  "orders": [ObjectId("...")]
}

# Orders Collection Example
{
  "_id": ObjectId("..."),
  "user_id": ObjectId("..."),
  "products": [ObjectId("...")],
  "total_price": 100,
  "status": "Shipped"
}

# Products Collection Example
{
  "_id": ObjectId("..."),
  "name": "Laptop",
  "description": "Gaming Laptop",
  "price": 1500,
  "stock": 10,
  "category": "Electronics"
}

## 8. Aggregation Pipeline
db.books.aggregate([
  { $group: { _id: "$genre", count: { $sum: 1 } } }
])
db.books.aggregate([
  { $group: { _id: null, avgYear: { $avg: "$publishedYear" } } }
])
db.books.find().sort({ rating: -1 }).limit(1)

## 9. Indexing
db.books.createIndex({ author: 1 })
