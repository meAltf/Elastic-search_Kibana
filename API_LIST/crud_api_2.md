DELETE /books

PUT /books

POST /books/_doc/1
{
  "title": "To Kill a Mockingbird",
  "author": "Harper Lee",
  "year": 1960,
  "genre": "Fiction",
  "rating": 4.9
}

POST /books/_doc/2
{
  "title": "1984",
  "author": "George Orwell",
  "year": 1949,
  "genre": "Dystopian",
  "rating": 4.8
}

POST /books/_doc/3
{
  "title": "The Great Gatsby",
  "author": "F. Scott Fitzgerald",
  "year": 1925,
  "genre": "Fiction",
  "rating": 4.7
}

POST /books/_doc/4
{
  "title": "Pride and Prejudice",
  "author": "Jane Austen",
  "year": 1813,
  "genre": "Romance",
  "rating": 4.6
}

# To get doc with id
GET /books/_doc/2

# query all
GET /books/_search

# To search with some keyword
GET /books/_search?q=Lee
GET /books/_search?q=fiction
GET /books/_search?q=4.6

# To update a doc with ID.
## POST will also work. PUT/POST will have the upsert behavior.

POST /books/_doc/5
{
  "title": "Pride and Robert",
  "author": "Robert Alataf",
  "year": 2000,
  "genre": "Hustle",
  "rating": 4.9
}

GET /books/_doc/3

# It will replace whole object with this one -> to update one field we need to give whole object again with PUT
PUT /books/_doc/3
{
  "year": 2002
}

GET /books/_doc/3

# Patch
# To update only specified field
POST /books/_update/5
{
    "doc":{
        "year": "2003",
        "genre": "Hustle-2"
    }
}

GET /books/_doc/3

# noop
## If same above query trying to apply again -> it will give result - "noop" | means no need to change it's already existed.
POST /books/_update/5
{
    "doc":{
        "year": "2003",
        "genre": "Hustle-2"
    }
}


# To add a new field
POST /books/_update/5
{
    "doc": {
        "price": "$200"
    }
}
