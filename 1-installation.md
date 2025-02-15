## MongoDb

> > Database best used for unstructured data
> > Can be used for structured as well

## Terminologies

SQL Mongodb

---

Table Collection
Row Document
Column Field
Database Database
Select Find
Insert Insert
Update Update
Delete Delete/Remove
Joins Lookups
Multiple-tables Nested collection
Avoid repeation No issues with repeation

> > Flexible Schema => Shape of our data/ Table structure
> > Data store in mongodb => BSON format => BInary JSON
> > JSON => Javascript Object Notation

       {
             "name":"Jack",
             "email":"jack@gmail.com"
      }

> > [
> > {

    "Tablename": "Customers",
    "Records": 91

},
{
"Tablename": "Categories",
"Records": 8
},
{
"Tablename": "Employees",
"Records": 10
},
{
"Tablename": "OrderDetails",
"Records": 518
},
{
"Tablename": "Orders",
"Records": 196
},
{
"Tablename": "Products",
"Records": 77
},
{
"Tablename": "Shippers",
"Records": 3
},
{
"Tablename": "Suppliers",
"Records": 29
},
{
"Tablename": "Persons",
"Records": 0
}
]

> > Object  
> >  => {

             name:"Jack",
             email:"jack@gmail.com"
      }

> > Why not json? => occupy more space
> > Store => BSON
> > Retrieve => JSON
> > Embedded document =>how many levels of nested document is possible in single document? => { } => 100 levels of nesting => 16 mb = 10,000 lines of text

https://www.mongodb.com/try/download/community

## Windows

> > Create one folder in c drive by the name of data
> > C:/data
> > Inside data create folder by the name of db
> > C:/data/db

## mac/Linux

> > Open terminal
> > mkdir data/db

> > Server
> > Which start mongodb
> > should always be running if using database
> > Shell
> > command line tool
> > use to verify the query

> > mongo --version => to check version
> > mongod => Kickstart the mongo server => mongo server
> > open cmd in start => mongod
> > mongo => take you to shell => mongo client
> > open cmd in start => mongo

> > https://stackoverflow.com/questions/51224959/mongo-is-not-recognized-as-an-internal-or-external-command-operable-program-o

default port => 27017

# Mac/Linux

Step to run mongodb server

> open terminal
> mongod --dbpath data/db

Step to run mongodb client

> open terminal
> mongo
