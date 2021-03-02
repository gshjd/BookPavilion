## 编写时间

2020-05-06

## 变更时间

1、2020-05-08 （1-3）
2、2020-05-09 （4-5）

## 变更内容

1、店铺分析接口第一段“storeAnalysis”修改为“shopAnalysis”
2、店铺分析 添加 前端渲染ID
3、修改店铺分析返回值
4、店铺分析 新增参数 shopId(店铺id)5、店铺返回参数改变，同时新增店铺诊断6、买家订单详情 返回参数 新增 付款件数

## 通信协议

HTTPS

## 请求方法

POST

# 店铺分析

## 1. 付款金额排行

### 1.1 接口地址

/shopAnalysis/paymentAmountRanking

### 1.2 字段

| 字段名                  | 类型   | 描述                               | 备注                        |
| ----------------------- | ------ | ---------------------------------- | --------------------------- |
| shopId                  | int    | 店铺id                             | -                           |
| statisticalDimension    | int    | 统计维度                           | 0单笔付款金额 1多笔付款金额 |
| payStartTime            | string | 付款开始时间                       | -                           |
| payEndTime              | string | 付款结束时间                       | -                           |
| excludeRefunds          | int    | 排除退款商品（含退款中和退款成功） | 0勾选 1不勾选               |
| excludeOrderAmount      | string | 排除订单金额低于                   | -                           |
| interceptionPeopleCount | int    | 截取人数                           | 只展示前?人                 |
| pageNumber              | int    | 当前页                             | -                           |
| pageSize                | int    | 条数                               | -                           |

### 1.3 返回结果

| 字段名        | 类型    | 描述         | 备注 |
| ------------- | ------- | ------------ | ---- |
| success       | boolean | 是否成功     | -    |
| code          | int     | 响应码       | -    |
| msg           | string  | 响应信息     | -    |
| totalCount    | long    | 总条数       | -    |
| data          | object  | 统计明细     | -    |
| shopDiagnosis | string  | 店铺诊断     | -    |
| count         | long    | 总条数       | -    |
| list          | list    | 列表         | -    |
| buyerId       | string  | 买家id       | -    |
| payAmount     | string  | 付款金额     | -    |
| payNumber     | int     | 付款件数(件) | -    |
| orderNumber   | string  | 订单号       | -    |
| payTime       | string  | 付款时间     | -    |
| frontEndId    | string  | 前端渲染id   | -    |

## 付款件数排行

### 2. 接口地址

 /shopAnalysis/numberOfPaymentsRanking

### 2.1 字段

| 字段名                  | 类型   | 描述                               | 备注                        |
| ----------------------- | ------ | ---------------------------------- | --------------------------- |
| shopId                  | int    | 店铺id                             | -                           |
| statisticalDimension    | int    | 统计维度                           | 0单笔付款金额 1多笔付款金额 |
| payStartTime            | string | 付款开始时间                       | -                           |
| payEndTime              | string | 付款结束时间                       | -                           |
| excludeRefunds          | int    | 排除退款商品（含退款中和退款成功） | 0勾选 1不勾选               |
| excludeOrderAmount      | string | 排除订单金额低于                   | -                           |
| excludeOrderNumber      | int    | 排除订单件数低于                   | -                           |
| interceptionPeopleCount | int    | 截取人数                           | 只展示前?人                 |
| pageNumber              | int    | 当前页                             | -                           |
| pageSize                | int    | 条数                               | -                           |

### 2.2 返回结果

| 字段名        | 类型    | 描述     | 备注 |
| ------------- | ------- | -------- | ---- |
| success       | boolean | 是否成功 | -    |
| code          | int     | 响应码   | -    |
| msg           | string  | 响应信息 | -    |
| data          | object  | 统计明细 | -    |
| shopDiagnosis | string  | 店铺诊断 | -    |
| count         | long    | 总条数   | -    |
| list          | list    | 列表     | -    |
| buyerId       | int     | 买家id   | -    |
| orderAmount   | string  | -        |      |
| payNumber     | string  | 付款件数 | -    |
| orderNumber   | string  | 订单号   | -    |
| payTime       | string  | 付款时间 | -    |

## 3. 付款时间排行

### 1.1 接口地址

 /shopAnalysis/topPaymentTimeRanking

### 1.2 字段

| 字段名                          | 类型   | 描述                               | 备注          |
| ------------------------------- | ------ | ---------------------------------- | ------------- |
| shopId                          | int    | 店铺id                             | -             |
| payStartTime                    | string | 付款开始时间                       | -             |
| payEndTime                      | string | 付款结束时间                       | -             |
| productName                     | string | 商品名称                           | -             |
| excludeRefunds                  | int    | 排除退款商品（含退款中和退款成功） | 0勾选 1不勾选 |
| excludeOrderAmount              | string | 排除订单金额低于                   | -             |
| numberOfSingleOrdersNumberStart | int    | 单笔订单购买商品件数 开始          | -             |
| numberOfSingleOrdersNumberEnd   | int    | 单笔订单购买商品件数 结束          | -             |
| interceptionPeopleCount         | int    | 截取人数                           | 只展示前?人   |
| pageNumber                      | int    | 当前页                             | -             |
| pageSize                        | int    | 条数                               | -             |

### 1.3 返回结果

| 字段名        | 类型    | 描述         | 备注 |
| ------------- | ------- | ------------ | ---- |
| success       | boolean | 是否成功     | -    |
| code          | int     | 响应码       | -    |
| msg           | string  | 响应信息     | -    |
| totalCount    | long    | 总条数       | -    |
| data          | object  | 统计明细     | -    |
| shopDiagnosis | string  | 店铺诊断     | -    |
| count         | long    | 总条数       | -    |
| list          | list    | 列表         | -    |
| buyerId       | string  | 买家id       | -    |
| orderAmount   | string  | 订单金额     | -    |
| payTime       | string  | 付款时间     | -    |
| orderNumber   | string  | 订单号       | -    |
| payNumber     | int     | 商品购买件数 | -    |
| productName   | string  | 商品名称     | -    |

## 4. 买家订单详情

### 1.1 接口地址

 /shopAnalysis/buyerOrderDetails

### 1.2 字段

| 字段名                          | 类型   | 描述                               | 备注          |
| ------------------------------- | ------ | ---------------------------------- | ------------- |
| shopId                          | int    | 店铺id                             | -             |
| memberId                        | int    | 买家id                             | -             |
| payStartTime                    | string | 付款开始时间                       | -             |
| payEndTime                      | string | 付款结束时间                       | -             |
| productName                     | string | 商品名称                           | -             |
| excludeRefunds                  | int    | 排除退款商品（含退款中和退款成功） | 0勾选 1不勾选 |
| excludeOrderAmount              | string | 排除订单金额低于                   | -             |
| numberOfSingleOrdersNumberStart | int    | 单笔订单购买商品件数 开始          | -             |
| numberOfSingleOrdersNumberEnd   | int    | 单笔订单购买商品件数 结束          | -             |
| interceptionPeopleCount         | int    | 截取人数                           | 只展示前?人   |
| pageNumber                      | int    | 当前页                             | -             |
| pageSize                        | int    | 条数                               | -             |

### 1.3 返回结果

| 字段名      | 类型    | 描述     | 备注 |
| ----------- | ------- | -------- | ---- |
| success     | boolean | 是否成功 | -    |
| code        | int     | 响应码   | -    |
| msg         | string  | 响应信息 | -    |
| totalCount  | long    | 总条数   | -    |
| data        | list    | 统计明细 | -    |
| buyerId     | int     | 买家id   | -    |
| payAmount   | string  | 付款金额 | -    |
| payNumber   | int     | 付款件数 | -    |
| orderNumber | string  | 订单号   | -    |
| payTime     | string  | 付款时间 | -    |

## 5. 店铺分析下载报表

### 1.1 接口地址

 /shopAnalysis/downloadReport

### 1.2 字段

| 字段名 | 类型 | 描述 | 备注 |
| ------ | ---- | ---- | ---- |
|        |      |      |      |

### 1.3 返回结果

| 字段名  | 类型    | 描述     | 备注 |
| ------- | ------- | -------- | ---- |
| success | boolean | 是否成功 | -    |
| code    | int     | 响应码   | -    |
| msg     | string  | 响应信息 | -    |
| data    | list    | 统计明细 | 空   |

# 客户分析

## 1. 评价行为分析

### 1.1 接口地址

/customerAnalysis/evaluationBehaviorAnalysis

### 1.2 字段

| 字段名    | 类型   | 描述             | 备注 |
| --------- | ------ | ---------------- | ---- |
| startTime | string | 确认收货起始时间 | -    |
| endTime   | string | 确认收货结束时间 | -    |

### 1.3 返回结果

| 字段名                              | 类型    | 描述             | 备注  |
| ----------------------------------- | ------- | ---------------- | ----- |
| success                             | boolean | 是否成功         | -     |
| code                                | int     | 响应码           | -     |
| msg                                 | string  | 响应信息         | -     |
| totalCount                          | long    | 总条数           | -     |
| data                                | list    | 统计明细         |       |
| confirmReceiptDate                  | string  | 确认收货时间     | -     |
| orderNumber                         | int     | 确认收货订单数   | -     |
| childOrderNumber                    | int     | 确认收货子订单数 | -     |
| notEvaluatedChildOrderNumber        | int     | 未评价子订单数   | -     |
| activeEvaluationChildOrderNumber    | int     | 主动评价子订单数 | -     |
| automaticEvaluationChildOrderNumber | int     | 自动评价子订单数 | -     |
| positiveComments                    | int     | 好评数           | -     |
| mediumRating                        | int     | 中评数           | -     |
| badReview                           | int     | 差评数           | -     |
| 诊断及建议：                        |         |                  |       |
| proportionOfActiveEvaluation        | string  | 主动评价占比     | 不带% |
| mediumRatingTotalNumber             | int     | 中评总数         | -     |
| badReviewTotalNumber                | int     | 差评总数         | -     |