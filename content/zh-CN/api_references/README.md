# API 参考资料集

MediaTek Cloud Sandbox (MCS)提供一系列的 RESTful API 让您能够便利的使用，例如上传和读取资料点，或是透过 TCP socket 对装置下指令。 MCS亦能储存照时间排序的资料数列，并以图表化形式呈现给您。

## Request URL

您可以透过以下网址来叫用 MCS API：

```
https://api.mediatek.com/v2
```

## 参数

跟在连接点后的参数用来在URL路径内，定义特定的资源：

```
https://api.mediatek.com/v2/devices/{deviceId}/retrieveDataPoints

```
在上方的范例中，您可以看到deviceId在URL中被定义了。在任何的API 请求中，不是以URL形式传送的参数，都必须定义以JSON或是CSV格式包装。您必须定义一个`content -Type` header 为`application/json` 或是`text/csv`。


## 客户端错误

MediaTek Cloud Sandbox (MCS) 使用标准HTTP状态来表达 API 请求的成功或是错误。以下是您呼叫 MCS API 有可能遇到的HTTP状态：

**200 OK** - 请求成功。

**201 Created ** - 请求成功，并且新资源已建立。

**202 Accepted** - 请求成功，但尚未完成。

**204 No Content** - 请求成功，但伺服器无回应任何内容。通常是删除特定资源的请求回覆。

**400 Bad Request** - 伺服器无法处理请求，由于客户端给的参数错误。

**401 Unauthorized** - 无提供授权或授权失败。需要提供授权的 header。

**403 Forbidden** - 伺服器拒绝对一个不合格的请求做回覆。

**404 Not Found** - 请求的资源不存在。

**405 Method Not Allowed** - 请求的方法不支援。

**500, 502 Server Error** - MCS伺服器错误。


## HTTP 请求方式

The Mediatek Cloud Sandbox (MCS) 提供以下型式的 API 请求方式：


**GET** - 用来取得资源状态。

**POST** - 用来建立资源。

**PUT** - 用来更新资源状态。

**DELETE** - 用来删除资源。



##  授权

所有的API请求皆须被授权。您必须有一个 header `Authentication` 为您的 Bearer token。如果未提供此授权码，系统则会回覆您无授权讯息。

## 资源 ID

每次当一个产品原型，资料通道或是测试装置被建立后，都会有一个独特的ID 被指派给该资源。这个独特的 ID 是不可编辑的，且您将再存取此资源时用到。您无法存取您无 ID 的资源。

举例来说，如欲从 MCS 取得某一资料通道的资料，您必须拥有此资料通道以及所述测试装置的资源 ID。


## 资源

以下是您使用 MCS 时，会时常使用到的词汇：

### 资料通道

一个资料通道是一个能够传送从装置回传的资料至 MCS 平台，或是能够将指令从 MCS 平台传达至装置的通道。简单来说，资料通道是一个云和装置之间单方向或是双方向的沟通管道。

MCS提供了许多 API 让使用者能够快速的存取资料通道上得资料点。

### 装置

在 MCS 平台上有两种种类的装置，其中第一种是测试装置。测试装置为在商品上市前，开发者可以用来测试开发结果的装置。第二种装置为商转后大量给终端使用者实际使用的装置。

MCS 提供了许多 API 让开发者和其他使用者能够快速的存取资料通道上得资料点，或是远端控制装置状态。

### 产品原型

产品原型是您将来要交付的终端商品。  MCS 提供了许多 API 让使用者能够使用。开发者能在产品原型页面中开发产品，例如新增资料通道并建立测试装置来测试确保之后商转功能。


