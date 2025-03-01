db.orders.insert([
{"_id": 1, "item":"almonds","price":12,"quantity":2},
{"_id": 2, "item":"pecans","price":20,"quantity":1},
{"_id":3}
])

db.orders.find().pretty()

db.inventory.insert([
{"_id": 1, "sku":"almonds","description":"product 1","instock":120},
{"_id": 2, "sku":"bread","description":"product 2","instock":80},
{"_id": 3, "sku":"cashews","description":"product 3","instock":120},
{"_id": 4, "sku":"pecans","description":"product 4","instock":60},
{"_id": 5, "sku": null,"description":"Incomplete","instock":70},
{"_id": 6}
])

db.inventory.find().pretty()

db.orders.aggregate([
    {
        $lookup:
        {
            from:"inventory",
            localField:"item",
            foreignField:"sku",
            as: "combine_data"
        }
    },
    {
        $project:{_id: 1, item: 1, stock_name: "$combine_data.sku", stock:"$combine_data.instock" }
    }
]).pretty()




db.inventory.aggregate([
    {
        $lookup:
        {
            from:"orders",
            localField:"sku",
            foreignField:"item",
            as: "combine_data"
        }
    },
    {
        $project:{_id: 1, sku: 1, stock_name: "$combine_data.item", stock:"$combine_data.quantity" }
    }
]).pretty()




db.classes.insert( [                                     6            5          1
  { _id: 1, title: "Reading is ...", enrollmentlist: [ "giraffe2", "pandabear", "artie" ], days: ["M", "W", "F"] },                                                3            1 
  { _id: 2, title: "But Writing ...", enrollmentlist: [ "giraffe1", "artie" ], days: ["T", "F"] } ])


db.classes.find().pretty()


db.members.insert( [
   { _id: 1, name: "artie", joined: new Date("2016-05-01"), status: "A" }, 
   { _id: 2, name: "giraffe", joined: new Date("2017-05-01"), status: "D" }, 
   { _id: 3, name: "giraffe1", joined: new Date("2017-10-01"), status: "A" }, 
   { _id: 4, name: "panda", joined: new Date("2018-10-11"), status: "A" }, 
   { _id: 5, name: "pandabear", joined: new Date("2018-12-01"), status: "A" }, 
   { _id: 6, name: "giraffe2", joined: new Date("2018-12-01"), status: "D" } 
])


db.members.find().pretty()




db.classes.aggregate([
    {
        $lookup:
        {
            from:"members",
            localField:"enrollmentlist",
            foreignField:"name",
            as:"student_info"
        }
    }
]).pretty()