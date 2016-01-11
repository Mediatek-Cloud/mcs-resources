# Data channel format

The API format of each data type is defined here. It is the format that the device report data to the command server.


**The timestamp is using the UNIX timestamp format, and it is not a required field. You can leave it blank, and the system will give the timestamp automatically as the server recorded time.

MCS supports both json and csv formats.

## Switch

For json:

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


For csv:

```
dataChnId,timestamp,{0 or 1}

```
0 stands for OFF, and 1 stands for ON.

For example:

switch01,, 1

To turn the switch01 to on state, and do not give the timestamp.

## Category

For json:

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


For csv:

```
dataChnId,timestamp,{Key Value}
```
The Key value will correspond to the Key name that you’ve set.

## Integer

For json:

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


For csv:

```
dataChnId,timestamp,{Integer}
```

## Float

For json:

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


For csv:

```
dataChnId,timestamp,{Float}
```

## Hex

For json:

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


For csv:

```
dataChnId,timestamp,{Hex value}
```
Hex is referred to hexadecimal value which only takes value from A-D and 0-9.

## String

For json:

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


For csv:

```
dataChnId,timestamp,{string}
```

## GPS
For json:

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


For csv:

```
dataChnId,timestamp,{latitude},{longitude},{altitude}
```

The range of latitude is from -90 to 90. 0 to 90 stands for North and 0 to -90 stands for South.

The range of longitude is from -180 to 180. 0 to 180 stands for East and 0 to -180 stands for West.

The range of altitude is from -20000 to 20000 in meter.

## GPIO

For json:

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


For csv:

```
dataChnId,timestamp,{0 ot 1}
```
0 stands for Low, and 1 stands for High.

## PWM
For json:

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
The range of Period and Value is from 0 to 1000.


For csv:

```
dataChnId,timestamp,{Value},{Period}
```

## Analog
For json:

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

For csv:

```
dataChnId,timestamp,{Integer value}
```
The range of Integer value is defined by users.

## Gamepad
For json:

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

For csv:

```
dataChnId,timestamp,{up/down/right/left/A/B value| press(1) or release(0)}
```

User can decide to only have the up/down/right/left value only or to have the A/B value together at the same time.

For example, if user set the up value to up when you created the data channel, then click up button, the value will be `up|0`. If user press up button, the value will be `up|1`.

You can use pre-defined hotkeys on keyboard to control this data channel:

`up = W`

`down = S`

`left = A`

`right = D`

`Key A = ,`

`Key B = .`

## Image

For json:

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


For csv:

```
dataChnId,timestamp,{image file base64 encoding string value}
```

To upload an image to the image display data channel, you have to convert the image file to base64 encoding. Upload the base 64 encoding string to the data channel, then the image will saved and shown.

Please be noted that the image data channel supports uploading files in JPG, JPEG, and PNG formats. However, after uploaded to MCS, all types of files will be saved in .PNG format.


## Video Stream

Unlike the other data channels of which the data points can be uploaded by either JSON or CSV format, you have to set up a video converter on your device before you can start streaming on MCS. 

Here are the video specifications the MCS currently supports:
 
* Video format: MPEG1
* Maximum resolution supported: 320x240
* Maximum fps supported: 30
* URL of MCS video relay server: 

	```
	http://52.76.74.57:8082/:deviceId/:deviceKey/:dataChnId/:width/:height
	```

* Recommended video converter on LinkIt Smart 7688: FFmpeg