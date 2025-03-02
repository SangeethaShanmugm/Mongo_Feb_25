Index => used when your having more amount of data 
_id => default index
Quick Search
index make your app query faster

Types
------

default index => _id
hashed index => hashed set for sharding => availability
text index => search based on text
geospatial => location, position
single field index => single index, sort operation
compound index => multiple fields
multi-key index => array data 
sparse index => make sure that key over index is unique also it doesnt include null

properties of index
----------------------

TTL index => Total time to live => used to delete document in mongodb automatically after specified amount of time
unique index => ensure duplicate values of index field
sparse index => ensures that search of document having indexed field without null


create index
---------------

db.collection.createIndex()

db.emp.insert(
    {
        emp_id:1001,
        firstName: "Aakash",
        lastName:"Mecwan",
        email:"aakash@gmail.com",
        phone:1234567,
        Job_id:"E3",
        sal:"200000",
        manager_id:"102",
    }
)


db.emp.find().pretty()

db.emp.insert(
    {
        emp_id:1002,
        firstName: "Anmol",
        lastName:"Singh",
        email:"anmol@gmail.com",
        phone:784674364,
        Job_id:"E4",
        sal:"400000",
        manager_id:"105",
    }
)


db.emp.createIndex({ "Job_id":1})

db.emp.getIndexes()

db.emp.find({Job_id:"E4"}).explain("executionStats")

db.emp.dropIndex({ "Job_id":1})


hashed index
----------------

hashed index support hashed sharding => shard key
use cases
----------
load balancing => distributing req to other servers

db.emp.createIndex({ "Job_id":"hashed"})

db.createView("empView","emp", [
    {$project: {emp_id:1, firstName:1, lastName:1, email:1} }
])

text index
--------------

db.article.insert(
    [
        {"text":"indians with cricket", "tags":["indians","cricket"]},
         {"text":"economy of india", "tags":["economy","india"]},
          {"text":"nature and beauty of himalayas", "tags":["himalayas","nature"]},
           {"text":"beauty of india", "tags":["beauty","india"]},
    ]
)

db.article.find().pretty()

db.article.createIndex({text:"text"})

db.article.getIndexes()

db.article.find({$text:{$search:"india"}}) => exact match

db.article.find({tags:{$regex:"ind"}}).pretty()

db.article.find({tags:{$regex:"h"}}).pretty()




db.quotes.insertMany( [
   {
      _id: 1,
      quote : "La suerte protege a los audaces."
   },
   {
      _id: 2,
      quote: "Nada hay más surrealista que la realidad."
   },
   {
      _id: 3,
      quote: "Es este un puñal que veo delante de mí?"
   },
   {
      _id: 4,
      quote: "Nunca dejes que la realidad te estropee una buena historia."
   }
] )


db.quotes.createIndex(
    {quote:"text"},
    {default_language:"spanish"}
)


db.quotes.find({$text:{$search:"suerte"}})

db.quotes.find({$text:{$search:"spanish"}})



TTL
---

db.quotes.createIndex({_id_1:1}, {expireAfterSeconds: 60})

db.quotes.createIndex({createdAt: 1}, {expireAfterSeconds: 60})


db.quotes.getIndexes()

db.quotes.insertOne(
     {
      _id: 5,
      quote: "Nunca dejes que la realidad",
      createdAt: new Date()
   }
)



db.logs.insertMany([
  { _id: 1, message: "User logged in", createdAt: new Date() },
  { _id: 2, message: "User updated profile", createdAt: new Date() },
  { _id: 3, message: "Payment processed", createdAt: new Date() }
])


db.logs.createIndex({createdAt: 1}, {expireAfterSeconds: 60})


db.otps.insertMany([
  { _id: 1, phone: "+919876543210", otp: "123456", createdAt: new Date() },
  { _id: 2, phone: "+918765432109", otp: "987654", createdAt: new Date() }
])

geospatial indexes
--------------------


db.places.insertMany([
  { name: "Pizza Hut", location: { type: "Point", coordinates: [77.5946, 12.9716] } }, // Bangalore
  { name: "McDonald's", location: { type: "Point", coordinates: [78.4867, 17.3850] } }, // Hyderabad
  { name: "Starbucks", location: { type: "Point", coordinates: [72.8777, 19.0760] } }  // Mumbai
])

db.places.createIndex({location:"2dsphere"})

//within 100 km
db.places.find({
    location:{
        $near:{
            $geometry:{type: "Point", coordinates: [78.4867, 17.3850]},
            $maxDistance:100000 //100 km (in meters)
        }
    }
})

//within 10 km earth radius

db.places.find(
    {
        location:{
            $geoWithin:{
                $centerSphere:[[78.4867, 17.3850], 10/6378.1]
            }
        }
    }
)