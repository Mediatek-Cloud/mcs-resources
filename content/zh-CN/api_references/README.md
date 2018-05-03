# API 参考手册

MediaTek Cloud Sandbox (MCS) 提供一系列的 RESTful APIs 让您能够便利的使用 MCS 服务，例如上传和读取资料点，或是透过 TCP socket 对装置下指令。MCS 亦能储存照时间排序的资料数列，并以图表化形式呈现。


## 请求网址（Request URL）

MCS 提供的各个服务皆位于此网址（URL）之下。

```
https://api.mediatek.com/mcs/v2/
```

您可透过在请求网址（URL）当中指定**资源 ID** 来使用该资源所提供的服务。以底下的请求为例，我们透过指定装置与资料通道的 ID（deviceID 与 dataChannelID）来使用 **datapoints** 相关的服务。

```
https://api.mediatek.com/mcs/v2/devices/{deviceID}/datachannels/{dataChannelID}/datapoints.csv
```

**范例**

以下为获取 **datapoints** 的完整请求（需将 {variable} 换成您的真实数据），在后续的章节中会有更详细的描述。

```
curl -X GET \
  https://api.mediatek.com/mcs/v2/devices/{deviceID}/datachannels/{dataChannelID}/datapoints.csv \
  -H 'devicekey: {deviceKey}' \
```

## 帐单方法（Request Method）

The MediaTek Cloud Sandbox (MCS)提供以下几种 API 请求方法：

* **GET** - 用來取得資源狀態。

* **POST** - 用來建立資源。

* **PUT** - 用來更新資源狀態。

* **DELETE** - 用來刪除資源。


## 请求表头（Request Header）
###1. 存取授权凭证（Access Token）

所有的 API 请求皆须被授权，因此您必须在请求表头当中带入授权凭证，才有权限存取对应的资源，进行对应的操作。MCS 开放的授权凭证主要有两种：

* **服务提供者（service provider）帐号**：
	
	如果您是自行开发应用程式，包括手机 App 或网站应用，您可以在个人档案页面中的服务提供者分页，申请取得 appId 以及 appSecret，使用此凭证存取 MCS 开放的所有 APIs。接着在所有 MCS 服务请求表头（request header）中带入 **appID** 与 **appSecret** 资讯。
	
	```
	appId: {your_appId}
	appSecret: {your_appSecret}
	```

* **装置金钥（device key）**:

	如果您开发的是装置端的应用，且只需要使用装置相关的服务 APIs，例如上传与获取资料点等，则您可直接使用装置 ID 与金钥作为认证。您可以在装置详情页面中找到装置 ID 与金钥，接着在所有 MCS 服务请求表头（request header）中带入 **deviceKey** 资讯。
		
	```
	deviceKey: {your_device_key}
	```
	由于装置 ID 已用于请求网址（request URL）中，用以指定所要存取的资源，因此不需再带入表头中。
	
###2. 内文格式（content-type）
您必须在请求表头中加上 **content-type** 这个栏位让 MCS 服务知道请求的内文格式并进行后续的处理与运算。

* `content-type: application/json` 表示内文为 JSON 格式。
* `content-type: text/csv` 表示内文为 CSV 格式。

## 请求内文（Request Body）

MCS 所支援的請求內文為 **JSON** 或 **CSV** 格式，不同的 APIs 服務所需要的參數皆不同，因此詳細的請求內容會在個別的 APIs 章節中介紹。

## 参数（Parameter）

以下介绍几个在使用 MCS APIs 时会用到的参数、格式以及代表意义。

* **时间戳（timestamp）**

	时间戳是用来记录一个资源被创建或更新的时间点，像是上传资料点当时的时间、产品原型被建立的时间等。在 MCS 系统中，时间是用 **Unix Epoch** 格式来表示，时间单位为毫秒（millisecond）。若您需要将 Unix Epoch 时间转换成可读性较高的常规表示法，可参考 [http://www.epochconverter.com/](http://www.epochconverter.com/)，例如：
	
	> *Timestamp in milliseconds: 1524720177000*
	> 可转换成
	> *Human time (GMT): Thursday, April 26, 2018 5:22:57 AM*
	
* **资源 ID**

	每次当一个产品原型、测试装置、资料通道或是韧体档案被建立后，都会有一个不重复的 ID 被指派给该资源。这个不重复的 ID 是不可编辑的，您可透过它存取该资源。
	
	举例来说，如欲从 MCS 取得某一资料通道的上传数据，您必须先知道此资料通道 ID 以及所属的测试装置 ID，并将其带入 HTTP 请求中以指定所要存取的资源。以下为三个 MCS 主要的资源类型。
	
	1. **资料通道**：一个资料通道是一个能够传送从装置回传的资料至 MCS 平台，或是能够将指令从 MCS 平台传达至装置的通道。简单来说，资料通道是一个云和装置之间单方向或是双方向的沟通管道。MCS 提供了许多 APIs 让使用者能够快速的存取资料通道上的资料点。
	
	2. **装置**：在 MCS 平台上有两种种类的装置，其中第一种是测试装置。测试装置为在商品上市前，开发者可以用来测试开发结果的装置。第二种装置为商转后大量给终端使用者实际使用的装置。MCS 提供了许多 APIs 让开发者和其他使用者能够快速的存取资料通道上的资料点，或是远端控制装置状态。
	
	3. **产品原型**：产品原型是您将来要交付的终端商品。MCS 提供了许多 APIs 让使用者能够使用。开发者能在产品原型页面中开发产品，例如新增资料通道并建立测试装置来测试确保之后商转功能。

## 回覆代码（Response Code）

Mediatek Cloud Sandbox (MCS) 使用标准 HTTP 状态来表达 API 请求的成功与否。以下是您呼叫 MCS API 有可能遇到的 HTTP 状态：

**200 OK** - 请求成功。

**201 Created**- 请求成功，并且新资源已建立。

**202 Accepted** - 请求成功，但尚未完成。

**204 No Content** - 请求成功，但伺服器无回应任何内容。通常是删除特定资源的请求回覆。

**400 Bad Request** - 伺服器无法处理请求，由于客户端给的参数错误。

**401 Unauthorized** - 无提供授权或授权失败。需要提供授权的表头。

**403 Forbidden** - 伺服器拒绝对一个不合格的请求做回覆。

**404 Not Found** - 请求的资源不存在。

**405 Method Not Allowed** - 请求的方法不支援。

**500, 502 Server Error** - MCS伺服器错误。
