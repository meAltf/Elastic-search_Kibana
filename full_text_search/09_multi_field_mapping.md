# Multi-field mapping
# delete index
DELETE /jobs

# create index with the mapping
# added one raw field to store same text as keyword
# raw it's just a name, we can able to change the name
PUT /jobs
{
  "mappings": {
    "properties": {
      "title": {
        "type": "text",
        "fields": {
          "raw": {
            "type": "keyword"
          }
        }
      }
    }
  }
}

# insert records
POST /jobs/_bulk
{"index":{}}
{"title": "Software Engineer"}
{"index":{}}
{"title": "Cloud Engineer"}
{"index":{}}
{"title": "Data Scientist"}
{"index":{}}
{"title": "Marketing Manager"}
{"index":{}}
{"title": "DevOps Engineer"}

# match query - no exact match for large text fields
POST /jobs/_search
{
  "query": {
    "match": {
      "title": "Cloud Engineer"
    }
  }
}

# term query | .raw-> it will search as a keyword type
POST /jobs/_search
{
  "query": {
    "term": {
      "title.raw": "Cloud Engineer"
    }
  }
}