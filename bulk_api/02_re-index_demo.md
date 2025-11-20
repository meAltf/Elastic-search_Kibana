##  Demo on re-index
PUT /countries
{
    "settings": {
        "number_of_shards": 1,
        "number_of_replicas": 0
    }
}

# bulk insert
POST /countries/_bulk
{ "create" : {"_id": 1 } }
{ "name" : "item1" }
{ "create" : {"_id": 2 } }
{ "name" : "item2" }
{ "create" : {"_id": 3 } }
{ "name" : "item3" }
{ "create" : {"_id": 4 } }
{ "name" : "item4" }
{ "create" : {"_id": 5 } }
{ "name" : "item5" }
{ "create" : {"_id": 6 } }
{ "name" : "item6" }

# query all
GET /countries/_search

# get shards info
GET /_cat/shards/countries?v

# create new index with 2 shards
PUT /new-countries
{
    "settings": {
        "number_of_shards": 2,
        "number_of_replicas": 0
    }
}

# reindex
POST /_reindex
{
 "source": {
   "index": "countries"
 },
 "dest": {
   "index": "new_countries"
 }
}

# query all
GET /new_countries/_search

# get shards info
GET /_cat/shards/new_countries?v

# delete indices
DELETE /countries,new_countries

# Reindex with specific fields

PUT /person
{
    "settings": {
        "number_of_shards": 1,
        "number_of_replicas": 0
    }
}

# bulk insert
POST /person/_bulk
{ "create" : { "_id": 1} }
{"name": "Alice Johnson", "age": 28, "gender": "Female", "city": "New York"}
{ "create" : { "_id": 2} }
{"name": "Michael Smith", "age": 34, "gender": "Male", "city": "Los Angeles"}
{ "create" : { "_id": 3} }
{"name": "Sophia Davis", "age": 22, "gender": "Female", "city": "Chicago"}
{ "create" : { "_id": 4} }
{"name": "James Brown", "age": 45, "gender": "Male", "city": "Houston"}
{ "create" : { "_id": 5} }
{"name": "Emily Garcia", "age": 30, "gender": "Female", "city": "Phoenix"}

# query all
GET /person/_search

# get shards info
GET /_cat/shards/person?v

# create new index with 2 shards
PUT /new-person
{
    "settings": {
        "number_of_shards": 2,
        "number_of_replicas": 0
    }
}

# reindex with specific fields
POST /_reindex
{
 "source": {
   "index": "person",
   "_source": []
 },
 "dest": {
   "index": "new-person"
 }
}

# query all
GET /new-person/_search

# get shards info
GET /_cat/shards/new-person?v

# delete indices
DELETE /person,new-person



## NOTE :
# source index can accept multiple indices as list, like combine the 2 index and copy the data into new one.
# 