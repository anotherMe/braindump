
## OpenSearch API

Remember, you can call the API using `curl` or the console integrated in *OpenSearch Dashboard*


### Delete all documents in given index

Given the index *foo*, you can flush all the related documents using the command:

```bash
curl -XPOST "http://localhost:9200/foo/_delete_by_query" -H 'Content-Type: application/json' -d'
{
  "query": {
    "match": {
      "_index": "foo"
    }
  }
}'
```

or, in the Dashboard console:

```bash
POST foo/_delete_by_query
{
  "query": {
    "match": {
      "_index": "foo"
    }
  }
}
```

See [OpenSearch Documentation - Delete by query](https://opensearch.org/docs/latest/api-reference/document-apis/delete-by-query/)