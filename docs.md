````js
GET /books*/_search
{
  "query": {
    "term": {
      "_id": "9780007179817"
    }
  }
}

POST /_sql?format=txt
{
  "query": "SELECT * FROM \"books*\" WHERE isbn = 9780007179817"
}

POST  /books*/_search
{
  "query": {
    "term": {
      "_id": "9780007179817"
    }
  },
  "aggs":{
    "dedup" : {
      "terms":{
        "field": "_id"
       },
       "aggs":{
         "dedup_docs":{
           "top_hits":{
             "size":1
           }
         }
       }    
    }
  }
}
````