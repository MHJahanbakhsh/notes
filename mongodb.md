## mongodb commands:
* `use <database name>` if database is not existed, will create one and switch to it;otherwise will switch to already existed database
* `show databases` to show all data bases.note that newly created database with no collection inside it and will not be visible with this command,untill you put some collections in it.
* `db.dropDatabase()` to delete the database that you are currently in
* `db` shows which database you are currently in
* `db.createCollection(<name of collection> , options)` to create a new collection
* `db.collection.drop()` to delete a collection
