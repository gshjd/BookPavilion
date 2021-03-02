![](https://user-gold-cdn.xitu.io/2020/6/19/172cc3ab7af1ee85?w=456&h=325&f=png&s=289804)



> 人生起起伏伏，有风光无限日，也有落魄失魂时，人在低谷时，唯有“熬过去，才会赢”  



#### 前言

大家好，我又来了，这一期要将多字段匹配了，进度还是有点慢的，哈哈哈哈，没关系没关系，我们慢慢学习啦。



## 多字符串查询

简单说，多字符川查询就是多条件查询，多条件查询，我们第一选择就是bool查询，bool查询本身采取的策略就是`条件越多越好`，当子查询是match语句时，bool查询语句的评分，是每条match语句评分加起来的总和。
具体的查询方式这里就不写了，之前的文章都有写过，这边只是顺带提到一下这个概念。



## multi_match查询
`multi_match查询`是在多个字段上对一个条件进行反复查询，缩短我们的代码量，比如我现在要在`title`和`content`两个字段，查询带有`elasticsearch good`这个字符串，我们可以简写成如下：

```json
{
    "query": {
        "multi_match": {
            "query": "elasticsearch good",
            "fields": ["name","nickName"]
        }
    }
}
```
这样就很简单方便了，这个语句转化成Spring Data的写法就更加方便了：
```java
public void multiMatch() {
    QueryBuilder queryBuilder = QueryBuilders.multiMatchQuery("39446462-d653-40d4-ab01-acb9f07a3161", "name.keyword", "nickName.keyword");
    out(queryBuilder);
}
```



## 前缀查询
前缀查询对应的是mysql的like%查询，也就是我们日常说的后模糊查询，后模糊查询性能代码对比如下：
DSL：
```json
{
    "query": {
        "prefix": {
            "name.keyword": "elasticsearch"
        }
    }
}
```
MySQL:
```sql
select * from demo where name like 'elasticsearch%'
```
Spring Data JPA：
```java
public void prefixQuery() {
    QueryBuilder queryBuilder = QueryBuilders.prefixQuery("name.keyword", "elasticsearch");
    out(queryBuilder);
}
```



## 通配符与正则表达式查询
除了刚才提到的后模糊查询，我们也可以使用通配符查询完全实现和like一样的查询操作。除开通配符查询意外，也是支持正则表达式的，可以自己更换一下查询。
DSL：
```json
{
    "query": {
        "wildcard": {
          "name.keyword": "*小*"
        }
    }
}
```
MySQL：
```sql
select * from demo where name like '%小%'
```
Spring Data JPA：
```java
public void wildcardQuery() {
    QueryBuilder queryBuilder = QueryBuilders.prefixQuery("name.keyword", "e");
    out(queryBuilder);
}
```
##### 注：通配符用法很多，可以参杂在中间查询，比如我要查询李小熊，我可以查询`李*熊`

## 查询时输入即搜索
查询时输入即搜索是`match_phrase_prefix`，它和`prefix`都是前缀搜索，`prefix`不做评分计算，只要匹配的，全都会返回，而且推荐使用`prefix`过滤器，因为这个是会有缓存的，而`prefix`是不会的。`match_phrase_prefix`是取一个字符串的末尾最后一个字符做前缀查询，比如我们查询`I like elast`这个时候实际上会展示 `I like elastisearch` 等词，但是查询结果没有`prefix`那么多，因为有`max_expansions`控制，他会控制`elast`匹配的词，再去查询含有`I`和l`like`的词。其实使用`match_phrase_prefix`而不加`keyword`的时候是等同于`match`，查询结果是一致的。

## 总结
最近elasticsearch和jpa有更新了，这边我也把代码升级了，支持最新版本的elasticsearch，这边我贴上github的地址，有兴趣的朋友可以下载看看，里面都有系列文章的所有操作。
##### `github：https://github.com/gshjd/elasticsearch-demo`



<p style="font-size: 16px; text-align: center;" align="center"><img src="https://user-gold-cdn.xitu.io/2020/4/15/1717b9ceedaa7d10?w=300&h=300&f=png&s=25086" data-ratio="1" alt="1d539c0bf7d7bb104a29bf93ff2db6ed.png" data-w="1" style="width:auto;"></p>
