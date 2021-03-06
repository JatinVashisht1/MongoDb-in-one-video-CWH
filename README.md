
## Some points about MongoDb:

1. MongoDb does not give a fuck about schema, unlike relational db.
2. It stores object as BSON (not JSON), which gives extra features
3. It gives a unique id to each object by itself
4. Its commands are very intuitive
5. We can also control db. operations through its gui i.e MongoDBCompass.


## Database commands 🔥

View all databases:
show dbs

to make new database/switch to another database:
use dbname

to know which database we are currently working with:
db

drop database:
db.dropDatabase()

-------

## Collection commands 🔥

collection equivalent to table of SQL

To view all collections of database:

show collections

To create a new collection named 'comments:

db.createCollection('comments')

To delete a collection name 'content':

db.content.drop()

-------

## Document commands 🔥

Document is equivalent to row of SQL

To insert "ONE" document:

db.comments.insert({'name':'Harry', 'lang':'JavaScript', 'member_since':5})

To insert "MANY" documents:

db.comments.insertMany([{'name':'Nitin', 'lang':'JavaScript', 'member_since':5}, {'name':'Jatin', 'lang':'Kotlin', 'member_since':2}])

To view all documents and fields(columns) in a collection:

db.database_name.find() 

db.database_name.find().pretty() [to visualise collection clearly 🙂] 

To insert date we can make an object of Date class

this feature is provided by BSON and is not present in JSON!

db.comments.insert({'name':'Harry', 'lang':'JavaScript', 'member_since':5, 'date': new Date()})

-------

## Search in MongoDb database 🔥

Searching with conditions:

db.comments.find({lang:'Kotlin', name: 'Jatin'})

Limiting results:

db.comments.find({lang:'Kotlin', name: 'Jatin'}).pretty().limit(1)

(we can see that after find we applied pretty function 

and after that we applied limit function

this process is called chaining)

To see the count of number of outputs:

db.find().count()

db.comments.find().limit(1).count()

(this will not limit the count to 1,

but it will show the original count in the database)

db.comments.find({name: 'Jatin'}).count()

(this will take the condition in account,

and will show the number of rows with name 'Jatin')

To find only one element:

db.comments.findOne({name:'Jatin'})

-------

## Sorting commands 🔥

1. to sort in ascending order
2. to sort in descending order


db.comments.find().sort({name:-1}).pretty()

-------

## Updating a row 🔥

db.comments.update({name: 'Harry'}, {
    'name': 'Harry',
    'lang': 'Cpp',
    'member_since':6
})

upsert means if it have to insert something while updating
(to enable upsertion we have to tell mongodb explicitly):

db.comments.update(
    {name:'Harry22'},
    {'name':'Harry', 'lang':'Cpp', 'member_since':69}, 
    {upsert:true}
    )

-------

## Update operators in MongoDB 🔥

Increment:

db.comments.update(
    {name:'Jatin'},
    {
        $inc:{
        member_since: 2
    }})


Rename:

// renames the fields

db.comments.update(
    {name:'Jatin'},
    {
        $rename:{
        member_since: 'member'
    }})

Delete Row:

db.comments.remove({name:'Jatin'})

Less than

db.comments.find({member_since: {$lt: 10}})

// similarly

// gt: greater than

// gte: greater than equals to

// lte: less than equals to

