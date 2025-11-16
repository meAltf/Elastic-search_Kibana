# node roles demo
# we have 3 nodes. es01 would be the master
GET /_cat/nodes?v

# get node detailed information
GET /_nodes

# create indices
PUT /products1
PUT /products2
PUT /products3
PUT /products4

# get the information about shards
GET /_cat/shards/products*?v

# delete the indices
DELETE /products1,products2,products3,products4