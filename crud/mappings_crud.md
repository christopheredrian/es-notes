# mappings


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
curl -XPOST 127.0.0.1:9200/movies/_doc/109487 -d '
{
	"genre": ["IMAX", "Sci-Fi"],
	"title": "Interstellar",
	"year": 2014
}'

```


## Get

```bash
curl -XGET 127.0.0.1:9200/movies/_search?pretty
```
