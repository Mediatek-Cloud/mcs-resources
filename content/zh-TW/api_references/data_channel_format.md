# 資料通道格式

此章節將會說明所有資料通道的API格式，此格式為裝置和command server溝通的格式。

**此處使用UNIX timestamp時間格式，且非必要欄位。您可保持:Timestamp為空，此時時間點則會由MCS所收到資料點的時間。

MCS支持JSON以及CSV兩種格式的資料。


## 開關

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
0代表關，1代表開。

範例：

switch01,, 1

代表將switch01資料通道的狀態改為開，並且由系統自動帶入時間。

## 分類

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

Key value 的值將會對應至您所設定的Key name。

## 整數

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

## 浮點數

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

## 十六進位數

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
十六進位數的值為A-F以及0-9。

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

緯度範圍從 -90 至 90。 0 至 90 代表北緯，0 至 -90 代表南緯。

經度範圍從 -180 至 180。 0 至 180 代表東經，0 至 -180 代表西經。

高度範圍從 0 至 20000公尺。


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


CSV格式：
```
dataChannelId,timestamp,{Value},{Period}
```
