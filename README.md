# Bluemix buildpack for Meteor

## Supported version

This buildpack is dedicated for use with Meteor 1.0+.

## Usage

* Create Meteor application

```
$ meteor create testmeteor
testmeteor: created.

To run your new app:
   cd testmeteor
   meteor
```
* Run and test the application in your local until all functions are stistisfied

* Since Bluemix planed to remove the MongoLab service around end of January 2016. It is recommended to
create mongodb instance from MongoLab as the link https://mongolab.com. You need to subscribe if you haven't done so. Then follow the steps below.

* Click "Create new" button to create mongo database
![CreateNewMongoDB](/docs/CreateNewMongoDB.png)

* Select "Single-node" > Sabdard Line as "Sandbox"
![SelectPlan](/docs/SelectFreePlan.png)

* Set database name and click "Create new MongoDB deployment"
![NameDatabase](/docs/NameDatabase.png)

* Click on the new created database
![NewDatabaseCreated](/docs/NewDatabaseCreated.png)

* Copy the mongodb URI to use in later step
![MongoDBURI](/docs/MongoDBURI.png)

* Click "Users" tab and add new user and password. It can be the same as you login user and password.
![AddDatabaseUser](/docs/AddDatabaseUser.png)

* In Bluemix console, create "Mongo by Compose" service and supply the MongoDB URI in the host field for the other fields you can supply any values.
![MongoByCompose](/docs/MongoByCompose.png)


* Create manifest.yml and put it under the testmeteor folder.
Here is the sample yml.

```
---
applications:
- memory: 1GB
  domain: mybluemix.net
  path: .
  buildpack: https://github.com/bancha001/bluemix-buildpack-meteor
  host: testmeteor
  name: testmeteor
  disk: 512M
  services:
    - MongoLab-4d
  instances: 1
```

* Create .cfignore to exclude the path 'local' to be uploaded

```
.meteor/local
```

* In testmeteor/.meteor folder, open the platforms file then remove the ios and android entries (if there exist)

* Under testmeter, Run

```
cf push

```
