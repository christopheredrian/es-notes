# mappings

## Installation

https://linuxize.com/post/how-to-install-elasticsearch-on-ubuntu-18-04/

## Create mapping

```bash

curl -XPUT 127.0.0.1:9200/movies -d '       curl -XPUT 127.0.0.1:9200/movies -d '
{
    "mappings": {
        "properties": {
                "year": {
                        "type": "date"
                }
        }
	}
}'

```

## Get Mapping

```bash
curl -XGET 127.0.0.1:9200/movies/_mapping
```

## Insert 

```bash
curl --header "Content-Type: application/json" -XPOST 127.0.0.1:9200/movies/_doc/100 -d '
{
    "genre": ["Fiction"],
    "title": "Lord of the ings",
    "year": 2001
}'

```


## Bulk Insert 

```bash
curl --header "Content-Type: application/json" -XPUT 127.0.0.1:9200/_bulk?pretty --data-binary @movies.json
```


## Get All

```bash

curl -H "Content-Type: application/json" -XGET 127.0.0.1:9200/movies/_search?pretty

```

## Get One

```bash

curl -H "Content-Type: application/json" -XGET 127.0.0.1:9200/movies/_doc/109487?pretty

```


## Updating documents

```bash

curl -H "Content-Type: application/json" -XPUT 127.0.0.1:9200/movies/_doc/109487?pretty -d '
{
    "genres": ["IMAX", "Sci-Fi"],
    "title": "Interstellar Updated"
}
'
```

## Partial Updates

```bash


curl -H "Content-Type: application/json" -XPOST 127.0.0.1:9200/movies/_doc/109487/_update?pretty -d '
{
    "doc" : {
        "title": "Interstellar"
    }
}
'

```

## Search

```bash

curl -H "Content-Type: application/json" -XGET 127.0.0.1:9200/movies/_search?q=Dark

```


## Delete

```bash

curl -H "Content-Type: application/json" -XDELETE 127.0.0.1:9200/movies/_doc/58559?pretty

```


## Analyzers

1. Exact match 
    - Use keyword on mapping
2. Analyzed field 
    - anything remotely relevant



```bash


# Relevant matches  / Partial matches

curl -H "Content-Type: application/json" -XGET 127.0.0.1:9200/movies/_search?pretty -d '
{
    "query": {
        "match": {
            "title": "Star Treck"
        }
    }    
}
'

curl -H "Content-Type: application/json" -XGET 127.0.0.1:9200/movies/_search?pretty -d '
{
    "query": {
        "match_phrase": {
            "genre": "sci"
        }
    }    
}
'


```


## Deleting Index


```bash

curl -H "Content-Type: application/json" -XDELETE 127.0.0.1:9200/movies

```


```bash

# Note
#   - genre is on type keyword
#   - title has an analyzer english

curl --header "Content-Type: application/json" -XPUT 127.0.0.1:9200/movies?pretty -d '
{
    "mappings": {
        "properties":  {
            "id": {
                "type": "integer"
            },
            "year": {
                "type": "date"
            },
            "genre": {
                "type": "keyword"
            },
            "title": {
                "type": "text",
                "analyzer": "english"
            }
        }
    }    
}
'

# Re-index

curl --header "Content-Type: application/json" -XPUT 127.0.0.1:9200/_bulk?pretty --data-binary @movies.json


# This time if we search - we don't have a match, must be an exact field

curl -H "Content-Type: application/json" -XGET 127.0.0.1:9200/movies/_search?pretty -d '
{
    "query": {
        "match_phrase": {
            "genre": "sci"
        }
    }    
}
'

curl -H "Content-Type: application/json" -XGET 127.0.0.1:9200/movies/_search?pretty -d '
{
    "query": {
        "match_phrase": {
            "genre": "Sci-Fi"
        }
    }    
}
'
```


## Data Modeling 





























