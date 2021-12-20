# Sequelize

## tl;dr

1. set up config and create database<br>
   @ npx sequelize init  
   @ npx sequelize db:create

2. create migration files<br>
   @ npx sequelize migration:generate --name <filename>

3. execute migration<br>
   @ npx sequelize db:migrate

4. create individual model files for ea table in database

5. set up /models/index.js by importing individual model files here

- _all steps above, i.e. all sequelize set-up files, use CJS module format (.js) for consistency_<br>
- _only from below use ESM module format (.mjs)_

6. voila! set-up is complete, can start using sequelize to manipulate database

which begs the question, why not just ESM module format all the way??<br>
read somewhere ESM plays well w CJS modules but not vice versa... i.e. poss to import CSJ modules into ESM script but diff to import ESM modules into CJS script<br>
think ESM is relatively new and sequelize cli has been ard for awhile, so prob sequelize cli is written in CJS format<br>
and so config and migration files need to be CJS modules so they can be used by sequelize cli<br>
whereas sequelize itself has been upgraded to play w ESM modules? hence model files can be ESM format...<br>
(https://stackoverflow.com/questions/62121277/using-sequelize-cli-in-node-14-with-type-module)

## Setting up

ref - https://github.com/sequelize/cli#usage

1. Optional: create .env file with DB_HOST, DB_USERNAME, DB_PASSWORD variables

2. `npx sequelize init`
   => creates
   /config/config.json
   /migrations
   /models/ index.js
   /seeders
