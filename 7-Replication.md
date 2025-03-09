## Scaling

> > Horizontal Scaling => adding more machines
> > Vertical scaling => adding more memory of RAM

replication => repeating same data in machines

1 primary - 2 secondary

//Mac/Linux

c:/data

mkdir data/rs1
mkdir data/rs2
mkdir data/rs3

mongod --port 2001 --dbpath c:\data\rs1 --replSet --sangeetha --oplogSize 128

mongod --port 2002 --dbpath c:\data\rs2 --replSet --sangeetha --oplogSize 128

mongod --port 2003 --dbpath c:\data\rs3 --replSet --sangeetha --oplogSize 128

> mongo --port 2001

> mongo --port 2002

> mongo --port 2003

rs.help()
rs.status() => no replset config has been received

rs.initiate() => to make a machine primary
rs.add("127.0.0.1:2002") => add machine as secondary
rs.add("127.0.0.1:2003") => add machine as secondary


Add priority
--------------

rs.add({_id:4, host:"localhost:27017", priority: 1 })

rs.add({_id:4, host:"localhost:27017", priority: 1, hidden: true})


db.first.insert({"name":"John"})

//Run over secondary  to allow Replication 


db.getMongo().setSlaveOk() | db.getMongo().setSecondaryOk()

//to add Arbiter

rs.addArb("SANGEETHA:3001")
rs.addArb("localhost:3001", true)
rs.remove() => remove any machine