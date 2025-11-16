# we have 3 nodes. es01 would be the master
GET /_cat/nodes?v

# bring es01 down and see what happens -> other node will became new master node

# get node detailed information
GET /_nodes