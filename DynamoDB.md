# AWS DynamoDB:

### Overview:

- Partition key: (primary key) unique, acting as data object identifier. ie. id, primary keys could require partition key and sort key. such as id and timestamp.
- attributes: fields of each data object. ie. firstName, lastName.
- one database per region, different data sets are organized by different tables within the same database.

### DynamoDB capabilities:

- can act as event source to trigger lambda functions.
- can act as data source from lambda functions.

### creating database and API hook up:

- input name, region, and config usage provisions.
- item tab: edit tables to add, delete, duplicate or edit.
- metrics tab: shows performance and trouble shooting errors.
- alarm tab: set up event alarms to alert admin of events.
- capacity tab: edits provisioned capacity and adjust payment tier.
- access control tab: control accessibility of the database.

### creating and scanning items/entries to table:

- select create item
- click plus icon to add new fields, specify data type and input value.
- all fields except primary key field can be added and removed.
- scanning can take in filters of multiple items.
- can also use query methods to search table objects.

### accessing database from lambda

- go to lambda and choose the function to access database from.
- import dynamo service: at top, outside of the lambda function code.
  const AWS = require('aws-sdk');
  const dynamodb = new AWS.DynamoDB({region:'use-east-2', apiVersion: '2012-08-10'});
- write code logic (refer to lambda function examples.)
- change role permissions by going to IAM for user settings > roles > choose the correct roles. attach a new prebuilt policy that allows dynamoDB full access.
