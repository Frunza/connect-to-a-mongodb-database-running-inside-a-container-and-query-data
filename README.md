# Connect to a MongoDB database running inside a container and query data

## Scenario

If you have a running container with a `MongoDB` database how can you query some data?

## Solution

Let's assume that your container is named *myContainer*.

1) Access the container
To access the running container, run the following command:
```sh
docker exec -it myContainer /bin/sh
```

Now you need to install appropriate tools that allow you to query the `MongoDB` database.

2) Add MongoDB GPG Key
Ensures the MongoDB package's integrity and authenticity by importing the GPG key with the following command:
```sh
wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | apt-key add -
```
This step is necessary for securely installing MongoDB packages from the official repository.

3) Add the MongoDB Repository
Run the following command:
```sh
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/debian buster/mongodb-org/4.4 main" | tee /etc/apt/sources.list.d/mongodb-org-4.4.list
```

4) Update the Package Index
```sh
apt-get update
```
This ensures that the `MongoDB` packages can be located and installed.

5) Install the MongoDB Shell
Installs the MongoDB shell in the container:
```sh
apt-get update
```

6) Connect to the MongoDB Instance
Open a connection to the `MongoDB` database running on port 3001 within the container. This is the default for `Meteor`, for example, but your application might run on another port. Run the following command:
```sh
mongo --port 3001
```

7) Switch to your database
Connect to your database. for a `Meteor` application, the database is called  `meteor`. Its name might be different for other cases. Run the following command:
```sh
use meteor
```

8) List the available collections
Displays all collections (similar to tables in relational databases) in the selected database:
```sh
show collections
```

9) Query a collection
Query all documents in the `customers` collection, for example, and format them for readability.
```sh
db.customers.find().pretty()
```
`.find()` fetches all documents in the collection.
`.pretty()` formats the output for easier reading.
