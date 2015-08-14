# 资料通道格式

此章节将会说明所有资料通道的 API 格式，此格式为装置和 command server 沟通的格式。


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
         "dataChnId":"dataChanId",
         "values":{
            "value":"{0 or 1}"
         }
      }
   ]
}

```


CSV 格式：
```
dataChannelId,timestamp,{0 or 1}

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
         "dataChnId":"dataChanId",
         "values":{
            "value":"{Key value}"
         }
      }
   ]
}

```


CSV 格式：
```
dataChannelId,timestamp,{Key Value}
```
Key value 的值将会对应至您所设定的 Key name。

## 整数

JSON 格式：
```
{
 "datapoints":[
      {
         "dataChnId":"dataChanId",
         "values":{
            "value":"{Integer value}"
         }
      }
   ]
}

```


CSV 格式：
```
dataChannelId,timestamp,{Integer}
```

## 浮点数

JSON 格式：
```
{
 "datapoints":[
      {
         "dataChnId":"dataChanId",
         "values":{
            "value":"{Float value}"
         }
      }
   ]
}

```


CSV 格式：
```
dataChannelId,timestamp,{Float}
```

## 十六进位数

JSON 格式：
```
{
 "datapoints":[
      {
         "dataChnId":"dataChanId",
         "values":{
            "value":"{HEX value}"
         }
      }
   ]
}

```


CSV 格式：
```
dataChannelId,timestamp,{Hex value}
```
十六进位数的值为 A-F 以及 0-9。

## 字串

JSON 格式：
```
{
 "datapoints":[
      {
         "dataChnId":"dataChanId",
         "values":{
            "value":"{string value}"
         }
      }
   ]
}

```


CSV 格式：
```
dataChannelId,timestamp,{string}
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
dataChannelId,timestamp,{latitude},{longitude},{altitude}
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
         "dataChnId":"dataChanId",
         "values":{
            "value":"{0 or 1}"
         }
      }
   ]
}

```


CSV 格式：
```
dataChannelId,timestamp,{0 ot 1}
```
0 代表低，1 代表高。

## PWM
JSON 格式：
```
{
 "datapoints":[
      {
         "dataChnId":"dataChanId",
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
dataChannelId,timestamp,{Value},{Period}
```
