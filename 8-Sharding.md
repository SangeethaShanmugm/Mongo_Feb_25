Sharding => Horizontal Scaling

## Hashed Sharding

if shard have an empty collection => create a two empty chunks/shard

hashed index => \_id

## Ranged Sharding

minkey .... maxkey

document => \_id => counter increment => shard key

balancer = >background processor
=> monitor no of chunks / shard

1 -> 3 shards(3 directories to store datafiles)
2 -> 3 config server(3 directories to store datafiles)
3 -> 1 query router(mongos)

//Shards

mkdir/shard1
mkdir/shard2
mkdir/shard3

mongod --shardsvr --port 2001 --replSet rs1 --dbpath data\shard1

mongod --shardsvr --port 2002 --replSet rs1 --dbpath data\shard2

mongod --shardsvr --port 2003 --replSet rs1 --dbpath data\shard3

mkdir/config1
mkdir/config2
mkdir/config3

//config server

mongod --configsvr --dbpath /data/config1 --port 2011 --replSet rs0

mongod --configsvr --dbpath /data/config2 --port 2012 --replSet rs0

mongod --configsvr --dbpath /data/config3 --port 2013 --replSet rs0

mongo --port 2011

mongo --port 2012

mongo --port 2013


rs.initiate(
    {
        _id:"rs0",
        members:[
            {_id: 0, host: "localhost:2011"},
            {_id: 1, host: "localhost:2012"},
            {_id: 2, host: "localhost:2013"},
        ]
    }
)

//query router => new mongod server

mongos --configdb "rs0/localhost:2011,localhost:2012,localhost:2013" --logpath log.mongos0 --port 27200

//connecting to mongos

mongo --port 27200

//Add shards

sh.addShard("rs1/localhost:2001")
sh.addShard("localhost:2002")
sh.addShard("localhost:2003")

sh.addShard("rs1/localhost:2001, rs1/localhost:2002, rs1/localhost:2003")