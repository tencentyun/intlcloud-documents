
This document describes how to use common queries and keywords in CTSDB with simple samples for curl. The metric structure used by all samples is as follows:
```
    {
        "ctsdb_test" : {
          "tags" : {
            "region" : "string"
          },
          "time" : {
            "name" : "timestamp",
            "format" : "epoch_millis"
          },
          "fields" : {
            "cpuUsage" : "float",
            "diskUsage" : "string",
            "dcpuUsage" : "integer"
          },
          "options" : {
            "expire_day" : 7,
            "refresh_interval" : "10s",
            "number_of_shards" : 5
          }
        }
    }
```

## Combined Query 
Combined queries can be used for single queries as well as composite queries. The `query` keyword in the query body can use query domain-specific language (DSL) to define query conditions. This document describes how to construct and combine filter conditions and process the returned result set.

### Common filter conditions 

#### 1. Range 
`Range` indicates range query, which supports fields of `string`, `long`, `integer`, `short`, `double`, `float`, and `date` types. The parameters that can be contained in a range query are as detailed below:

| Parameter | Description       |
| -------- | ---------- |
| gte      | Greater than or equal to |
| gt       | Greater than       |
| lte      | Less than or equal to |
| lt       | Less than       |

>?If a range query involves time types, you can use the `format` parameter to specify the time format. For the specific time formats, please see [Creating Metric](https://intl.cloud.tencent.com/document/product/1100/40909).

Sample code of time range query for curl:
```
    curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search -d'
    {
    	"query": {
    		"range": {
    			"timestamp": {
    				"gte": "01/01/2018",
    				"lte": "03/01/2018",
    				"format": "MM/dd/yyyy",
    				"time_zone":"+08:00"
    			  }
    		  }
    	  }
     }'
```

Sample code of numeric range query for curl:
```
	curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search -d'
	{
		"query": {
			"range": {
				"cpuUsage": {
					"gte": 1.0,
					"lte": 10.0
				}
			}
		}
	}'  
```

#### 2. Terms  
The `terms` keyword can be used to match specific fields during query, and its value needs to be enclosed by brackets ([]).

Sample code for curl:
```
    curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search -d'
    { 
    	"query": {
    		"terms": {
    			"region": ["sh", "bj"]
    		}
    	}
    }'
```

### Filter condition combination
A composite query usually uses bool keywords to combine multiple query conditions. Common combination keywords used for bool queries include `filter` (similar to `AND`), `must_not` (similar to `NOT`), and `should` (similar to `OR`). To improve the query efficiency, you must add a range query for the `time` field, which always returns a value in `epoch_millis` format no matter how the query is written. The combination of `query-bool-filter` can greatly improve the query performance, so please be sure to use it.

#### 1. Sample code of `AND` condition for curl
```
    curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search -d'
    {
  	"query": {
	    "bool": {
	      "filter": [
	        {
	          "range": {
	            "timestamp": {
	              "format": "yyyy-MM-dd HH:mm:ss",
	              "gte": "2017-11-06 23:00:00",
	              "lt": "2018-03-06 23:05:00",
				  "time_zone":"+08:00"
	            }
	
	          }
	        },
	        {
	          "terms": {
	            "region": ["sh"]
	          }
	        },
	        {
	          "terms": {
	            "cpuUsage": ["2.0"]
	          }
	        }
	      ]
	    }
	  },
  	 "docvalue_fields": [
	    "cpuUsage",
	    "timestamp"
  	  ]
	}'
```

>?The query conditions are similar to `timestamp>='2017-11-06 23:00:00' AND timestamp<'2018-03-06 23:05:00' AND region=sh AND cpuUsage=2.0`.

#### 2. Sample code of `OR` condition for curl
```
    curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search -d'
    {
  	"query": {
	    "bool": {
	      "filter": [
	        {
	          "range": {
	            "timestamp": {
	              "format": "yyyy-MM-dd HH:mm:ss",
	              "gte": "2017-11-06 23:00:00",
	              "lt": "2018-11-06 23:05:00",
				  "time_zone":"+08:00"
	            }
	          }
	        },
	        {
	          "term": {
	            "region": "gz"
	          }
	        }
	      ],
	      "should": [
	        {
	          "terms": {
	            "cpuUsage": ["2.0"]
	          }
	        },
	        {
	          "terms": {
	            "cpuUsage": ["2.5"]
	          }
	        }
	      ],
	      "minimum_should_match": 1
	    }
  	},
  	"docvalue_fields": [
	    "cpuUsage",
	    "timestamp"
  	]
	}'
```

>?The query conditions are similar to `timestamp>='2017-11-06 23:00:00' AND timestamp<'2018-11-06 23:05:00' AND region='gz' AND (cpuUsage=2.0 or cpuUsage=2.5)`. The `minimum_should_match` parameter is used to set the minimum number of results that should match `cpuUsage=2.0` and `cpuUsage=2.5`, and its default value is 0.

#### 3. Sample code of `NOT` condition for curl
```
	curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search -d'
	{
  	"query": {
	    "bool": {
	      "filter": [
	                {
	          "range": {
	            "timestamp": {
	              "format": "yyyy-MM-dd HH:mm:ss",
	              "gte": "2017-11-06 23:00:00",
	              "lt": "2018-11-06 23:05:00",
				  "time_zone":"+08:00"
	            }
	
	          }
	        },
	        {
	          "terms": {
	            "region": ["gz"]
	          }
	        }
	      ],
	      "must_not": [
	       {
	          "terms": {
	            "cpuUsage": ["2.0"]
	          }
	        }
	      ]
	    }
  	},
  	"docvalue_fields": [
	    "cpuUsage",
	    "timestamp"
  		]
  	}'
```

>?The query conditions are similar to `timestamp>=2017-11-06 23:00:00 AND timestamp\<2018-11-06 23:05:00 AND region='gz' AND cpuUsage !=2.0`.

### Processing of returned result set

#### 1. From/Size
You can paginate query results by setting the `from` and `size` keywords. The `from` keyword defines the offset of the first data entry in the query results, and `size` the maximum number of returned results. The default values of `from` and `size` are 0 and 10, respectively. The sum of `from` and `size` cannot exceed 65,536 by default. If you want to have more results returned, please see the description of query with the `scroll` keyword in this document.

Sample code for curl:
```
	curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search -d'
	{
		"from": 0,
		"size": 5,
		"query": {
			"bool": {
				"filter": {
					"range": {
						"timestamp": {
							"gte": "01/01/2018",
							"lte": "03/01/2018",
							"format": "dd/MM/yyyy",
							"time_zone":"+08:00"
						}
					}
				},
				"must_not": {
					"terms": {
						"region": ["bj"]
					}
				}
			}
		}
	}'
```

#### 2. Scroll
A scroll operation is similar to a cursor in a relational database. Therefore, it is suitable for backend batch processing rather than real-time search.
You can divide a scroll operation into two phases: initialization and traversal. During initialization, all search results matching the search conditions will be cached like with a snapshot, from which data will be taken out during traversal. Note that insertion, deletion, and update of metrics after scroll initialization will not affect the traversal result.
During initialization, you can use the `size` keyword to specify the size of the returned result set, whose default value is 10 and maximum value is 65,536. You can also use the `query` and `docvalue_fields` keywords to specify the query conditions and returned fields respectively. The `_scroll_id` field will be returned during both initialization and traversal. You can specify the `_scroll_id` returned by the previous traversal for a new traversal until the returned result is empty. During initialization and traversal, you can also use the `scroll` parameter to set the context retention time of the traversal, after which the `scroll_id` will become invalid. The time format is as detailed below:

| Format   | Description         |
| ------ | ------------ |
| d      | days         |
| h      | hours        |
| m      | minutes      |
| s      | seconds      |
| ms     | milliseconds |
| micros | microseconds |
| nanos  | nanoseconds  |

Sample code for curl:

Scroll initialization:
```
    curl -u root:le201909 -H 'Content-Type:application/json' -X POST 172.16.345.14:9201/ctsdb_test/_search?scroll=1m -d'
    {
       "size":5,
       "query": {
       "bool": {
         "filter": [
           {
             "terms": {
               "region": ["gz"]
             }
           }
         ]
       }
     },
    "docvalue_fields": [
      	"cpuUsage",
        "region",
        "timestamp"
  	  ]
	}'

```

Response of scroll initialization:
```
    {
      "_scroll_id": "DnF1ZXJ5VGhlbkZldGNoAwAAAAAADrOFFm5YSEhnMjdnUWNPcndHS1k5Wjc3bHcAAAAAAAz_1RZiRkZTcGp4dFRXR18xMGtzSmhEUFJRAAAAAAAP5vQWOXFOR29lc0hROHFWMmFGTkVmSkxmZw==",
      "took": 10641,
      "timed_out": false,
      "_shards": {
       "total": 3,
       "successful": 3,
       "skipped": 0,
       "failed": 0
      },
      "hits": {
        "total": 1592072666,
        "max_score": 0.65708643,
        "hits": [
          {
            "_index": "ctsdb_test@0_-1",
            "_type": "doc",
            "_id": "oyylNU0U65cZjByyt7sW_JmPPgAACY4Bh0",
            "_score": 0.65708643,
            "_routing": "354d14eb",
            "fields": {
              "region": [
                "gz"
              ],
              "cpuUsage": [
                "2.0"
              ],
              "timestamp": [
                1509909300000
              ]
            }
          },
          {
            "_index": "ctsdb_test@0_-1",
            "_type": "doc",
            "_id": "oyykFN0yd1d9NDPfzjRdrJ8whQAACYsBqc",
            "_score": 0.65708643,
            "_routing": "14dd3277",
            "fields": {
              "region": [
                "gz"
              ],
              "cpuUsage": [
                "1.8"
              ],
              "timestamp": [
                1509908340000
              ]
            }
          },
          {
            "_index": "ctsdb_test@0_-1",
            "_type": "doc",
            "_id": "oyylHLp9jl_3sF4N2rnh67h4SgAABHIBso",
            "_score": 0.65708643,
            "_routing": "1cba7d8e",
            "fields": {
              "region": [
                "gz"
              ],
              "cpuUsage": [
                "2.5"
              ],
              "timestamp": [
                1509909720000
              ]
            }
          },
          {
            "_index": "ctsdb_test@0_-1",
            "_type": "doc",
            "_id": "oyylH2JsOKnFHGUinQ7jM-ZwkgAAAvcBso",
            "_score": 0.65708643,
            "_routing": "1f626c38",
            "fields": {
              "region": [
                "gz"
              ],
              "cpuUsage": [
                "2.1"
              ],
              "timestamp": [
                1509909720000
              ]
            }
          },
          {
            "_index": "ctsdb_test@0_-1",
            "_type": "doc",
            "_id": "oyylHLp9jl_3sF4N2rnh67h4SgAABGsBso",
            "_score": 0.65708643,
            "_routing": "1cba7d8e",
            "fields": {
              "region": [
                "gz"
              ],
              "cpuUsage": [
                "2.0"
              ],
              "timestamp": [
                1509909720000
              ]
            }
          }
        ]
      	}
    }

```

Scroll traversal:

```
    curl -u root:le201909 -H 'Content-Type:application/json' -X POST 172.16.345.14:9201/_search/scroll  -d'
    {
    "scroll" : "1m", 
    "scroll_id" : "DnF1ZXJ5VGhlbkZldGNoAwAAAAAADrOFFm5YSEhnMjdnUWNPcndHS1k5Wjc3bHcAAAAAAAz_1RZiRkZTcGp4dFRXR18xMGtzSmhEUFJRAAAAAAAP5vQWOXFOR29lc0hROHFWMmFGTkVmSkxmZw==" 
    }'

```

>?`scroll_id` in this request is the value of `_scroll_id` returned in scroll initialization. In the next traversal, the `scroll_id` parameter value should be adjusted to the `_scroll_id` value returned in the previous traversal, that is, the `scroll_id` parameter value in each request is the `_scroll_id` value returned in the previous request, and traversal will end until the returned result is empty.

#### 3. Sort 
The `sort` keyword is mainly used to sort query results and has two orders: `asc` and `desc`. The default sorting order for custom fields in CTSDB is `asc`. Available sorting modes include `min`, `max`, `sum`, `avg`, and `median`, where `sum`, `avg`, and `median` are suitable only for fields of `array` type that store numbers only.

Sample code for curl:
```
    curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search -d'
    {
    	"query": {
    		"bool": {
    			"must": {
    				"range": {
    					"timestamp": {
    						"gte": "01/01/2018",
    						"lte": "03/01/2018",
    						"format": "MM/dd/yyyy",
    						"time_zone":"+08:00"
    					}
    				}
    			}
    		}
    	},
    	"sort": [
            {
    			"cpuUsage": {
    				"order": "asc",
    				"mode": "min"
    			}
    		},
            {
    			"timestamp": {
    				"order": "asc"
    			}
    		}, 
            "diskUsage"
        ]
    }'

```

#### 4. docvalue_fields 
The `docvalue_fields` keyword specifies the names of the fields to be returned in an array.

Sample code for curl:
```
    curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search -d'
    {
    	"query": {
    		"terms": {
    			"region": ["sh", "bj"]
    		}
    	},
    	"docvalue_fields": ["timestamp", "cpuUsage"]
    }'

```

## Aggregate Query
The `agg` keyword is mainly used to construct aggregate queries. You can get the aggregate results in the returned `aggregations` field. The returned aggregate fields are as detailed below. If you want to focus only on the aggregate results, please set the `size` parameter to 0 during query.

| Field | Description                                                         |
| ------------ | ------------------------------------------------------------ |
| hits      | Matched query results. Here, the `total` field indicates the number of data records participating in aggregate. The `hits` field is an array, which contains the first 10 query results if not specified. Each result in the `hits` array contains `_index` ([child metric](https://intl.cloud.tencent.com/document/product/1100/40909#rolling) involved in the query). If `docvalue_fields` is specified in the query, the `fields` field will be returned to indicate the value of each field. |
| took      | Time in milliseconds taken by the entire query.                                       |
| `_shards`  | Number of shards involved in the query. Here, `total` indicates the total number of shards, `successful` the shards that were successfully queried, `failed` the shards that failed to be queried, and `skipped` skipped shards. |
| timed_out | Indicates whether query timed out. Valid values: false, true.                         |
| aggregations | Returned aggregate result.                                               |

The following lists some common aggregate modes:

### Regular aggregate
For a regular aggregate, you need to specify the aggregate name, mode (common modes include `min`, `max`, `avg`, `value_count`, and `sum`), and target fields.

Sample code for curl:
```
    curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search -d'
    {
    	"size":0,
    	"query": {
    		"terms": {
    			"region": ["sh", "bj"]
    		}
    	},
    	"aggs": {
    		"myname": {
    			"max": {
    				"field": "cpuUsage"
    			}
    		}
    	}
    }'

```

>?The above sample aggregates the `cpuUsage` field in `max` mode (you can also use other modes such as `min` and `avg`), and the returned aggregate results are named the alias `myname` field (you can also specify another name).

Response:
```
{
  "took": 1,
  "timed_out": false,
  "_shards": {
    "total": 20,
    "successful": 20,
    "skipped": 0,
    "failed": 0
  },
  "hits": {
    "total": 7,
    "max_score": 0,
    "hits": []
  },
  "aggregations": {
    "myname": {
      "value": 4
    }
  }
}
```

### `terms` aggregate
A `terms` aggregate is mainly used to query all the unique values and the number of such values of a field. You can specify the rule of sorting the returned unique values and the number of returned results and perform fuzzy or exact match for data fields participating in the aggregate. For more information, please see the sample below. You can use the `filter_path` parameter to customize the returned result fields as instructed in [Batch Querying Data](https://intl.cloud.tencent.com/document/product/1100/40903).

Sample code for curl:

Request:
```
	curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search?filter_path=aggregations -d'
	{
	    "aggs": {
	        "myname": {
	            "terms": {"field":"region"}
	        }
	    }
	}'

```

Response:
```
	{
	  "aggregations": {
	    "myname": {
	      "doc_count_error_upper_bound": 0,
	      "sum_other_doc_count": 0,
	      "buckets": [
	        {
	          "key": "sh",
	          "doc_count": 10
	        },
	        {
	          "key": "Motor_sports",
	          "doc_count": 6
	        },
	        {
	          "key": "gz",
	          "doc_count": 3
	        },
	        {
	          "key": "bj",
	          "doc_count": 2
	        },
	        {
	          "key": "cd",
	          "doc_count": 2
	        },
	        {
	          "key": "Winter_sports",
	          "doc_count": 1
	        },
	        {
	          "key": "water_sports",
	          "doc_count": 1
	        }
	      ]
	    }
	  }
	}

```

>?The above sample returns all the unique values and their numbers of occurrences in the `region` field in `ctsdb_test`. By analyzing the `buckets` field in the returned `aggregations` field, you can find that the `region` field has 7 types of values, i.e., `sh`, `Motor_sports`, `gz`, `bj`, `cd`, `Winter_sports`, and `water_sports`, and the occurrence number of each value of the returned fields is indicated in `doc_count`.

You can use the `size` field to specify the number of unique values to be returned; for example, if the `region` field has 7 unique values, you can set the `size` field to 5 to return only the first 5 values. For more information, please see the sample.

Request:
```
	curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search?filter_path=aggregations -d'
	{
	    "aggs": {
	        "myname": {
	            "terms": {
	               "field":"region",
	                "size":5
	            }
	        }
	    }
	}'

```

Response:
```
	{
	  "aggregations": {
	    "myname": {
	      "doc_count_error_upper_bound": 0,
	      "sum_other_doc_count": 2,
	      "buckets": [
	        {
	          "key": "sh",
	          "doc_count": 10
	        },
	        {
	          "key": "Motor_sports",
	          "doc_count": 6
	        },
	        {
	          "key": "gz",
	          "doc_count": 3
	        },
	        {
	          "key": "bj",
	          "doc_count": 2
	        },
	        {
	          "key": "cd",
	          "doc_count": 2
	        }
	      ]
	    }
	  }
	}

```

You can sort the returned results as instructed in the sample below:
1. Request (the returned results are sorted by number of unique values in descending order):
```
    curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search?filter_path=aggregations -d'
    {
      "aggs": {
          "myname": {
              "terms": {
                "field":"region",
                "order":{"_count":"desc"}
              }
          }
      }
    }'

```

Response:
```
   {
      "aggregations": {
        "myname": {
          "doc_count_error_upper_bound": 0,
          "sum_other_doc_count": 0,
          "buckets": [
            {
              "key": "sh",
              "doc_count": 10
            },
            {
              "key": "Motor_sports",
              "doc_count": 6
            },
            {
              "key": "gz",
              "doc_count": 3
            },
            {
              "key": "bj",
              "doc_count": 2
            },
            {
              "key": "cd",
              "doc_count": 2
            },
            {
              "key": "Winter_sports",
              "doc_count": 1
            },
            {
              "key": "water_sports",
              "doc_count": 1
            }
          ]
        }
      }
    }

```

2. Request (the returned results are sorted alphabetically in ascending order):
```
    curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search?filter_path=aggregations -d'
    {
      "aggs": {
          "myname": {
              "terms": {
                "field":"region",
                "order":{"_term":"asc"}
              }
          }
      }
    }'
```

Response:
```
    {
      "aggregations": {
        "myname": {
          "doc_count_error_upper_bound": 0,
          "sum_other_doc_count": 0,
          "buckets": [
            {
              "key": "Motor_sports",
              "doc_count": 6
            },
            {
              "key": "Winter_sports",
              "doc_count": 1
            },
            {
              "key": "bj",
              "doc_count": 2
            },
            {
              "key": "cd",
              "doc_count": 2
            },
            {
              "key": "gz",
              "doc_count": 3
            },
            {
              "key": "sh",
              "doc_count": 10
            },
            {
              "key": "water_sports",
              "doc_count": 1
            }
          ]
        }
      }
    }

```

You can set a regular expression to fuzzily match fields in the `terms` aggregate or exactly match specified fields as instructed in the sample below:

Sample code of fuzzy match:
Request (only the `region` fields whose values contain `sport` and don't start with `water_` are aggregated and returned):

```
	curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search?filter_path=aggregations -d'
	{
	  "aggs": {
	      "myname": {
	          "terms": {
	            "field":"region",
	            "include" : ".*sport.*",
	          	"exclude" : "water_.*"
	          }
	      }
	  }
	}'
```

Response:
```
	{
	  "aggregations": {
	    "myname": {
	      "doc_count_error_upper_bound": 0,
	      "sum_other_doc_count": 0,
	      "buckets": [
	        {
	          "key": "Motor_sports",
	          "doc_count": 6
	        },
	        {
	          "key": "Winter_sports",
	          "doc_count": 1
	        }
	      ]
	    }
	  }
	}
```

Sample code of exact match:
Request (the `region` fields whose values are `sh`, `bj`, `cd`, and `gz` are aggregated in `region_zone`, and the `region` fields whose values are not `sh`, `bj`, `cd`, and `gz` are aggregated in `region_sports`):

```
	curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search?filter_path=aggregations -d'
	{
	"aggs" : {
	  "region_zone" : {
	    "terms" : {
	      "field" : "region",
	      "include" : ["sh", "bj","cd","gz"]
	      }
	    },
	    "region_sports" : {
	     "terms" : {
	         "field" : "region",
	         "exclude" : ["sh", "bj","cd","gz"]
	     }
	    }
	  }
	}'
```

Response:
```
	{
	  "aggregations": {
	    "region_sport": {
	      "doc_count_error_upper_bound": 0,
	      "sum_other_doc_count": 0,
	      "buckets": [
	        {
	          "key": "Motor_sports",
	          "doc_count": 6
	        },
	        {
	          "key": "Winter_sports",
	          "doc_count": 1
	        },
	        {
	          "key": "water_sports",
	          "doc_count": 1
	        }
	      ]
	    },
	    "region_zone": {
	      "doc_count_error_upper_bound": 0,
	      "sum_other_doc_count": 0,
	      "buckets": [
	        {
	          "key": "sh",
	          "doc_count": 10
	        },
	        {
	          "key": "gz",
	          "doc_count": 3
	        },
	        {
	          "key": "bj",
	          "doc_count": 2
	        },
	        {
	          "key": "cd",
	          "doc_count": 2
	        }
	      ]
	    }
	  }
	}
```

### Date histogram aggregate
A date histogram is mainly used to aggregate dates into a histogram.
Sample code for curl:
```
    curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search -d'
    {
    	"query": {
    		"terms": {
    			"region": ["sh", "bj"]
    		}
    	},
    	"aggs": {
    		"time_1h_agg": {
    			"date_histogram": {
    				"field": "timestamp",
    				"interval": "1h"
    			},
    			"aggs": {
    				"avgCpuUsage": {
    					"avg": {
    						"field": "cpuUsage"
    					}
    				}
    			}
    		}
    	}
    }'
```

Response:
```
    {
      "took": 5,
      "timed_out": false,
      "_shards": {
        "total": 20,
        "successful": 20,
        "skipped": 0,
        "failed": 0
      },
      "hits": {
        "total": 6,
        "max_score": 0.074107975,
        "hits": [
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2QtGR5xcjRaw2ETf-",
            "_score": 0.074107975,
            "_routing": "sh"
          },
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2QtGR5xcjRaw2ETf_",
            "_score": 0.074107975,
            "_routing": "sh"
          },
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2Q5Xr5xcjRaw2ETgA",
            "_score": 0.074107975,
            "_routing": "sh"
          },
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2Q5Xr5xcjRaw2ETgB",
            "_score": 0.074107975,
            "_routing": "sh"
          },
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2RGfF5xcjRaw2ETgC",
            "_score": 0.074107975,
            "_routing": "sh"
          },
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2RGfF5xcjRaw2ETgD",
            "_score": 0.074107975,
            "_routing": "sh"
          }
        ]
      },
      "aggregations": {
        "time_1h_agg": {
          "buckets": [
            {
              "key_as_string": "1520222400",
              "key": 1520222400000,
              "doc_count": 1,
              "avgCpuUsage": {
                "value": 2.5
              }
            },
            {
              "key_as_string": "1520226000",
              "key": 1520226000000,
              "doc_count": 0,
              "avgCpuUsage": {
                "value": null
              }
            },
            {
              "key_as_string": "1520229600",
              "key": 1520229600000,
              "doc_count": 0,
              "avgCpuUsage": {
                "value": null
              }
            },
            {
              "key_as_string": "1520233200",
              "key": 1520233200000,
              "doc_count": 0,
              "avgCpuUsage": {
                "value": null
              }
            },
            {
              "key_as_string": "1520236800",
              "key": 1520236800000,
              "doc_count": 0,
              "avgCpuUsage": {
                "value": null
              }
            },
            {
              "key_as_string": "1520240400",
              "key": 1520240400000,
              "doc_count": 0,
              "avgCpuUsage": {
                "value": null
              }
            },
            {
              "key_as_string": "1520244000",
              "key": 1520244000000,
              "doc_count": 0,
              "avgCpuUsage": {
                "value": null
              }
            },
            {
              "key_as_string": "1520247600",
              "key": 1520247600000,
              "doc_count": 1,
              "avgCpuUsage": {
                "value": 2
              }
            },
            {
              "key_as_string": "1520251200",
              "key": 1520251200000,
              "doc_count": 4,
              "avgCpuUsage": {
                "value": 2.25
              }
            }
          ]
        }
      }
    }
```

>?The above sample aggregates the `cpuUsage` field in `date_histogram` mode with a granularity of 1 hour. The total aggregate name of the returned results is `time_1h_agg` (you can specify another name), and the aggregate name in each time interval is `avgCpuUsage` (you can specify another name). The valid time granularities for `interval` include `year`, `quarter`, `month`, `week`, `day`, `hour`, `minute`, and `second`. You can also represent the time granularity as a time unit; for example, `1y` represents 1 year, and `1h` 1 hour. The system does not support decimal time units; therefore, you need to convert `1.5h` to `90min` for example.

### Percentiles aggregate
You can specify the percentile in percentiles aggregate. The system default percentiles are 1, 5, 25, 50, 75, 95, and 99.

Sample code for curl:
```
	curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search -d'
	{
		"query": {
			"terms": {
				"region": ["sh", "bj"]
			}
		},
		"aggs": 
	    {
	        "myname": 
	        {
	            "percentiles":
	            {
	                "field": "cpuUsage",
	                "percents": [1,25,50,70,99]
	            }
	        }
	    }
	}'

```

Response:
```
    {
      "took": 18,
      "timed_out": false,
      "_shards": {
        "total": 20,
        "successful": 20,
        "skipped": 0,
        "failed": 0
      },
      "hits": {
        "total": 6,
        "max_score": 0.074107975,
        "hits": [
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2QtGR5xcjRaw2ETf-",
            "_score": 0.074107975,
            "_routing": "sh"
          },
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2QtGR5xcjRaw2ETf_",
            "_score": 0.074107975,
            "_routing": "sh"
          },
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2Q5Xr5xcjRaw2ETgA",
            "_score": 0.074107975,
            "_routing": "sh"
          },
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2Q5Xr5xcjRaw2ETgB",
            "_score": 0.074107975,
            "_routing": "sh"
          },
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2RGfF5xcjRaw2ETgC",
            "_score": 0.074107975,
            "_routing": "sh"
          },
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2RGfF5xcjRaw2ETgD",
            "_score": 0.074107975,
            "_routing": "sh"
          }
        ]
      },
      "aggregations": {
        "myname": {
          "values": {
            "1.0": 2,
            "25.0": 2,
            "50.0": 2.25,
            "70.0": 2.5,
            "99.0": 2.5
          }
        }
      }
    }
```

>?The above sample aggregates the `cpuUsage` field in `percentiles` mode, and the selected percentiles are 1, 25, 50, 70, and 99. The returned aggregate results are named the alias `myname` (you can also specify another name).

### Cardinality aggregate
A cardinality aggregate is mainly used to get the number of deduplicated results. By default, if the number of aggregate results is less than or equal to 3,000, the result returned by `cardinality` will be precise; otherwise, the result will be approximate.

Sample code for curl:
```
	curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/ctsdb_test/_search -d'
	{
		"query": {
			"terms": {
				"region": ["sh", "bj"]
			}
		},
		"aggs": 
	    {
	        "myname": 
	        {
	            "cardinality":
	            {
	                "field": "cpuUsage"
	            }
	        }
	    }
	}'
```

Response:
```
    {
      "took": 15,
      "timed_out": false,
      "_shards": {
        "total": 20,
        "successful": 20,
        "skipped": 0,
        "failed": 0
      },
      "hits": {
        "total": 6,
        "max_score": 0.074107975,
        "hits": [
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2QtGR5xcjRaw2ETf-",
            "_score": 0.074107975,
            "_routing": "sh"
          },
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2QtGR5xcjRaw2ETf_",
            "_score": 0.074107975,
            "_routing": "sh"
          },
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2Q5Xr5xcjRaw2ETgA",
            "_score": 0.074107975,
            "_routing": "sh"
          },
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2Q5Xr5xcjRaw2ETgB",
            "_score": 0.074107975,
            "_routing": "sh"
          },
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2RGfF5xcjRaw2ETgC",
            "_score": 0.074107975,
            "_routing": "sh"
          },
          {
            "_index": "ctsdb_test@1520092800000_3",
            "_type": "doc",
            "_id": "AWH2RGfF5xcjRaw2ETgD",
            "_score": 0.074107975,
            "_routing": "sh"
          }
        ]
      },
      "aggregations": {
        "myname": {
          "value": 2
        }
      }
    }
```

>?The above sample aggregates the `cpuUsage` field in `cardinality` mode, and the returned aggregate result is named the alias `myname` (you can also specify another name).
