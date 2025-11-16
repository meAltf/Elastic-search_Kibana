# Ensure that, 3 node cluster up and running
# create index
PUT /products

# get the information about shards
GET /_cat/shards/products?v
GET /_cat/nodes?v
GET /products/_search
GET /products/_refresh
# docker compose stop es02 | try to see an example of high availibility

# store some documents
POST /products/_doc
{
    "name": "product 3"
}

# delete index
DELETE /products