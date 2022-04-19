## mongodb commands:
* `use <database name>` if database is not existed, will create one and switch to it;otherwise will switch to already existed database
* `show databases` to show all data bases.note that newly created database with no collection inside it and will not be visible with this command,untill you put some collections in it.
* `db.dropDatabase()` to delete the database that you are currently in
* `db` shows which database you are currently in
* `db.createCollection(<name of collection> , options)` to create a new collection
* `db.<collection name>.drop()` to delete a collection
----
each docmuent in mongodb has a unique __id__ that is automatically generated.( _id ). it has 24 charchter    

---
### what is BSON and how it differs from JSON?
as we already know JSON is supported by most languages and is easy to parse and render.but it has some limitations    
BSON(binary encoded json) is an extended version of JSON that supprorts some additional mongodb datatypes that JSON doesn't such as : date , timestamp , objectId.    
BSON is exclusively in mongodb    