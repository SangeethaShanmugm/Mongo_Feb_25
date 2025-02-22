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