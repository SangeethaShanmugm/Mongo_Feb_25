db.books.insert([
{
"name": "Charlotte's web",
"poster": "https://cdn.britannica.com/64/103064-050-295C6879/Charlottes-Web-EB-Garth-Williams.jpg",
"rating": 8.8,
"summary": "The novel tells the story of a livestock pig named Wilbur and his friendship with a barn spider named Charlotte. When Wilbur is in danger of being slaughtered by the farmer, Charlotte writes messages praising Wilbur in her web in order to persuade the farmer to let him live."
},
{
"name": "The power of your subconscious mind",
"poster": "https://kbimages1-a.akamaihd.net/6f3cf06c-4811-42d4-bd63-564c8264bc2d/1200/1200/False/the-power-of-your-subconscious-mind-57.jpg",
"rating": 7,
"summary": "Your subconscious mind is a powerful force to be reckoned with. It makes up around 95% of your brain power and handles everything your body needs to function properly, from eating and breathing to digesting and making memories"
},
{
"name": "Attitude is everything ",
"poster": "https://miro.medium.com/max/1400/1*ItFOYfi8Dyy0yj9n1SE8uQ.jpeg",
"rating": 8.1,
"summary": "Attitude, In psychology, a mental position with regard to a fact or state. Attitudes reflect a tendency to classify objects and events and to react to them with some consistency. Attitudes are not directly observable but rather are inferred from the objective, evaluative responses a person makes."
},
{
"name": "The Secret",
"poster": "https://m.media-amazon.com/images/I/81fdQIY6ykL.jpg",
"summary": "There's no secret to The Secret. The book and movie simply state that your thoughts control the universe. Through this “law of attraction” you “manifest” your desires. “It is exactly like placing an order from a catalogue",
"rating": 8.8
},
{
"name": "Discover Your Destiny",
"rating": 6,
"summary": "'Discover Your Destiny' is a story about enlightenment of Dar Sanderson, who is an incredibly ambitious executive. The book throws light on the fact that 'happiness and harmony can never be achieved and assured by SUCCESS'. Dar is an achiever in almost every aspect of life, yet he is void from the inside.",
"poster": "https://m.media-amazon.com/images/I/61t18yWH5qL.jpg"
},
{
"name": "The 5 AM Club",
"poster": "https://m.media-amazon.com/images/I/71zytzrg6lL.jpg",
"rating": 8.6,
"summary": "In The 5 AM Club: Own Your Morning. Elevate Your Life, he uses a fictitious story about a billionaire mentor teaching a struggling artist and an entrepreneur about the importance of waking up early to show how revolutionary it is for success."
},
{
"name": "Atomic Habits",
"poster": "https://m.media-amazon.com/images/I/91bYsX41DVL.jpg",
"rating": 8,
"summary": "Atomic Habits is the definitive guide to breaking bad behaviors and adopting good ones in four steps, showing you how small, incremental, everyday routines compound into massive, positive change over time."
},
{
"name": "I Can Do It",
"poster": "https://images-na.ssl-images-amazon.com/images/I/81T3L1yTJwL.jpg",
"rating": 8,
"summary": "Hay shows you that you “can do, change and improve virtually every aspect of your life—by understanding and using affirmations correctly. Louise explains that every thought you think and every word you speak is an affirmation. Even your self-talk, your internal dialogue, is a stream of affirmations"
}
])

//display all book info

db.books.find().pretty()

//delete "I Can Do It" book

db.books.findOne({name: "I Can Do It"})

db.books.deleteOne({name: "I Can Do It"})

db.books.insertOne(
{
"name": "I Can Do It",
"poster": "https://images-na.ssl-images-amazon.com/images/I/81T3L1yTJwL.jpg",
"rating": 8,
"summary": "Hay shows you that you “can do, change and improve virtually every aspect of your life—by understanding and using affirmations correctly. Louise explains that every thought you think and every word you speak is an affirmation. Even your self-talk, your internal dialogue, is a stream of affirmations"
}
)

db.books.find({name: "I Can Do It"}).pretty()

db.books.count()

//Restaurant data CRUD

db.restaurant.find().pretty()

//condition => query operator

db.restaurant.find({condition}).pretty()

db.restaurant.find({cost: {$gt: 1000}}).pretty()

//get "restaurant_name" : "Burger King"

db.restaurant.find({restaurant_name: {$eq: "Burger King"}}).pretty()

//projection

> > inclusion => 1

db.restaurant.find({condition}, {projection}).pretty()

db.restaurant.find({cost: {$gt: 1000}}, {restaurant_name: 1, average_rating: 1, cost: 1}).pretty()

> > exclusion => 0

db.restaurant.find({cost: {$gt: 1000}}, {restaurant_name: 0, average_rating: 0, cost: 0}).pretty()

> > inclusion + exclusion ❌

db.restaurant.find({cost: {$gt: 1000}}, {restaurant_name: 1, average_rating: 1, cost: 0}).pretty()

> > ignore \_id

db.restaurant.find({cost: {$gt: 1000}}, {\_id: 0, restaurant_name: 1, average_rating: 1, cost: 1}).pretty()

// gt & lt => 500 - 1000

db.restaurant.find({cost: {$gt: 500, $lt: 1000}}, {restaurant_name: 1, cost: 1}).pretty()

// $or || $and

db.restaurant.find(
{$or: [ {cost: {$gt: 500, $lt: 1000}}, {cost: {$gt: 2000, $lt: 2500}} ]},
{restaurant_name: 1, cost: 1}
).pretty()

// in & nin
db.restaurant.find().pretty()

db.restaurant.find(
{"mealTypes.mealtype_name": { $in: ["Breakfast", "Drinks","Lunch"]} },
{restaurant_name: 1, cost: 1, mealTypes: 1}
).pretty()

10 mins
//nin => Breakfast, Lunch, Dinner

db.restaurant.find(
{"mealTypes.mealtype_name": { $nin: ["Breakfast", "Dinner","Lunch"]} },
{restaurant_name: 1, cost: 1, mealTypes: 1}
).pretty()

//and => "mealTypes.mealtype_id": 4, "mealTypes.mealtype_id": 5

db.restaurant.find(
{$and: [{"mealTypes.mealtype_id": 4},{"mealTypes.mealtype_id": 5} ]},
{restaurant_name: 1, cost: 1,mealTypes: 1}
).pretty()

//sorting

//asc = 1
db.restaurant.find({},{restaurant_name: 1, cost: 1}).sort({cost: 1}).pretty()

//desc = -1
db.restaurant.find({},{restaurant_name: 1, cost: 1}).sort({cost: -1}).pretty()

//limit
db.restaurant.find({},{restaurant_name: 1, cost: 1}).sort({restaurant_name: -1}).limit(5).pretty()

//skip

db.restaurant.find({},{restaurant_name: 1, cost: 1}).sort({restaurant_name: 1}).limit(5).skip(5).pretty()
