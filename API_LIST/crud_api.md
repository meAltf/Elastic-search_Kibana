# create index
PUT /books

# Create 
## Insert documents

POST /books/_doc
{
  "title": "To Kill a Mockingbird",
  "author": "Harper Lee",
  "year": 1960,
  "genre": "Fiction",
  "rating": 4.9
}

# To see the content inside index
GET /books/_search
