# Usage

Clone the repo 

```
git clone https://github.com/robinagandhi/datascience
```

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

Open a new terminal in Jupyter

```
conda install pymongo

#inspect the link for MongoDB
#and record the container name
cat /etc/hosts

#inspect the environment
env | grep DATASCIENCE

```

Use the connection strings available above to connect using mongo client in your python code.

```
#Function to connect to MongoDB Containter
def get_db():
    from pymongo import MongoClient
    client = MongoClient('datascience_db_1:27017')
    db = client.testDB
    return db

```
Load the sample notebooks available into Jupyter and check for errors.

Hit `control+c` to gracefully shutdown the containers when done.

## Password protecting Jupyter Notebooks
- [Instructions](http://jupyter-notebook.readthedocs.io/en/latest/public_server.html)

