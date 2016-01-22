# 资料通道格式

此章节将会说明所有资料通道的 API 格式，此格式为装置和 command server 沟通的格式。

**此处使用 UNIX timestamp 时间格式，且非必要栏位。您可保持 Timestamp 为空，此时时间点则会由 MCS 所收到资料点的时间。

MCS 支持 JSON 以及 CSV 两种格式的资料。
。

## 开关

JSON 格式：

```
{
 "datapoints":[
      {
         "dataChnId":"dataChnId",
         "values":{
            "value":"{0 or 1}"
         }
      }
   ]
}

```


CSV 格式：

```
dataChnId,timestamp,{0 or 1}

```
0 代表关，1 代表开。

范例：

switch01,, 1

代表将 switch01 资料通道的状态改为开，并且由系统自动带入时间。

## 分类

JSON 格式：

```
{
 "datapoints":[
      {
         "dataChnId":"dataChnId",
         "values":{
            "value":"{Key value}"
         }
      }
   ]
}

```


CSV 格式：

```
dataChnId,timestamp,{Key Value}
```
Key value 的值将会对应至您所设定的 Key name。

## 整数

JSON 格式：

```
{
 "datapoints":[
      {
         "dataChnId":"dataChnId",
         "values":{
            "value":"{Integer value}"
         }
      }
   ]
}

```


CSV 格式：

```
dataChnId,timestamp,{Integer}
```

## 浮点数

JSON 格式：

```
{
 "datapoints":[
      {
         "dataChnId":"dataChnId",
         "values":{
            "value":"{Float value}"
         }
      }
   ]
}

```


CSV 格式：

```
dataChnId,timestamp,{Float}
```

## 十六进位数

JSON 格式：

```
{
 "datapoints":[
      {
         "dataChnId":"dataChnId",
         "values":{
            "value":"{HEX value}"
         }
      }
   ]
}

```


CSV 格式：

```
dataChnId,timestamp,{Hex value}
```
十六进位数的值为 A-F 以及 0-9。

## 字串

JSON 格式：

```
{
 "datapoints":[
      {
         "dataChnId":"dataChnId",
         "values":{
            "value":"{string value}"
         }
      }
   ]
}

```


CSV 格式：

```
dataChnId,timestamp,{string}
```

## GPS

JSON 格式：

```
{
 "datapoints":[
       {
         "dataChnId":"dataChnId",
         "values":{
            "latitude":"{latitude value}",
            "longitude":"{longitude value}",
            "altitude":"{altitude value}"
         }
      }
   ]
}

```

CSV 格式：

```
dataChnId,timestamp,{latitude},{longitude},{altitude}
```

纬度范围从 -90 至 90。 0 至 90 代表北纬，0 至 -90 代表南纬。

经度范围从 -180 至 180。 0 至180 代表东经，0 至-180 代表西经。

高度范围从 -20000 至 20000公尺。

## GPIO

JSON 格式：

```
{
 "datapoints":[
      {
         "dataChnId":"dataChnId",
         "values":{
            "value":"{0 or 1}"
         }
      }
   ]
}

```


CSV 格式：

```
dataChnId,timestamp,{0 ot 1}
```
0 代表低，1 代表高。

## PWM
JSON 格式：

```
{
 "datapoints":[
      {
         "dataChnId":"dataChnId",
         "values":{
            "value":"{string value}",
            "period":"{period value}"
         }
      }
   ]
}

```
PWM的值和期间只能为0至1000之间。


CSV 格式

```
dataChnId,timestamp,{Value},{Period}
```

## 类比

JSON 格式：

```
{
 "datapoints":[
      {
         "dataChnId":"dataChnId",
         "values":{
            "value":"{Integer value}"
         }
      }
   ]
}

```


CSV 格式：

```
dataChnId,timestamp,{Integer value}
```
整数的范围需由使用者自行定义

## 游戏控制器
JSON 格式：

```
{
 "datapoints":[
      {
         "dataChnId":"dataChnId",
         "values":{
            "value":"{up/down/right/left/A/B value| press(1) or release(0)}"
         }
      }
   ]
}

```

CSV 格式：

```
dataChnId,timestamp,{up/down/right/left/A/B value| press(1) or release(0)}
```
使用者可以决定是否同时给上下左右的值和AB键的值。

举例来说，若使用在建立游戏控制器资料通道时，将上的值设为 up，当使用者点上时，对应的值为 `up|0`。若长按 up，对应的值则为 `up|1`。

您可以使用预设的键盘热键如下：


`上= W`

`下= S`

`左= A`

`右= D`

`键A =`

`键B =.`

## 图片

JSON 格式:
```
{
 "datapoints":[
      {
         "dataChnId":"dataChnId",
         "values":{
            "value":"{image file base64 encoding string value}"
         }
      }
   ]
}

```

CSV 格式:
```
dataChnId,timestamp,{image file base64 encoding string value}
```
在上传图片档案至 MCS 之前,您必须先将图片档案转为 base64 编码的字串。上传此字串至图片资料通道后,此图片将会被储存与显示。

请注意,目前图片资料通道支援 JPG、JPEG、和 PNG 三种图片档案格式。一旦上传至 MCS  后,则都会被储存为 PNG 档案格式。

## 视频流

有别于其他资料通道，可以透过上传 CSV 或是 JSON 格式的资料更新资料点，您在使用影像串流前必须先在设备上安装视频转换器套件。

以下是目前 MCS 所支援的视频流规格

* 视频格式：MPEG1
* 最大解析度：320x240
* 最大画面更新率：30 fps
* MCS 视频流服务器：

```
http://stream.mcs.mediatek.com:80/:deviceId/:deviceKey/:dataChnId/:width/:height
```
请将其中的 deviceId, deviceKey, dataChnId, width 和 height 更换成您设备上实际的数据。其中 width 与 height 是上载视频流时所设定的解析度大小。
	
* 在 LinkIt Smart 7688 上建议的视频转换器套件：FFmpeg

```
ffmpeg -s 176x144 -f video4linux2 -r 30 -i /dev/video0 -f mpeg1video -r 30 -b 800k http://stream.mcs.mediatek.com:80/:deviceId/:deviceKey/:dataChnId/176/144
```