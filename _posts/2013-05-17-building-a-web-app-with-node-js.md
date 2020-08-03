---
author: Aishwarya Singhal
comments: true
date: 2013-05-17 09:02:32+00:00
layout: post
slug: building-a-web-app-with-node-js
title: Building a web app with node js
wordpress_id: 195
tags:
- javascript
- nodejs
---

NodeJS is an event driven javascript framework that makes writing asynchronous code a piece of cake! For small apps and a limited user base, this is almost magical - the code can be churned out fast, it is clean and it is perfectly unit testable. The purpose of this blog is not to sell node js though, we'll instead look at how an application could be built easily.

The applications I work on are primarily client-server, like web apps, or mobile apps with a backend. So here's what my toolkit with node js looks like:
	
  * **Express JS**: Sinatra like web framework that gives basic structure to the web app
  * **Sequelize JS**: ORM framework
  * **Require JS**: for modularization
  * **Node DB Migrate module**: just like rails db migrations
  * **Mocha JS**: For unit tests
  * **Chai JS**: For test assertions
  * **Crypto**: For encryptions
  * **Angular JS**: For the front end
  * **MySQL**: database

Lets keep the front end out of scope for this article and only focus on getting an app that can serve JSON over REST.


### Setting up the environment

	
1. Install [nodejs](http://nodejs.org/)	
2. Next, we need [expressjs](http://expressjs.com/guide.html)
3. Run the following

    ```bash
        npm install -g express
        # create the app now. we'll call it 'myapp'
        express myapp
        cd myapp
        node app.js
    ```

4. You should now see something like this "Express server listening on port 3000"
5. Yay! You now have a basic Express JS app running!



### Configuring the app

	
  1. The [ExpressJS guide](http://expressjs.com/guide.html) is a pretty good resource for getting started, so I would recommend that you read through it.

	
  2. Next, add the following in package.json under dependencies:
     ```javascript
     {
       "mysql": "*",
       "supervisor": "*",
       "db-migrate": "*",
       "sequelize": "*",
       "requireindex": "*",
       "mocha": "*",
       "crypto": "*",
       "chai": "*"
     }
     ```

	
  3. Save package.json and run "npm install"

	
  4. Supervisor module is a great module for development environments and it auto reloads the app on change, so you dont have to restart your node server every time. To run the app using supervisor, just use "supervisor app.js"

	
  5. [Requireindex](https://github.com/stephenhandley/requireindex/) is a nice module that helps get all objects from  a directory into a single object, without adding a "require" for each file

	
  6. Add the error handler in app.js (as described in expressjs guide)

     ```javascript
     app.use(function(err, req, res, next){
       console.error(err.stack);
       res.send(500, 'Something broke!');
     });
     ```

	
  7. Run the app again and access using http://localhost:3000.




### Adding database support





	
  1. Install [mysql](http://dev.mysql.com/downloads/mysql/)

	
  2. We already have the node module included in package.json (mysql), so the app is now ready to start talking to the database

	
  3. We'll use node db migrate module to set up the database.

	
  4. Create a file database.json under myapp. The contents should look as follows:

     ```javascript
    {
      "dev": {
        "driver": "mysql",
        "user": "root",
        "database": "myapp"
      },

      "test": {
        "driver": "mysql",
        "user": "root",
        "database": "myapp_test"
      },

      "production": {
        "driver": "mysql",
        "user": "root",
        "database": "myapp"
      }
    }
     ```

	
  5. Create a db.js in the myapp directory with the following contents:

     ```javascript
     var express = require('express'),
         Sequelize = require("sequelize");

     var app = express();
     var env = app.get('env') == 'development' ? 'dev' : app.get('env');

     // db config
     var fs = require('fs');
     var dbConfigFile = __dirname + '/database.json';
     var data = fs.readFileSync(dbConfigFile, 'utf8');

     var dbConfig = JSON.parse(data)[env];
     var password = dbConfig.password ? dbConfig.password : null;
     var sequelize = new Sequelize(dbConfig.database, dbConfig.user, password, { logging: true });

     exports.sequelize = sequelize
     ```

	
  6. The above uses the same file (database.json) as used by db-migrate module so all your configuration stays at one place. It also initializes our ORM framework viz. sequelizejs.

	
  7. To use this, just add `require('db.js')` as required and get sequelize.


### Configure unit tests

	
  1. Modify your package.json and add the following under "scripts":

     ```javascript
     "pretest": "db-migrate up -m ./migrations --config ./database.json -e test",
     "test": "NODE_ENV=test mocha test test/*/**"
     ```

  2. The above will ensure that your db migrations are run automatically when you run the tests, and also that you don't have to remember longish commands for recursively running tests in sub directories.

  3. Add a basic test case under "test" directory.

     ```javascript
     var expect = require('chai').expect,
     should = require('chai').should();
     var db = require("../db.js").sequelize;
     var DataTypes = require("sequelize");
     var assert = require("assert")
     describe('DB', function(){
         it('should check db connection', function(done){
             db
             .query("select count(1) from users")
             .success(function(o){
                 expect(o.length).to.not.equal(0);
                 done();
             }).error(function(error) {
                 done();
             });
       })
     })
     ```

  4. Prepare for test data - create a file _setup.js under tests and put the following:

     ```javascript
     var db = require('../db.js').sequelize;

     var testData = [
     "INSERT INTO users (name) VALUES ('test user');",
     "INSERT INTO users (name) VALUES ('test user 2');"
     ];

     // now run the test data
     testData.forEach(function(sql){
         db.query(sql).success(function(){ }).error(function(e){ console.log(e); });
     });

     console.log(">>>> starting tests...");
     ```
	
  5. The SQLs above are obviously just indicative and you'll have to add your SQLs as needed.
	
  6. Run `npm test` to execute the tests!


### Build a model

	
  1. Start creating your db migrations (like `db-migrate create users`) ! They will be stored under myapp/migrations directory.

	
  2. Run the following:

     ```bash
     db-migrate create users
     ```

	
  3. Now open the migration that has been created under migrations directory and add table definition, e.g.

     ```javascript
     var dbm = require('db-migrate');
     var type = dbm.dataType;

     exports.up = function(db, callback) {
         db.createTable('users', {
             id: { type: 'int', primaryKey: true, autoIncrement: true },
             name: 'string'
           }, callback);
     };

     exports.down = function(db, callback) {
         db.dropTable('users', callback);
     };
     ```

	
  4. Run the migrations to create users table.

  5. Now create a directory called "models" under myapp. This is where we'll put our models.
	
  6. Under models, create `users.js` with the following contents (or similar)

     ```javascript
     var db = require("../db.js").sequelize;
     var crypto = require('crypto');
     var DataTypes = require("sequelize");

     var User = function(name, username, password) {
       this.name = name,
       this.user_name = username,
       this.password = password
     };

     var users_table = db.define('users', {
          name: DataTypes.STRING,
          user_name: DataTypes.STRING,
          password: DataTypes.STRING
        }, {
          timestamps: false,
          underscored: true
        });

     User.prototype.save=function(onSuccess, onError) {
        var shasum = crypto.createHash('sha1');
        shasum.update(this.password);
        this.password = shasum.digest('hex');

        users_table.build(this).save().success(onSuccess).error(onError);
     };

     User.find=function(username, password, onSuccess, onError) {
        users_table.find({ where: {user_name: username, password: password}, attributes: ['id', 'name', 'user_name'] }).success(onSuccess).error(onError);
     };

     User.lookup=function(name, onSuccess, onError) {
        users_table.findAll( { where : [ "name like ?", '%' + name + '%' ] } ).success(onSuccess).error(onError);
     };

     exports.get=User;
     exports.table=users_table;
     ```

	
  7. As a reminder, we use [sequelizejs](http://www.sequelizejs.com/documentation) for ORM and [crypto](http://nodejs.org/api/crypto.html) for encryptions above.

	
  8. To use this model, all we now need is to create an object of User and call `user.save()`, or directly call `User.find` or `User.lookup` as needed. Notice that these take callbacks for success and error, thats because node js is a totally event driven framework and everything is synchronous. These methods don't return anything :smile:

	
  9. Lets add a route, create user.js under routes directory.

     ```javascript
     var User = require('../models/users').get;

     exports.authenticate = function(req, res) {
       User.find(req.body.username, req.body.password, function(o) {
         if (o) {
           res.json(o.selectedValues);
         } else {
           res.send(401, "Auth failed");
         }
       }, function(error) {
         console.log(error);
         res.send("Auth failed");
       });
     };
     ```

  10. And in app.js, add the route.

      ```javascript
      app.post('/authenticate', user.authenticate);
      ```
	
  11. All done! You now have an app that can connect to the database and authenticate users!


In the next blog, we'll see how we can quickly assemble a front end
