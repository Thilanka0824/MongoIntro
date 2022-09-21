# MongoIntro

- Insert the 10 sample blogs into the blogs collection with the following datatypes per field: 
{
 "createdAt": {Date},
 "title": {String},
 "text": {String},
 "author": {String},
 "lastModified": {Date},
 "categories": {String[]},
 "id": {String},
 "objectId": {Number}
}

db.blogs.insertMany([one, two, three, four, five, six, seven, eight, nine, ten])

- Insert a new blog into the collection

const eleven = 
    {
	 createdAt: new Date("2022-04-16T06:33:29.080Z"),
	 title : "",
	 text: "",
	 author: "Ronald Barrows",
	 lastModified: new Date(),
	 categories: ["nulla", "quasi", "beatae"],
	 id: "dcc2102d-a20a-4765-8dc4-9079af9fdc9b",
	 objectId: 11
	}
	
db.blogs.insertOne(eleven)

- Find one blog by author

 db.blogs.find({
    author: "Ronald Barrows"
})

- Find all blogs whose objectId is greater than 5

db.blogs.find({
    objectId: {
        $gt: 5
    }
})

- Find all blogs whose createdAt is greater than April 1, 2022

db.blogs.find({
    createdAt: {
        $gt: new Date("2022-04-01") 
    }
})

- Find all blogs where the field lastModified exists

db.blogs.find({
    lastModified: {
        $exists: true
    }
})

- Find all blogs where the createdAt type is a date

db.blogs.find({
    createdAt: {
        $type: "date"
    }
})

- Stretch

- Find a blog with a specific phrase in the text

db.blogs.find({
    text: {
        $regex: /nam explicabo/
    }
})

- Find all blogs that have "qui" in the categories array

db.blogs.find({
    categories: {
        $in: ["qui"]
    }
})


- Find all blogs in which the lastModified does not exist and set it

db.blogs.updateMany({
   lastModified: {
       $exists: false
   }
},{
    $set:{
        lastModified: new Date()
    }
})

- From now on, all the following queries should update lastModified to be the current datetime 

- Find all blogs created after May 2022 and add "lorem" as a new category in the categories array

db.blogs.updateMany({
    createdAt: {$gt: new Date("2022-05-01")},
    {$addToSet: {
        categories: "lorem"},
        $set: {lastModified: new Date()}
    }
    
})

- Find all blogs that have the category "voluptas" and pull "voluptas" from the categories

db.blogs.updateMany({
    categories: {$in: ["voluptas"]}
},{$pull:{
    categories: "voluptas"},
     $set: {lastModified: new Date()
})

- Find all blogs with "corrupti" in the categories and delete those blogs

db.blogs.deleteMany({
    categories: {$in: ["corrupti"]}
})