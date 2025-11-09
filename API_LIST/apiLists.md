API:

# GET RESPONSE OF API'S
# Normal & details response
- GET /_cluster/health
- GET /_nodes

#To get response in short
- GET /_cat/health?v
- GET /_cat/nodes?v

#CRUD operation
GET /_cat/indices?v

#To find indices based on name | search like this: *Keyword*
GET /_cat/indices/*transform*?v

# CREATE & DELETE indices
PUT /products
GET /_cluster/health
DELETE /products