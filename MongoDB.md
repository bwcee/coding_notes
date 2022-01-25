# MongoDB/ Mongoose

## MongoDB

1. [Get started with databases on Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-database)
2. [how to completely remove mongoDB with all instance from ubuntu](https://stackoverflow.com/questions/57199607/how-to-completely-remove-mongodb-with-all-instance-from-ubuntu)
3. [How do I remove old mongo tools?](https://askubuntu.com/questions/1348289/how-do-i-remove-old-mongo-tools)
4. [how can I see what ports mongo is listening on from mongo shell?](https://stackoverflow.com/questions/9346431/how-can-i-see-what-ports-mongo-is-listening-on-from-mongo-shell)
   `sudo lsof -iTCP -sTCP:LISTEN | grep mongo` This is result for mongodb running on my local computer: mongod 92 mongodb 12u IPv4 16464 0t0 TCP localhost:27017 (LISTEN)
5. [How do I see what packages are installed on Ubuntu Linux?](https://www.cyberciti.biz/faq/apt-get-list-packages-are-installed-on-ubuntu-linux/)

### Data Modelling

1. [Data Modeling Introduction](https://docs.mongodb.com/manual/core/data-modeling-introduction/#data-modeling-introduction) See section on Data Model Examples and Patterns -> Helpful explanation on how to think about relationships between collections

## Mongoose

1. [Express Tutorial Part 3: Using a Database (with Mongoose)](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/mongoose) Altho MDN web docs is THE ref, found this not so straightfwd
2. [Connect MongoDB to Node using Express and Mongoose](https://javascript.plainenglish.io/connect-mongodb-to-node-using-express-and-mongoose-c405d1158c) Has examples of using Postman
3. [How to use express with mongoose](https://kb.objectrocket.com/mongo-db/how-to-use-express-with-mongoose-1003) This seems to be the most straight fwd...
4. [Creating the User Model](https://thinkster.io/tutorials/node-json-api/creating-the-user-model) Building User model w some validation and password authentication
5. [How to Seed MongoDB Database From Node: The Simplest Way](https://javascript.plainenglish.io/seeding-mongodb-database-from-node-the-simplest-way-3d6a0c1c4668)
6. [Mongoose order of methods](https://www.codeproject.com/Questions/5260095/Mongoose-order-of-methods)

### Referencing how-to

1. [Referencing another schema in Mongoose](https://stackoverflow.com/questions/18001478/referencing-another-schema-in-mongoose)

2. [Building query using chaining syntax](https://mongoosejs.com/docs/queries.html) See the section under Executing
