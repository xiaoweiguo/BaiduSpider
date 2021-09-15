# Dolphin API接口文档
# 更新记录

## 2021.09.10  （v4.4.0）

* 完善faultcode

## 2021.07.16

* 编辑活动/订单/投放  ponumber 唯一性检测

## 2021.06.29

* 新版接口V2版本:   优化字段类型检查、优化报错信息
* 新版接口V2配置信息:  请求地址 =>  .../soap/v2/index.php  wsdl文件地址 => .../soap/v2/wsdl.php

## 2021.06.21
* 修正接口: addSolution缺少字段ponumber
* 修正接口: banner相关接口中字段targeturl 应该为string类型
* 移除接口: 移除无效接口getSolutionStatus

## 2021.06.07

* 新增接口参数: 新建/编辑投放 (solution)时， 增加参数pubdate，用来设置详细排期
* 新增接口: 根据ponumber获取单个活动 => getCampaignByPonumber
* 新增接口: 根据ponumber获取单个订单 => getOrderByPonumber
* 新增接口: 根据ponumber获取单个投放 => getSolutionByPonumber
* 修正：editCampaignByPonumber/ editOrderByPonumber / editSolutioniByPonumber 接口参数中去除 多余的 ponumber 参数
* 修正：editOrderByPonumber / editSolutionByPonumber 无法调用

## 2021.04.02 

* 新增字段: 活动 (campaign) 增加ponumber字段
* 新增接口: 根据ponumber修改活动数据 => editCampaignByPonumber
* 新增接口: 根据ponumber修改订单数据 => editOrderByPonumber
* 新增接口: 根据ponumber修改投放数据 => editSolutionByPonumber

# 文档说明
## 传输协议
* 采用SOAP通信协议
请将传漾提供的WSDL文件url引用到客户端代码中。WSDL文件将提供该文档中各个接口的细节描述。

* 数据编码格式为 UTF-8
非utf8编码的中文字符在传递到接口时，请先转码为utf8格式

* 身份验证
soap请求头需要含有传漾提供的授权码，授权请求关键字 SOAP_AUTH
SoapHead 验证格式示例:   
`<SOAP-ENV:Header><ns1:SOAP_AUTH>xxxxxx</ns1:SOAP_AUTH></SOAP-ENV:Header>`

## 异常描述
|CODE|description|
| -------- | -------- |
|501 |unknow exception|
|502 |unknow exception|
|503 |core error|
|504 |code error|
|514 |user authenticate unsuccessful|
|515 |cannot authenticate|
|516 |soap service disabled|
|521 |ponumber exist|
|522 |ponumber doesn't exist|
|533 |campaign id doesn't exist|
|541 |order name exist|
|542 |order status wrong|
|543 |order id wrong|
|551 |solution empty pubdate|
|552 |solution name exist|
|553 |solution status wrong|
|554 |fromdate format wrong|
|555 |todate format wrong|
|556 |solution id wrong|
|561 |banner id wrong|
|562 |params check error|
|571 |website id wrong|
|581 |channelgroup id wrong|
|591 |channel id wrong|
|592 |channel name exist|
|602 |date format error|
|603 |schedule format error|

# API接口

## 广告活动

### addCampaign - 新建广告活动

输入参数描述

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| info  | Campaign 对象 (详见下方)  | 是 | |

Campaign 对象

| 参数 | 类型 | 必填 | 默认值 | 描述 |
| -------- | -------- |  -------- |  -------- | -------- |
| name | string  | 是  |  | 广告活动名称 |
| memo | string  | 否 | 空 | 备注信息 |

返回数据描述

Campaign(广告活动)的ID  (类型: int)

### editCampaign - 编辑广告活动

输入参数描述

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| id | int    | 是  |   广告活动ID  |
| info | Campaign 对象 (详见下方)  | 是  |  |

Campaign 对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- |   -------- | -------- |
| name | string  | 否  | 广告活动名称 |
| memo | string  | 否 | 备注信息 |
| ponumber | string | 否 | 广告活动外部编号 |

返回数据描述

是否成功 (类型: boolean)

### editCampaignByPonumber -根据Ponumber 编辑广告活动

输入参数描述

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| ponumber | string    | 是  |   广告活动外部编号  |
| info | Campaign 对象 (详见下方)  | 是  |  |

Campaign 对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- |   -------- | -------- |
| name | string  | 否  | 广告活动名称 |
| memo | string  | 否 | 备注信息 |

返回数据描述

是否成功 (类型: boolean)

### getCampaign - 获取单个广告活动

输入参数描述

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| id  | int   | 是   |  广告活动ID  |

返回数据描述

Campaign(广告活动) 对象

### getCampaignByPonumber - 根据Ponumber获取单个广告活动

输入参数描述

| 参数     | 类型   | 必填 | 描述             |
| -------- | ------ | ---- | ---------------- |
| ponumber | string | 是   | 广告活动Ponumber |

返回数据描述

Campaign(广告活动) 对象

### getCampaignList - 获取广告活动列表

输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| info  | ResourceSearch(搜索条件对象) 详见下方  | 是   |    |

搜索条件对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| kw | string | 否 | 关键字 |


返回数据描述： 

| 参数 | 类型 | 描述 |
| -------- | -------- | -------- |
| count  | int |  结果数  |
| data  | array: 由多个Campain(广告活动) 对象组成 $Campaign$ |  数据集  |



## 广告订单

### addOrder - 新建广告订单

输入参数描述

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| info  | Order 对象 (详见下方)  | 是 | |

Order 对象

| 参数 | 类型 | 必填 | 默认值 | 描述 |
| -------- | -------- |  -------- |  -------- | -------- |
| name | string  | 是  |  | 广告订单名称 |
| status | int | 否 | 1 | 状态：2表示归档，1表示有效，0表示无效 |
| campaignid   | int  | 是 | | 所属广告活动ID |
| fromdate | string   | 是 | | 订单开始日期，格式"YYYY-MM-DD" |
| todate | string | 是 | | 订单结束日期，格式"YYYY-MM-DD" |
| ponumber | string | 否 | 空 | 订单外部编号 |

返回数据描述

Order(广告订单)的ID  (类型: int)

### editOrder - 编辑广告订单

输入参数描述

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| id | int    | 是  |   广告订单ID  |
| info | Order 对象 (详见下方)  | 是  |  |

Order 对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- |   -------- | -------- |
| name | string  | 否  | 广告订单名称 |
| status | int | 否 | 状态：2表示归档，1表示有效，0表示无效 |
| campaignid   | int  | 否 | 所属活动ID |
| fromdate | string  | 否 | 订单开始日期，格式"YYYY-MM-DD" |
| todate | string | 否 | 订单结束日期，格式"YYYY-MM-DD" |
| ponumber | string | 否 | 订单外部编号 |

返回数据描述

是否成功 (类型: boolean)

### editOrderByPonumber - 根据Ponumber编辑广告订单

输入参数描述

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| ponumber | string    | 是  |   广告订单外部编号  |
| info | Order 对象 (详见下方)  | 是  |  |

Order 对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- |   -------- | -------- |
| name | string  | 否  | 广告订单名称 |
| status | int | 否 | 状态：2表示归档，1表示有效，0表示无效 |
| campaignid   | int  | 否 | 所属活动ID |
| fromdate | string  | 否 | 订单开始日期，格式"YYYY-MM-DD" |
| todate | string | 否 | 订单结束日期，格式"YYYY-MM-DD" |

返回数据描述

是否成功 (类型: boolean)

### getOrder - 获取单个广告订单

输入参数描述

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| id  | int   | 是   |  广告订单ID  |

返回数据描述

Order(广告订单) 对象

### getOrderByPonumber - 根据Ponumber获取单个广告订单

输入参数描述

| 参数     | 类型   | 必填 | 描述             |
| -------- | ------ | ---- | ---------------- |
| ponumber | string | 是   | 广告订单Ponumber |

返回数据描述

Order(广告订单) 对象

### getOrderList - 获取广告订单列表

输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| info  | ResourceSearch(搜索条件对象) 详见下方  | 是   |    |

搜索条件对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| kw | string | 否 | 关键字 |


返回数据描述： 

| 参数 | 类型 | 描述 |
| -------- | -------- | -------- |
| count  | int |  结果数  |
| data  | array: 由多个Order(广告订单) 对象组成  |  数据集  |

## 广告投放
### addSolution - 新建广告投放

输入参数描述：

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| info  | 对象: Solution (广告投放) 详见下方表格 | 是   |  传递一整个 Solution (广告投放) 对象 |

Solution 对象

| 参数 | 类型 | 必填 | 默认值 | 描述 |
| -------- | -------- | -------- | -------- | -------- |
| name | string |  是 | | 投放名称 |
| status | int | 否 | 1 | 状态：2表示归档，1表示有效，0表示无效 |
| orderid | int | 是 | | 所属订单ID |
| channelid | string |  是 | | 投放目标广告位ID (多个用英文逗号隔开) |
| priority   | int | 否 | 40 | 投放优先级 |
| location  | string | 否 | 空 | 地域定向 |
| fromdate | string | 是 | | 投放开始日期，格式"YYYY-MM-DD" |
| todate   | string | 是 | | 投放结束日期，格式"YYYY-MM-DD" |
| pubdate | string | 否 |空 | 详细排期设置，格式"YYYY-MM-DD HH:ii:ss\~YYYY-MM-DD HH:ii:ss\|YYYY-MM-DD HH:ii:ss~YYYY-MM-DD HH:ii:ss"  例: "2021-06-10 12:00:00~2021-06-12 06:00:00\|2021-06-20 08:00:00~2021-06-20 22:00:00" |
| saletype  | string | 是 | | 广告位售卖方式 (cpd / cpm / cpc) |
| cpmcount  | int | 否 | 0 | cpm方式下售卖的量，精确到每个显示量 (saletype = cpm，才需要填写) |
| cpccount  | int | 否 | 0 | cpc方式下售卖的量，精确到每个显示量 (saletype = cpc，才需要填写) |
| frequency  | int | 否 | 0 |  频次，次数 |
| burnout   | int | 否 | 0 | 循环时间，值表示多少秒循环一次 |
| interval   | int | 否 | 0 | 频次间隔 |
| asap   | int  | 否 | 0 | 尽快播放，0为平均，1为尽快 |
| keyword | string  | 否 | 空 | 关键字定向 |
| targeturl | string | 否 | 空 | 点击地址 |
| bannerimage | string | 否 | 空 | 若传值则自动为该投放建立一个创意。仅限banner形式广告位。 |
| ponumber | string |  否 | 空 | 投放外部编号 |

返回数据描述：

Solution (广告投放) 的ID  (类型: int)

### editSolution - 编辑广告投放

输入参数描述：

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| id | int    | 是 |   广告投放ID  |
| info  | 对象 Solution (广告投放)  | 是   | 传递一整个 Solution (广告投放) 对象 |

Solution 对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| name | string |  否 | 投放名称 |
| status | int |  否 | 状态：2表示归档，1表示有效，0表示无效 |
| orderid | int |  否 | 所属订单ID |
| channelid | string |  否 | 投放目标广告位ID (多个用英文逗号隔开) |
| priority   | int |  否 | 投放优先级 |
| location  | string |  否 | 地域定向 |
| fromdate | string |  否 | 投放开始日期，格式"YYYY-MM-DD" |
| todate   | string |  否 | 投放结束日期，格式"YYYY-MM-DD" |
| pubdate | string | 否 |详细排期设置，格式"YYYY-MM-DD HH:ii:ss~YYYY-MM-DD HH:ii:ss\|YYYY-MM-DD HH:ii:ss~YYYY-MM-DD HH:ii:ss"  例: "2021-06-10 12:00:00~2021-06-12 06:00:00\|2021-06-20 08:00:00~2021-06-20 22:00:00" |
| saletype  | string |  否 | 广告位售卖方式 (cpd / cpm / cpc) |
| cpmcount  | int |  否 | cpm方式下售卖的量，精确到每个显示量 (saletype = cpm，才需要填写) |
| cpccount  | int |  否 | cpc方式下售卖的量，精确到每个显示量 (saletype = cpc，才需要填写) |
| frequency  | int |  否 | 频次，次数 |
| burnout   | int |  否 | 循环时间，值表示多少秒循环一次 |
| interval   | int |  否 | 频次间隔 |
| asap   | int |  否 | 尽快播放，0为平均，1为尽快 |
| keyword | string |  否 | 关键字定向 |
| targeturl | string |  否 | 点击地址 |
| bannerimage | string |  否 | 若传值则自动为该投放建立一个创意。仅限banner形式广告位。 |
| ponumber | string |  否 | 投放外部编号 |

返回数据描述：

布尔值 (类型: Boolean)

### editSolutionByPonumber -根据Ponumber 编辑广告投放

输入参数描述：

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| ponumber | string | 是 |   广告投放外部编号  |
| info  | 对象 Solution (广告投放)  | 是   | 传递一整个 Solution (广告投放) 对象 |

Solution 对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| name | string |  否 | 投放名称 |
| status | int |  否 | 状态：2表示归档，1表示有效，0表示无效 |
| orderid | int |  否 | 所属订单ID |
| channelid | string |  否 | 投放目标广告位ID (多个用英文逗号隔开) |
| priority   | int |  否 | 投放优先级 |
| location  | string |  否 | 地域定向 |
| fromdate | string |  否 | 投放开始日期，格式"YYYY-MM-DD" |
| todate   | string |  否 | 投放结束日期，格式"YYYY-MM-DD" |
| pubdate | string | 否 |详细排期设置，格式"YYYY-MM-DD HH:ii:ss~YYYY-MM-DD HH:ii:ss\|YYYY-MM-DD HH:ii:ss~YYYY-MM-DD HH:ii:ss"  例: "2021-06-10 12:00:00~2021-06-12 06:00:00\|2021-06-20 08:00:00~2021-06-20 22:00:00" |
| saletype  | string |  否 | 广告位售卖方式 (cpd / cpm / cpc) |
| cpmcount  | int |  否 | cpm方式下售卖的量，精确到每个显示量 (saletype = cpm，才需要填写) |
| cpccount  | int |  否 | cpc方式下售卖的量，精确到每个显示量 (saletype = cpc，才需要填写) |
| frequency  | int |  否 | 频次，次数 |
| burnout   | int |  否 | 循环时间，值表示多少秒循环一次 |
| interval   | int |  否 | 频次间隔 |
| asap   | int |  否 | 尽快播放，0为平均，1为尽快 |
| keyword | string |  否 | 关键字定向 |
| targeturl | string |  否 | 点击地址 |
| bannerimage | string |  否 | 若传值则自动为该投放建立一个创意。仅限banner形式广告位。 |

返回数据描述：

布尔值 (类型: Boolean)

### getSolution - 获取单个广告投放
输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| id  | int   | 是   |  广告投放ID  |

返回数据描述： 

对象: Solution (广告投放)

### getSolutionByPonumber - 根据Ponumber获取单个广告投放

输入参数描述:

| 参数     | 类型   | 必填 | 描述             |
| -------- | ------ | ---- | ---------------- |
| ponumber | string | 是   | 广告投放ponumber |

返回数据描述： 

对象: Solution (广告投放)

### getSolutionList - 获取广告投放列表

输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| info  | ResourceSearch(搜索条件对象) 详见下面表格  | 是   |    |

搜索对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- |  ------- | -------- |
| kw | string | 否 | 关键字 |
| campaignid | string | 否 | 活动id |
| orderid | string | 否 | 订单id |
| channelid | string | 否 | 广告位id |
| status | string | 否 | 状态：2表示归档，1表示有效，0表示无效 |



返回数据描述： 

| 参数 | 类型 | 描述 |
| -------- | -------- | -------- |
| count  | int |  结果数  |
| data  | array:  由多个Solution(广告投放)对象组成  |  数据集  |

## 广告创意

### addBanner - 新建广告创意

输入参数描述：

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| info  | 对象: Banner (广告创意) 详见下方表格   | 是 | 传递一整个 Banner (广告创意)对象  |

Banner 对象

| 参数 | 类型 | 必填 | 默认值 | 描述 |
| -------- | -------- | -------- | -------- | -------- |
| name  | string | 是 | | 创意名称 |
| status   | int | 否 | 1 | 状态：2表示归档，1表示有效，0表示无效 |
| solutionid   | int | 是 | | 所属投放ID |
| weight  | int | 否 | 10 |  |
| targeturl   | string | 否 |  空 | 点击地址 |
| bannerimage  | string | 否 | 空 | 素材地址:url格式,支持素材类型:jpg,gif,png,swf |
| html   | string | 否 | 空 | 自定义创意模板，支持宏变量，[ADSAMECLICK]]表示加监测点击地址 |



返回数据描述：

Banner (广告创意)的ID  (类型: int)

### editBanner - 编辑广告创意

输入参数描述：

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| id | int    | 是    |   广告创意ID  |
| info  | 对象: Banner (广告创意)    |  对象中的字段 选填  | 传递一整个 Banner (广告创意)对象   |

Banner 对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| name  | string | 否 | 创意名称 |
| status   | int | 否 | 状态：2表示归档，1表示有效，0表示无效 |
| weight  | int | 否 | 权重 |
| targeturl   | string | 否 | 点击地址 |
| bannerimage  | string | 否 | 素材地址:url格式,支持素材类型:jpg,gif,png,swf |
| html   | string | 否 | 自定义创意模板，支持宏变量，[ADSAMECLICK]]表示加监测点击地址 |

返回数据描述：

布尔值 (类型: Boolean)

### getBanner - 获取单个广告创意

输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| id  | int   | 是   |  广告创意ID  |

返回数据描述： 

对象: Banner (广告创意)



### getBannerList - 获取广告创意列表

输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| info  | ResourceSearch(搜索条件对象) 详见下面表格  | 是  |    |

搜索对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- |  ------- | -------- |
| kw | string | 否 | 关键字 |
| campaignid | string | 否 | 活动id |
| orderid | string | 否 | 订单id |
| solutionid | string | 否 | 投放id |
| channelid | string | 否 | 广告位id |
| status | string | 否 | 状态：2表示归档，1表示有效，0表示无效 |

返回数据描述： 

| 参数 | 类型 | 描述 |
| -------- | -------- | -------- |
| count  | int |  结果数  |
| data  | array: 由多个Banner(广告创意)对象组成  |  数据集  |

## 网站

### addWebsite - 新建网站

输入参数描述：

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| info  | 对象: Website (网站) 详见下方表格   | 是  | 传递一整个 Website (网站)对象  |

Website 对象

| 参数 | 类型 | 必填 | 默认值 | 描述 |
| -------- | -------- |  -------- |  -------- | -------- |
| name | string  | 是  |  | 网站名称 |
| memo | string  | 否 | 空 | 备注信息 |

返回数据描述：

Website (网站) 的ID  (类型: int)


### editWebsite - 编辑网站

输入参数描述：

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| id | int    | 是  |  网站ID  |
| info  | 对象: Website (网站) 详见下方表格  | 是   |  传递一整个 Website (网站)对象  |

Website 对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- |   -------- | -------- |
| name | string  | 否  | 活动名称 |
| memo | string  | 否 | 备注信息 |

返回数据描述：

布尔值 (类型: Boolean)


### getWebsite - 获取单个网站

输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| id  | int   |  是   |  网站ID  |

返回数据描述： 

对象: Website (网站)

### getWebsiteList - 获取网站列表

输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| info  | ResourceSearch(搜索条件对象) 详见下面表格  | 是   |    |

搜索对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| kw | string | 否 | 关键字 |


返回数据描述： 

| 参数 | 类型 | 描述 |
| -------- | -------- | -------- |
| count  | int |  结果数  |
| data  | array: 由多个Website (网站)对象组成  |  数据集  |

## 频道

### addChannelgroup - 新建频道

输入参数描述：

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| info  | 对象: Channelgroup (频道) 详见下方表格 | 是  | 传递一整个 Channelgroup (频道)对象  |

Channelgroup 对象

| 参数 | 类型 | 必填 | 默认值 | 描述 |
| -------- | -------- |  -------- |  -------- | -------- |
| name | string  | 是  |  | 网站名称 |
| status | int | 否 | 1 | 状态：2表示归档，1表示有效，0表示无效 |
| websiteid | int | 是 | | 所属网站ID |

返回数据描述：

Channelgroup (频道) 的ID  (类型: int)

### editChannelgroup - 编辑频道

输入参数描述：

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| id | int    | 是  | 频道ID  |
| info  | 对象: Channelgroup (频道) 详见下方表格  | 是   | 传递一整个 Channelgroup (频道)对象  |

Channelgroup 对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- |  -------- | -------- |
| name | string  | 否  | 频道名称 |
| status | int | 否 | 状态：2表示归档，1表示有效，0表示无效 |

返回数据描述：

布尔值 (类型: Boolean)

### getChannelgroup - 获取单个频道

输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| id  | int   | 是   |  频道ID  |

返回数据描述： 

对象: Channelgroup (频道)


### getChannelgroupList - 获取频道列表

输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| info  | ResourceSearch(搜索条件对象) 详见下面表格  | 是   |    |

搜索对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- |  ------- | -------- |
| kw | string | 否 | 关键字 |
| websiteid | string | 否 | 网站id |
| status | string | 否 | 状态：2表示归档，1表示有效，0表示无效 |

返回数据描述： 

| 参数 | 类型 | 描述 |
| -------- | -------- | -------- |
| count  | int |  结果数  |
| data  | array: 由多个Channelgroup (频道)对象组成  |  数据集  |

## 广告位

### addChannel - 新建广告位

输入参数描述：

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| info  | 对象: Channel (广告位) 详见下方表格  | 是  | 传递一整个 Channel (广告位)对象  |

Channel 对象

| 参数 | 类型 | 必填 | 默认值 | 描述 |
| -------- | -------- |  -------- |  -------- | -------- |
| name   | string | 是 | | 广告位名称 |
| status   | int | 否 | 1 | 状态：2表示归档，1表示有效，0表示无效 |
| channelgroupid | int | 是 | | 所属频道ID |
| width | int | 是 | | 宽度 |
| height | int | 是 | | 高度 |
| url | string | 否 | 空 | 链接 |
| memo | string | 否 | 空 | 备注信息 |


返回数据描述：

Channel (广告位) 的ID  (类型: int)


### editChannel - 编辑广告位

输入参数描述：

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| id | int    | 是  |  广告位ID  |
| info  | 对象: Channel (广告位) 详见下方表格  | 是   | 传递一整个 Channel (广告位)对象  |

Channel 对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- |  ------- | -------- |
| name   | string | 否 | 广告位名称 |
| status   | int | 否 | 状态：2表示归档，1表示有效，0表示无效 |
| channelgroupid | int | 否 | 所属频道ID |
| width | int | 否 | 宽度 |
| height | int | 否 | 高度 |
| url | string | 否 | 链接 |
| memo | string | 否 | 备注信息 |


返回数据描述：

布尔值 (类型: Boolean)


### getChannel - 获取单个广告位

输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| id  | int   | 是   |  广告位ID  |

返回数据描述： 

对象: Channel (广告位)

### getChannelList - 获取广告位列表

输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| info  | ResourceSearch(搜索条件对象) 详见下面表格  | 是  |    |

搜索对象

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- |  ------- | -------- |
| kw | string | 否 | 关键字 |
| websiteid | string | 否 | 网站id |
| channelgroupid | string | 否 | 频道id |
| status | string | 否 | 状态：2表示归档，1表示有效，0表示无效 |

返回数据描述： 

| 参数 | 类型 | 描述 |
| -------- | -------- | -------- |
| count  | int |  结果数  |
| data  | array: 由多个Channel (广告位)对象组成  |  数据集  |

## 报表相关

### getReport - 获取普通报表

输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| info  | ResourceSearch(搜索条件对象)  | 是   |    |

返回数据描述： 

| 参数 | 类型 | 描述 |
| -------- | -------- | -------- |
| count  | int |  结果数  |
| data  | array: 由多个Report (报表) 对象组成  |  数据集  |

### getRealtimeReport - 获取实时报表

输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| type  | string | 是   |  website: 网站报表，channelgroup: 频道报表，channel: 广告位报表，campaign: 活动报表，order: 订单报表，solution: 投放报表，banner: 创意报表。   |
| ids  | string | 是   |  要获取的数据报表的数据的id（多个id以逗号隔开）  |

返回数据描述： 

realtimeReportList 

## 其他

### getChannelCode - 取广告位代码

输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| id  | int  | 是   |  广告位ID  |
| type  | string |  否  | 广告代码格式,  默认值:js ,可选值：js / iframe / xml |

返回数据描述： 
类型：string
数据：dolphin对应广告位代码

### pushSetting - 同步数据

输入参数描述:

无

返回数据描述： 

布尔值 (Boolean)

### getMonitorCode - 获取监测代码

输入参数描述:

| 参数 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| sid  | int  | 是   |  投放ID  |

返回数据描述： 
monitorcode数组对象

# 数据对象

## Campaign - 广告活动

| 字段名 | 类型 | 描述 |
| -------- | --------  | -------- |
| ID   | int      | 广告活动ID |
| name   | string    | 广告活动名称 |
| memo   | string    | 广告活动备注 |
| ponumber | string | 广告活动外部编号 |

## Order - 广告订单

| 字段名 | 类型 | 描述 |
| -------- | -------- | ------- |
| id | int | 订单ID |
| name | string | 订单名称 |
| status | int | 状态：2表示归档，1表示有效，0表示无效 |
| campaignid   | int   | 所属活动ID |
| fromdate | string   | 订单开始日期，格式"YYYY-MM-DD" |
| todate | string | 订单结束日期，格式"YYYY-MM-DD" |
| ponumber | string | 订单外部编号 |

## Solution - 广告投放


| 字段名 | 类型 | 描述 |
| -------- | -------- | -------- |
| ID | int | 投放ID |
| name | string | 投放名称 |
| status | int | 状态：2表示归档，1表示有效，0表示无效 |
| campaignid   | int | 所属活动ID |
| orderid | int | 所属订单ID |
| channelid | string | 投放目标广告位ID (多个用英文逗号隔开) |
| priority   | int | 投放优先级 |
| location  | string | 地域定向 |
| fromdate | string | 投放开始日期，格式"YYYY-MM-DD" |
| todate   | string | 投放结束日期，格式"YYYY-MM-DD" |
| saletype  | string | 广告位售卖方式 (cpm/cpd) 默认cpd |
| cpmcount  | int | cpm方式下售卖的量，精确到每个显示量 |
| cpccount  | int | cpc方式下售卖的量，精确到每个显示量 |
| frequency  | int  | 频次，次数 |
| burnout   | int | 循环时间，值表示多少秒循环一次 |
| interval   | int | 频次间隔 |
| asap   | int  | 尽快播放，0为平均，1为尽快 |
| keyword | string  | 关键字定向 |
| targeturl | string | 点击地址 |
| bannerimage | string | 若传值则自动为该投放建立一个创意。仅限banner形式广告位。 |
| ponumber | string | 订单外部编号 |

<!--| advertise_ID | int | 广告主ID |-->
<!--| advertise_name | string | 广告主名称 | -->

## Banner - 广告创意


| 字段名 | 类型 | 描述 |
| -------- | -------- | -------- |
| ID   | int | 创意ID |
| name  | string | 创意名称 |
| status   | int | 状态：2表示归档，1表示有效，0表示无效 |
| solutionid   | int | 所属投放ID |
| fid   | int | 所属创意组(bannergroup)ID (前端不展示，可无视) |
| weight  | int | 权重 |
| targeturl   | <font color="red">string</font> | 点击地址 |
| bannerimage  | string | 素材地址:url格式,支持素材类型:jpg,gif,png,swf |
| html   | string | 自定义创意模板，支持宏变量，[ADSAMECLICK]]表示加监测点击地址 |


## Website - 网站



| 字段名 | 类型 | 描述 |
| -------- | -------- | -------- |
| ID | int  | 网站ID |
| name | string | 网站名称 |
| memo | string | 备注信息 |


<!-- | userid | int | 所属用户ID | -->

## Channelgroup - 频道


| 字段名 | 类型 |描述 |
| -------- | -------- | -------- |
| ID   | int | 频道ID |
| name | string | 频道名称 |
| status | int | 状态：2表示归档，1表示有效，0表示无效 |
| websiteid | int | 所属网站ID |

## Channel - 广告位


| 字段名 | 类型 | 描述 |
| -------- | -------- | -------- |
| ID  | int | 广告位ID |
| name   | string | 广告位名称 |
| status   | int | 状态：2表示归档，1表示有效，0表示无效 |
| websiteid | int | 所属网站ID |
| channelgroupid | int | 所属频道ID |
| width | int | 宽度 |
| height | int | 高度 |
| url | string | 链接 |
| memo | string | 备注信息 |

<!--  | adsizeid | int | 广告尺寸ID  <br/>一个adsizeid 对应一组width/height  |   -->

## ResourceSearch - 搜索条件对象

| 字段名 | 类型 | 描述 |
| -------- | -------- | -------- |
| kw | string | 关键字 |
| status | string | 状态：2表示归档，1表示有效，0表示无效 |
| type | string | 类型 |
| campaignid | string | 活动id |
| orderid | string | 订单id |
| solutionid | string | 投放id |
| websiteid | string | 网站id |
| channelgroupid | string | 频道id |
| channelid | string | 广告位id，按广告位id查询投放 |
| advertiseinfo | boolean | 是否返回广告主信息。为true时，solution对象advertise_name有内容。|
| limit | string | 导出limit值的数量的数据，由逗号分隔，前面数字表示从第几条数据开始，后一个数字表示需要多少条数据。（例如：0,2 表示从第一条开始取，取2条数据）|
| sort | string | 按sort值的字段排序 |

## reportSearch - 报表输入参数对象

| 字段名 | 类型 | 描述 |
| -------- | -------- | -------- |
| type | string	| 报表类型：base: 普通报表，hour: 小时报表，location: 省级地域报表，city: 城市地域报表。 |
| fromdate | string | 导出报表开始时间 |
| todate | string | 导出报表结束时间 |
| resource | string | 导出的数据类型：website: 网站报表，channelgroup: 频道报表，channel: 广告位报表，campaign: 活动报表，order: 订单报表,solution: 投放报表，banner: 创意报表。 |
| ids | string | 指定resource类型的数据id ，多id用逗号间隔 |
| ponumber | string | 外部编号，多个外部编号用逗号间隔 |
| limit | string | 导出limit值的数量的数据，由逗号分隔，前面数字表示从第几条数据开始，后一个数字表示需要多少条数据。（例如：0,2 表示从第一条开始取，取2条数据） |
| sort | string | 按sort值的字段排序 |

## report - 普通报表对象

| 字段名 | 类型 | 描述 |
| -------- | -------- | -------- |
| id   | int    | 当前资源id	|
| day	| string	| 日期	|
| hour	| Int	| 小时报表	|
| location	| string	| 省级地域报表	|
| city	| string	| 城市地域报表	|
| shows	| int	| 显示数	|
| clicks	| int	| 点击数	|
| uniqueshows	| int	| 唯一显示	|
| uniqueclicks	| int	| 唯一点击	|

## realtimeReportResult - 实时数据报表对象

| 字段名 | 类型 | 描述 |
| -------- | -------- | -------- |
| id | int |	实时数据的id |
| shows | int | 实时数据的总显示数 |
| clicks | int | 实时数据的总点击数 |
| hour | 详见realtimeReportList - 细分小时数据对象 | 细分每个小时的点击数和显示数 |

## realtimeReportList - 实时数据报表列表对象

| 字段名 | 类型 | 描述 |
| -------- | -------- | -------- |
| realtimeReportList | 详见 realtimeReportResult 对象 |	实时数据的id |

## monitorcode  - 监测代码对象

| 参数 | 类型 | 说明 |
| -------- | -------- | -------- |
| showcode  | string | 显示监测代码  |
| clickcode  | string | 点击监测代码 |
