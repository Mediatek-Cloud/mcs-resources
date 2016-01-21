# 資料通道格式

此章節將會說明所有資料通道的 API 格式，此格式為裝置和 command server 溝通的格式。

**此處使用 UNIX timestamp 時間格式，且非必要欄位。您可保持 Timestamp 為空，此時時間點則會由 MCS 所收到資料點的時間。

MCS 支持 JSON 以及 CSV 兩種格式的資料。


## 開關

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
0 代表關，1 代表開。

範例：

switch01,, 1

代表將 switch01 資料通道的狀態改為開，並且由系統自動帶入時間。

## 分類

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

Key value 的值將會對應至您所設定的 Key name。

## 整數

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

## 浮點數

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

## 十六進位數

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
十六進位數的值為 A-F 以及 0-9。

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

緯度範圍從 -90 至 90。 0 至 90 代表北緯，0 至 -90 代表南緯。

經度範圍從 -180 至 180。 0 至 180 代表東經，0 至 -180 代表西經。

高度範圍從 -20000 至 20000 公尺。


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
PWM的值和期間只能為 0 至 1000 之間。

CSV 格式：

```
dataChnId,timestamp,{Value},{Period}
```

## 類比
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
整數的範圍需由使用者自行定義


## 遊戲控制器
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
dataChnId,timestamp,{up/down/right/left/A/B value|press(1) or release(0)}
```
使用者可以決定是否同時給上下左右的值和 AB 鍵的值。

舉例來說，若使用在建立遊戲控制器資料通道時，將上的值設為 up，當使用者點上時，對應的值為 `up|0`。若長按 up，對應的值則為 `up|1`。

您可以使用預設的鍵盤熱鍵如下：


`上 = W`

`下 = S`

`左 = A`

`右 = D`

`鍵 A = ,`

`鍵 B = .`

## 圖片

JSON 格式：

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


CSV 格式：

```
dataChnId,timestamp,{image file base64 encoding string value}
```
在上傳圖片檔案至 MCS 之前，您必須先將圖片檔案轉為 base64 編碼的字串。上傳此字串至圖片資料通道後，此圖片將會被儲存與顯示。

請注意，目前圖片資料通道支援 JPG、JPEG、和 PNG三種圖片檔案格式。一旦上傳至 MCS 後，則都會被儲存為 PNG 檔案格式。

## 影像串流

有別於其他資料通道，可以透過上傳 CSV 或是 JSON 格式的資料更新資料點，您在使用影像串流前必須先在設備上安裝視頻轉換器套件。

以下是目前 MCS 所支援的影像串流規格

* 影像格式：MPEG1
* 最大解析度：320x240
* 最大畫面更新率：30 fps
* MCS 影像串流服務器：

```
http://stream.mcs.mediatek.com:80/:deviceId/:deviceKey/:dataChnId/:width/:height
```
請將其中的 deviceId, deviceKey, dataChnId, width 和 height 更換成您設備上實際的數據。其中 width 與 height 是上傳影像串流時所設定的解析度大小。
	
* 在 LinkIt Smart 7688 上建議的視頻轉換器套件：FFmpeg

```
ffmpeg -s 176x144 -f video4linux2 -r 30 -i /dev/video0 -f mpeg1video -r 30 -b 800k http://stream.mcs.mediatek.com:80/:deviceId/:deviceKey/:dataChnId/176/144
```

