$match
> It is used for filtering documents(condition)
 $project
> It will select some specific fields from a collection
$group
> It is used to group documents on basis of some values
 $sort
> Its used to sort data 
$skip
> skip number of documents
 $limit
> To retrieve number of documents
$unwind
> Deconstructs an array, like flat the array
>$out
> It is to write the document output

## Accumulator

 
count
avg
min
max
first
last


db.students.aggregate([
{
    $match: {"sec": "A"}
},
{
    $count: "Total Number of Students in Sec A"
}

])

//group

db.students.aggregate([
    {
        $group:{
            _id: "$sec",
            total_st:{ $sum: 1},
            max_age:{ $max :"$age"}
        }
    }
])


{ "_id" : "B", "total_st" : 3, "max_age" : 40 }
{ "_id" : "A", "total_st" : 4, "max_age" : 37 }


db.students.aggregate([
   {
    $sort:{age: 1}
   },
   {
    $limit:2
   }
]).pretty()




db.students.aggregate([
   {
    $unwind: "$subject"
   }
]).pretty()

db.employees.find().pretty()

db.employees.aggregate([
    {
        $match: {"gender":"female"}
    }
])


//group employee based on department

db.employees.aggregate([
    {
        $group:{
            _id:"$department.name",
            totalEmp:{$sum: 1}
        }
    }
])

//avg salary

db.employees.aggregate([
    {
        $match:{"gender": "male"}
    },
    {
        $group:{
            _id:"$department.name",
            totalEmp:{$sum: 1},
            totalSalary:{$avg: "$salary"}
        }
    },
    {
        $sort: {"_id":1}
    }
])
    

db.products.insertMany([
    {_id:0, productName:"Steel Beam", status:"new", quantity: 10},
    {_id:1, productName:"Steel Beam", status:"urgent", quantity: 20},
    {_id:2, productName:"Steel Beam", status:"urgent", quantity: 30},
    {_id:3, productName:"Iron Rod", status:"new", quantity: 15},
    {_id:4, productName:"Iron Rod", status:"urgent", quantity: 50},
    {_id:5, productName:"Iron Rod", status:"urgent", quantity: 10}
])     

db.products.find().pretty()


//select sum(quantity) from products where status="urgent" groupby productName
//group by productName

//stage - 1

db.products.aggregate([
    {
        $match: { status:"urgent"}
    }
])


//stage - 2

//$group, $sum

db.products.aggregate([
    {
        $match: { status:"urgent"}
    },
    {
        $group:{
            _id:"$productName",
            totalUrgentQuantity:{$sum:"$quantity"}
        }
    }
])





