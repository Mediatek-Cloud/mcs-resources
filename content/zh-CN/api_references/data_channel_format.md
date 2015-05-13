# 资料通道格式

此章节将会说明所有资料通道的API格式，此格式为装置和command server沟通的格式。


# 资料通道格式

此章节将会说明所有资料通道的API格式，此格式为装置和command server沟通的格式。

**此处使用UNIX timestamp时间格式，且非必要栏位。您可保持:Timestamp为空，此时时间点则会由MCS所收到资料点的时间。

MCS支持JSON以及CSV两种格式的资料。

## 开关

JSON格式：
```
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


CSV格式：
```
dataChannelId,timestamp,{0 or 1}

```
0代表关，1代表开。

范例：

switch01,, 1

代表将switch01资料通道的状态改为开，并且由系统自动带入时间。

## 分类

JSON格式：
```
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


CSV格式：
```
dataChannelId,timestamp,{Key Value}
```
Key value 的值将会对应至您所设定的Key name。

## 整数

JSON格式：
```
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


CSV格式：
```
dataChannelId,timestamp,{Integer}
```

## 浮点数

JSON格式：
```
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


CSV格式：
```
dataChannelId,timestamp,{Float}
```

## 十六进位数

JSON格式：
```
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


CSV格式：
```
dataChannelId,timestamp,{Hex value}
```
十六进位数的值为A-F以及0-9。

## 字串

JSON格式：
```
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


CSV格式：
```
dataChannelId,timestamp,{string}
```

## GPS

JSON格式：
```
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

CSV格式：

```
dataChannelId,timestamp,{latitude},{longitude},{altitude}
```

纬度范围从 -90 至 90。 0 至 90 代表北纬，0 至 -90 代表南纬。

经度范围从 -180 至 180。 0 至180 代表东经，0 至-180 代表西经。

高度范围从 0 至 20000公尺。

## GPIO

JSON格式：
```
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


CSV格式：
```
dataChannelId,timestamp,{0 ot 1}
```
0代表低，1代表高。

## PWM
JSON格式：
```
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


CSV格式
```
dataChannelId,timestamp,{Value},{Period}
```
