# Usage

Clone the repo 

```
git clone https://github.com/robinagandhi/datascience
```

Make sure docker is installed and running.

Create a named docker volume. Use the name "sciencedata" as shown below.

```
docker volume create --name=sciencedata 
```

Make sure Docker has permission to write to your drives. You can adjust this in your preferences for Mac and Windows docker settings.

Now navigate into the project directory and issue the following command:

```
docker-compose up
```

Copy the authenticated token URL from the terminal and browse to it. 

Your notebook is ready to use!

If you want to connect with MongoDB using Python then follow the rest of the steps here.

Open a new terminal in Jupyter to install pymongo to interact with MongoDB. 

```
conda install pymongo

#inspect the link for MongoDB
#and record the container name
cat /etc/hosts

#inspect the environment
env | grep DATASCIENCE

```
If you have your own mongodb instance then use the code below in a notebook to connect to it. 

```
import pymongo
from pymongo import MongoClient
dbConnectionString = "<<mongo connection string here>>"
client = MongoClient(dbConnectionString)

``` 

If you want to use just a **test** mongodb instance then continue with the instructions here.

```
import pymongo
from pymongo import MongoClient
client = MongoClient('datascience_db_1:27017')

```
Load the sample notebooks available into Jupyter and check for errors.

Hit `control+c` in the terminal to gracefully shutdown the containers when done.

