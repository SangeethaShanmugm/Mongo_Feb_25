> List of city
> Relationship between city & rest
> Meal Type
> Meal Type + rest + cost + cuisine

Table - 4
Restaurants
City
Cuisine
MealType

Restaurants

Rest Id | RestName | Cost | CityId | MealId | CuisineId

[
{
"\_id":323423,
"rest_id":1,
"rest_name":"Ama Cafe",
"city_id":1,
"cost":450,
"rating_text":"Very Good",
"rating":4.5,
"Cuisine":[
{
"cuisineid":1,
"cuisineName":"North India"
},
{
"cuisineid":2,
"cuisineName":"English Breakfast"
},
{
"cuisineid":3,
"cuisineName":"Tibetan"
}
],
"mealTypes":[
{
"mealId":1,
"mealName":"BreakFast"
},
{
"mealId":2,
"mealName":"Lunch"
},
]
},
{
"\_id":323422,
"rest_id":2,
"rest_name":"Punjabi Grills",
"city_id":2,
"cost":950,
"rating_text":"Good",
"rating":4.1,
"Cuisine":[
{
"cuisineid":1,
"cuisineName":"North India"
},
{
"cuisineid":4,
"cuisineName":"South Indian"
}
],
"mealTypes":[
{
"mealId":1,
"mealName":"BreakFast",
"menu":[
{
"type":"Veg",
"items":["Panner","Dal"]
},
{
"type":"Non-Veg",
"items":["Chicken","Mutton"]
}
]
},
{
"mealId":2,
"mealName":"Lunch"
},
{
"mealId":3,
"mealName":"Dinner"
}
]

    }

]

collection-2
City

[
{
_id:1,
name:"Delhi"
}
{
_id:2,
name:"Bangalore"
}
]

## movies

[
{
id: 1,
mname:"Avengers",
poster:"https://m.media-amazon.com/images/M/MV5BNDYxNjQyMjAtNTdiOS00NGYwLWFmNTAtNThmYjU5ZGI2YTI1XkEyXkFqcGdeQXVyMTMxODk2OTU@._V1_.jpg",
rating:8,
description:"Earth's Mightiest Heroes stand as the planet's first line of defense against the most powerful threats in the universe. The Avengers began as a group of extraordinary individuals who were assembled to defeat Loki and his Chitauri army in New York City.",
trailer:"https://www.youtube.com/watch?v=hA6hldpSTF8"
}
]

# to see all db's

> > show dbs

# Go inside Db

use dbName

# to show all collections

show collections

# to find the record

> db.collectionname.find().pretty()

# create a new db

use dbName

# insert into mongodb

db.users.insert({"name":"Aishwarya", "city":"Delhi"})
db.users.insert({"name":"Alok", "city":"Mumbai"})
db.users.insert({\_id:1, "name":"Ankur", "city":"Pune"})
db.users.insert({\_id:2,"name":"Ashok", "city":"Hyderabad"})

db.users.find().pretty()

# Object ID

A 4-byte timestamp, measured in seconds

A 5-byte random value generated once per process. This random value is unique to the machine and process.

A 3-byte incrementing counter, initialized to a random value.

ObjectId("00000020f51bb4362eee2a4d")

A four byte time stamp, 00000020

A five byte random element, f51bb4362e

A three byte counter, ee2a4d

> > 64fdefd68105d59859fa0588

64fdefd68105d59859fa0588 => 12 bytes

_id => primary key
12 bytes
5 bytes => Series
4 bytes => timestamp
3 byte => random number

# Add series for \_id

db.counters.insert({
"\_id":"cityId",
"sequence_value":0
})

    function generateSeries(sequenceName){
        var sequenceDocument = db.counters.findAndModify({
            query:{_id: sequenceName},
            update:{$inc: {sequence_value: 10}},
            new: true
        })
        return sequenceDocument.sequence_value
    }


    db.city.insert({
        "_id":generateSeries("cityId"),
        "name":"Delhi",
        "country":"India"
    })

       db.city.insert({
        "_id":generateSeries("cityId"),
        "name":"Paris",
        "country":"France"
    })

     db.city.insert({
        "_id":generateSeries("cityId"),
        "name":"Helsinki",
        "country":"Finland"
    })

# Embedded document

> > One to One
> > {

    _id:ObjectId("43546"),
    name:"jack",
    job:"Developer",
    address:{
        street: "876 test street",
        city:"New York",
        pobox:77455
    }

}

> > one to Many

{
\_id:ObjectId("43546"),
name:"jack",
job:"Developer",
address:[
{
street: "876 test street",
city:"New York",
pobox:77455,
type:"Permanent"
},
{
street: "876 test street",
city:"London",
pobox:77455,
type:"Temporary"
}
]

}

# Remove/ Delete

# delete records

db.users.deleteOne({\_id: "64fdefd68105d59859fa0588" }) ❌

db.users.deleteOne({"\_id": ObjectId("64fdefd68105d59859fa0588") }) ✅

# delete collection

db.users.drop()

//use dbName
db.dropDatabase()
