1. Create a database named `blog`.
use blog

2. Create a collection called 'articles'.
db.createCollection('articles')
3. Insert multiple documents(at least 3) into articles. It should have fields
db.articles.insertMany([{name: 'Virat', title : 'The Run Machine', tags :['cricket', 'test'], age :29},{name: 'Rohit',title : 'The Hitman' tags : ['cricket', 'one-day'], age :32},{name: 'Dhoni',title : 'Helicopter' tags : ['cricket', 't20'], age :36}])
4. Find all the articles using `db.COLLECTION_NAME.find()`
db.articles.find();

5. Find a document using _id field.
db.articles.find({ "_id" : ObjectId("5d9ffc48674a5eb252550471")});

6. Find documents using title and author's name field.
db.articles.find({name: 'Virat', title: 'The Run Machine'});

7. Find document using a specific tag.
db.articles.find({"tag" : {$all : ['one-day']}});
db.articles.find({"tag" : {$all : ['t20']}});
db.articles.find({"tag" : {$all : ['test']}});
db.articles.find({"tag" : {$all : ['cricket']}});

8. Update title of a document using its _id field.
db.articles.update({_id: ObjectId("5d9ffc48674a5eb252550471")}, {$set: {title: 'The Wonder'}});

9. Update a author's name using article's title.
db.articles.update({title: 'The Run Machine'}, {$set: {name: 'Virat Kohli'}});

10. rename details field to description from articles collection. 
db.articles.update({name: "Dhoni"}, {$set: {details: "I am an ordinary player"}});
db.articles.update({name: "Dhoni"}, {$rename: {"details":"description"}});

11. Add additional tag in a specific document.
db.articles.update({name: "Rohit"}, {$push: {tag: "genius"}});

12. Update an article's tags using $set and without $set.
  - Write the differences here ?
  with $set: replaces the tag field only.
db.articles.update({name: "Dhoni"}, {$set: {tag: ["hello"]}});

without $set: replaces all the field with tag field.
db.articles.update({name: "Dhoni"}, {tag: ["hello-world"]});

13. Increment an auhtor's age by 5.  
db.articles.update({name: "Dhoni"}, {$inc: {age: 5}});
db.articles.update({name: "Virat Kohli"}, {$inc: {age: 5}});
db.articles.update({name: "Rohit"}, {$inc: {age: 5}});
14. Delete a document using _id field with `db.COLLECTION_NAME.remove()`.
db.articles.remove({_id: ObjectId("5d9ffc48674a5eb252550471")});

Use sample.js data for below queries.

1. Find all males who play cricket.
db.users.find({gender: "Male", sports: {$all: ['football']}});
2. Update user with extra golf field in sports array whose name is "Steve Ortega".
db.users.update({name: "Steve Ortega"}, {$push: {sports: "golf"}});
3. Find all users who play either 'football' or 'cricket'.
db.users.find({sports: {$in: ['football', 'cricket']}});
4. Find all users whose name includes 'ri' in their name.
db.users.find({name: /ri/i});