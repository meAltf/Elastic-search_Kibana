PUT /countries

# Bulk insert
POST /countries/_bulk
{"create" : {} }
{"name" : "Dubai" }
{"create" : {} }
{"name" : "Saudi Arab" }
{"create" {} }
{"name" : "Iran" }

GET /countries/_search
DELETE /countries

# bulk insert with id
POST /countries/_bulk
{ "create" : { "_id": 1 } }
{ "name" : "item1" }
{ "create" : { "_id": 2 } }
{ "name" : "item2" }
{ "create" : { "_id": 3 } }
{ "name" : "item3" }

# query all
GET /countries/_search

# bulk insert / update / delete
POST /countries/_bulk
{ "create" : { "_id": 1 } }
{ "name" : "item1" }
{ "create" : { "_id": 2 } }
{ "name" : "item2" }
{ "create" : { "_id": 3 } }
{ "name" : "item3" }
{ "update" : { "_id": 2 } }
{ "doc": { "name" : "item2-updated" }}
{ "create" : { "_id": 4 } }
{ "name" : "item4" }
{ "delete" : { "_id": 1 } }

# query all
GET /my-index/_search