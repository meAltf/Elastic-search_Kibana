# standard analyzer = standard tokenizer + lowercase token filter
POST /_analyze
{
  "text": "Reach out to Support at support@domain.com or send mail to 123,Non Main Street, Atlanta, for assistance!",
  "analyzer": "standard"
}

# as standard analyzer is default, we can omit
POST /_analyze
{
  "text": "Reach out to Support at support@domain.com or send mail to 123,Non Main Street, Atlanta, for assistance!"
}