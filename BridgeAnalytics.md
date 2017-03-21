
# Jupyter and MongoDB Test with Docker Compose 


```python
#Import modules
import json
import random
import pprint

#Function to connect to MongoDB Containter
def get_db():
    from pymongo import MongoClient
    client = MongoClient('datascience_db_1:27017')
    db = client.testDB
    return db

#Function to add cracks to MongoDB
def add_crack(db):
    for i in range (1, 10000):
        crack = {}
        crack['crack'] = "crack" + str(i)
        crack['width'] = round(random.random(),2)
        db.cracks.insert_one(crack)

#Function to return cracks in MongoDB
def get_cracks(db):
    return db.cracks.find()

#Initialize DB
db = get_db()
print(db)
```

    Database(MongoClient(host=['datascience_db_1:27017'], document_class=dict, tz_aware=False, connect=True), 'testDB')



```python
add_crack(db)
```

Iterate through all the cracks in the DB


```python
# Print all cracks 
for i in get_cracks(db):
    print(i)
```

Count number of cracks in the database


```python
db.cracks.count()
```




    9999



# Invoke the MongoDB Aggregation Framework


```python
# Pipeline to compute avergage, max and min width of cracks
pipeline = [{ 
    "$group": { 
        "_id": "null", 
        "min_width": {
            "$min": "$width" 
        },
        "avg_width": {
            "$avg": "$width" 
        },
        "max_width": {
            "$max": "$width" 
        }
    }
}]

pprint.pprint(list((db.cracks.aggregate(pipeline))))
```

    [{'_id': 'null',
      'avg_width': 0.5041464146414641,
      'max_width': 1.0,
      'min_width': 0.0}]


# Import MongoDB data into a DataFrame


```python
import pandas as pd

cursor = db.cracks.find()
df =  pd.DataFrame(list(cursor))
len(df)
print(df)
```

                               _id      crack  width
    0     58cdac5960589b000a5931c6     crack1   0.70
    1     58cdac5960589b000a5931c7     crack2   0.97
    2     58cdac5960589b000a5931c8     crack3   0.43
    3     58cdac5960589b000a5931c9     crack4   0.68
    4     58cdac5960589b000a5931ca     crack5   0.27
    5     58cdac5960589b000a5931cb     crack6   0.99
    6     58cdac5960589b000a5931cc     crack7   0.91
    7     58cdac5960589b000a5931cd     crack8   0.94
    8     58cdac5960589b000a5931ce     crack9   0.66
    9     58cdac5960589b000a5931cf    crack10   0.23
    10    58cdac5960589b000a5931d0    crack11   0.12
    11    58cdac5960589b000a5931d1    crack12   0.12
    12    58cdac5960589b000a5931d2    crack13   0.46
    13    58cdac5960589b000a5931d3    crack14   0.33
    14    58cdac5960589b000a5931d4    crack15   0.73
    15    58cdac5960589b000a5931d5    crack16   0.72
    16    58cdac5960589b000a5931d6    crack17   0.18
    17    58cdac5960589b000a5931d7    crack18   0.51
    18    58cdac5960589b000a5931d8    crack19   0.87
    19    58cdac5960589b000a5931d9    crack20   0.38
    20    58cdac5960589b000a5931da    crack21   0.05
    21    58cdac5960589b000a5931db    crack22   0.82
    22    58cdac5960589b000a5931dc    crack23   0.49
    23    58cdac5960589b000a5931dd    crack24   0.38
    24    58cdac5960589b000a5931de    crack25   0.70
    25    58cdac5960589b000a5931df    crack26   0.13
    26    58cdac5960589b000a5931e0    crack27   0.27
    27    58cdac5960589b000a5931e1    crack28   0.20
    28    58cdac5960589b000a5931e2    crack29   0.17
    29    58cdac5960589b000a5931e3    crack30   0.54
    ...                        ...        ...    ...
    9969  58cdac5d60589b000a5958b7  crack9970   0.21
    9970  58cdac5d60589b000a5958b8  crack9971   0.30
    9971  58cdac5d60589b000a5958b9  crack9972   0.13
    9972  58cdac5d60589b000a5958ba  crack9973   0.68
    9973  58cdac5d60589b000a5958bb  crack9974   0.01
    9974  58cdac5d60589b000a5958bc  crack9975   0.92
    9975  58cdac5d60589b000a5958bd  crack9976   0.32
    9976  58cdac5d60589b000a5958be  crack9977   0.33
    9977  58cdac5d60589b000a5958bf  crack9978   0.84
    9978  58cdac5d60589b000a5958c0  crack9979   0.55
    9979  58cdac5d60589b000a5958c1  crack9980   0.88
    9980  58cdac5d60589b000a5958c2  crack9981   0.98
    9981  58cdac5d60589b000a5958c3  crack9982   0.16
    9982  58cdac5d60589b000a5958c4  crack9983   0.72
    9983  58cdac5d60589b000a5958c5  crack9984   0.04
    9984  58cdac5d60589b000a5958c6  crack9985   0.88
    9985  58cdac5d60589b000a5958c7  crack9986   0.14
    9986  58cdac5d60589b000a5958c8  crack9987   0.79
    9987  58cdac5d60589b000a5958c9  crack9988   0.86
    9988  58cdac5d60589b000a5958ca  crack9989   0.76
    9989  58cdac5d60589b000a5958cb  crack9990   0.59
    9990  58cdac5d60589b000a5958cc  crack9991   0.11
    9991  58cdac5d60589b000a5958cd  crack9992   0.73
    9992  58cdac5d60589b000a5958ce  crack9993   0.19
    9993  58cdac5d60589b000a5958cf  crack9994   0.26
    9994  58cdac5d60589b000a5958d0  crack9995   0.71
    9995  58cdac5d60589b000a5958d1  crack9996   0.92
    9996  58cdac5d60589b000a5958d2  crack9997   0.87
    9997  58cdac5d60589b000a5958d3  crack9998   0.58
    9998  58cdac5d60589b000a5958d4  crack9999   0.62
    
    [9999 rows x 3 columns]


## Drop the database


```python
db.cracks.drop()
```


```python

```
