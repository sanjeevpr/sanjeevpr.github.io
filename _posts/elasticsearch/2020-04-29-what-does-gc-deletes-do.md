---
layout: post
title: "What Does gc_deletes Do?"
description: "gc_deletes and it's mistery"
comments: true
keywords: "elasticsearch, gc_deletes"
---

In Elasticsearch, we usually index, update and delete documents quiet frequently. But there are few caveats or catches that you need to look out for if you do it frequently and within short intervals of time.

## Deletion of a document
The deletion of a document also updates the version of the document. For example, if the `_version` of the document with the `_id` 1 was 3, after a successful deletion, the `_version` will be incremented to 4. When a document is deleted, it is not deleted immediately, it will be temporarily marked as deleted. At this point, the document won't be searchable. After some amount of time, the Elasticsearch garbage collector collects the documents which are marked as deleted for permanent deletion. If the same document is indexed or updated with the same `_id`, the document will be resurrected and the `_version` will be incremented by 1. This is of course not expected at all. This can lead to some unexpected behaviors. 

## gc_deletes to the rescue
The time after which the documents are picked up for permanent deletion by the Elasticsearch garbage collector is set in the _settings field called gc_deletes. This is set to 60 seconds by default during the index creation. This can be changed dynamically, after the index creation also using the following query:  
```javascript
curl -X PUT "localhost:9200/myindex/_settings?pretty" -H 'Content-Type: application/json' -d'  
{  
    "index" : {  
        "gc_deletes" : 0  
    }  
}'  
```  

Setting it to 0 or 0 sec instructs Elasticsearch GC to immediately pick-up the documents which are marked as deleted. Hence, the subsequent index operation using the same id will be a new document with `_version 1`. You can check the new value in using the _settings API  
```javascript
curl -X GET "localhost:9200/myindex/_settings?pretty"
```

## References
[https://www.elastic.co/blog/versioning](https://www.elastic.co/blog/versioning)
[https://github.com/elastic/elasticsearch/issues/2166](https://github.com/elastic/elasticsearch/issues/2166])
