## Analysis

ik 分词器: [https://github.com/medcl/elasticsearch-analysis-ik](https://github.com/medcl/elasticsearch-analysis-ik)

```shell
# 查看插件目录
GET /_cat/plugins

# 查看分词效果
GET _analyze
{
  "analyzer": "ik_smart",
  "text": "服务器更新至第三版"
}
GET _analyze
{
  "analyzer":"ik_max_word",
  "text": "服务器更新至第三版"
}
```



## 衡量相关性

Information Retrieval

- Precision(查准率) - 尽可能返回较少的无关文档
- Reca(查全率) - 尽量返回较多的相关文档
- Ranking - 是否能够按照相关度进行排序?



## Query DSL

### Full text queries-全文查询 [^2]

#### match [^1]

先用分词器拆词之后再搜索文档, "hello world" 先拆分成 "hello" 和 "world"

- Example1:  会搜索到 包含 "hello" 和 "world" 文档的结果 	

```
GET match_test/_search
{
"query": {
  "match": {
    "title": "hello world"
  }
}
```
等同于:
```
GET match_test/_search
{
  "query": {
    "match": {
      "title": {
        "query": "hello world",
        "operator": "or"
      }
    }
  }
}
```

- Example2:  只会搜索到同时包含 "hello" 和 "world" 文档的结果 	

```
GET match_test/_search
{
  "query": {
    "match": {
      "title": {
        "query": "hello world",
        "operator": "and"
      }
    }
  },
  "profile": "true"
}
```

####　Match Phrase 短语搜索

查询的内容必须按照顺序出现，slop 可以指定最多能跳过多少个词语匹配

Example1：

```
GET match_test/_search
{
  "query": {
    "match_phrase": {
      "title": {
        "query": "hello world"
      }
    }
  }
}
```

- [x] hello world
- [x] say hello world
- [ ] hello my world

Example1：

```
GET match_test/_search
{
  "query": {
    "match_phrase": {
      "title": {
        "query": "hello world",
        "slop": 1
      }
    }
  }
}
```

- [x] hello world
- [x] say hello world
- [x] hello **my** world



#### match 和 match phrase

Match中的 terms 之间是 or 的关系， Match phrase 的 terms 之间是 and 的关系，并且 term 之间位置关系也影响搜索的结果



### term 查询

>  term 是表达语义的最小单位

- 使用 term 查询**不会做分词**，会当做一个整体在倒排索引中查找准确的词，并且使用相关度算分公式为每个包含该词项的文档进行**相关度算分**
- 可以通过 Constant Score 将查询转换成一个 Filtering， 避免算分，并利用缓存，提高性能



Example1：

```
POST apple/_bulk
{"index":{"_id":1}}
{"productId": "xxx-a-b-1", "title":"iPhone"}
{"index":{"_id":2}}
{"productId": "xxx-a-b-2", "title":"iPad"}
{"index":{"_id":3}}
{"productId": "xxx-a-b-3", "title":"MBP"}
```

查询：

```
GET apple/_search
{
  "query": {
    "term": {
      "title": {
        "value": "iPhone"
      }
    }
  }
}

# 返回结果 []
```

返回结果为空，理论上应该要返回一条记录，为什么呢？

因为 term 是不分词查询，但数据录入时，es 会自动进行分词处理，我们来看看 iPhone 会分成什么样

```
GET _analyze
{
  "analyzer": "standard",
  "text": "iPhone"
}
```

结果：

```
{
  "tokens" : [
    {
      "token" : "iphone",
      "start_offset" : 0,
      "end_offset" : 6,
      "type" : "<ALPHANUM>",
      "position" : 0
    }
  ]
}
```

原来是分词成了 iphone ，因为 term 是不分词查询，所以 iPhone 无法匹配到 iphone 所以就导致没有结果

可以查询子字段的 keyword ，就会查询出一条结果

```
GET apple/_search
{
  "query": {
    "term": {
      "title.keyword": {
        "value": "iPhone"
      }
    }
  }
}
```









[^1]:https://www.elastic.co/guide/en/elasticsearch/reference/7.0/query-dsl-match-query.html#match-field-params
[^2]:https://www.elastic.co/guide/en/elasticsearch/reference/7.0/full-text-queries.html

