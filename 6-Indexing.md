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