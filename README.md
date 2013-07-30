mongoDB-tools
=============

A collection on tools used around mongoDB 

Script: mongoInitScreen
=============

## Overview

The mongoInitScreen shell script is designed to help with running your
mongo set-up in development. 

## Usage

We use it locally, on test/edge systems to run mongod replica sets
and test application behaviour when services are manipluted (e.g. take
down primary set)..

## Prerequisites

To run mongoInitScreen make sure that you have the following installed:

* [bash](http://www.gnu.org/software/bash/)
* [screen](http://www.gnu.org/software/screen/manual/screen.html)
* [mongoDB] (http://www.mongodb.org/downloads)

## Configuration, not for production

Follow [the set-up
guide] (http://docs.mongodb.org/manual/tutorial/deploy-replica-set/#deploy-a-
development-or-test-replica-set) on creating your replicate sets. At the
point of starting each mongodb instance follow this guide to allow 
Using screen sessions, create socketnames based on the port number you
are 

* Download the mongoInitScreen script to the system running mongod

``` 
$ git clone https://github.com/digitalanimal/mongoDB-tools
```

Set up screen sessions, you need a session per replica set, to look like
this:

```
$ screen -ls
There are screens on:
10459.mongo.27018(Detached)
10472.mongo.27019(Detached)
10619.mongo.27017(Attached)
```
To create a screen session use: ```$ screen -S mongo.PORT_NUMBER```

Attach to the sreen an just run the script, example:

```
$ screen -r 10472.mongo.27019

$ ./mongoDB-tools/scripts/mongoInitScreen
Checking your port out
Running mongod...
mongod --port 27019 --dbpath /srv/mongodb/rs0-2 --replSet rs0
--smallfiles --oplogSize 128 --keyFile '/srv/mongodb/keyfile'
```

Detach the screen and leave mongod running ``` CTRL-a d ```

Run ``` rs.status() ``` in mongo to see your replicate set status.

