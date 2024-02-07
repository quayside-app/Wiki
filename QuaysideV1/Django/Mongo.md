# Setting Mongo with Django

**2/6/2024 • Mya Schroder**

Django has a built in ORM (Object Relational Manager). However, it is designed for SQL-like databases and doesn't work with MongoDB. This means features like the Admin Panel won't work. However, there are 3 library options for using Mongo with Django (aka Python):

1. Djongo
    * Attempts to map Mongo to Django's built in ORM.
    * Not supported any more and does not work with recent versions of Django.

2. Pymongo
    * Low level MongoDB  driver.
    * Officially supported by MongoDB.

3. MongoEngine
    * Built off of Pymongo to be higher level. 
    * Enforces schemas and data integrity.

I decided to go with MongoEngine because it is currently supported and enforces data integrity.

Citations: <br>
[Read This Before Using Django With MongoDB](https://www.mongodb.com/compatibility/mongodb-and-django) <br>
[How to Use Django with MongoDB](https://www.mongodb.com/compatibility/mongodb-and-django)