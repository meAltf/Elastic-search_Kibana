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


## Demo -2 | Optimistic concurrency control / multiple indices

# bulk insert
POST /countries/_bulk
{ "create" : { "_id": 1 } }
{ "name" : "Dubai" }
{ "create" : { "_id": 2 } }
{ "name" : "Saudi Arabia" }
{ "create" : { "_id": 3 } }
{ "name" : "Iran" }

# bulk update
POST /countries/_bulk
{ "update" : { "_id": 2, "if_seq_no": "1", "if_primary_term": "1" } }
{ "doc": { "name" : "item2-updated" }}
{ "update" : { "_id": 3, "if_seq_no": "2", "if_primary_term": "1" } }
{ "doc": { "name" : "item3-updated" }}

# query all
GET /countries/_search

# bulk insert
POST /_bulk
{ "create" : { "_index": "countries1", "_id": 1 } }
{ "name" : "Dubai" }
{ "create" : { "_index": "countries2", "_id": 2 } }
{ "name" : "Saudi Arabia" }
{ "create" : { "_index": "countries3", "_id": 3 } }
{ "name" : "Iraq" }

# query countries1
GET /countries1/_search

# query all indices
GET /countries*/_search

# delete all the indices
DELETE /countries1,countries2,countries3


# Demo -3 | file upload
# go to location of bulk upload file and run the below command

curl -XPOST "http://localhost:9201/products/_bulk?pretty" -H "Content-Type: application/x-ndjson" --data-binary @products-bulk-upload.ndjson
