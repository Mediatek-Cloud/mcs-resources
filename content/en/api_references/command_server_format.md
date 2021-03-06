# Command server format
The command server format of each data type is defined here. It is the format that the command server sent to the device to process.

**The timestamp is using the UNIX timestamp format.

The device will get the data as the following format from the command server, and the user can write a parser in the device to parse the data needed.


## Prerequsite
Before the device can get the command from command server, you need to first connect the device to MCS.

Call the RESTful API: GET https://api.mediatek.com/mcs/v2/devices/{deviceId}/connections to obtain the response value for Socket Server IP and Port.
Command server respond format:

```
{
    "ip": "ServerIp",
    "port": "serverPort"
}

```
Open a tcp connection to the given ip and port and send a heartbeat message.

Heartbeat format:

```
    deviceId,deviceKey,timestamp

```
The timestamp is optional, if you do not want to send the timestamp, just put 0 in the timestamp field.


After the TCP long connecion is built, the user can give command to the device via the MCS platform.

The command Format:

```
    deviceId,deviceKey,timestamp,dataChnId,commandValue

```


## Command formats for each data channel type


### Switch

```
deviceId,deviceKey,timestamp,dataChnId,{0 or 1}

```
0 stands for OFF, and 1 stands for ON.

For example:

switch01,, 1

To turn the switch01 to on state, and do not give the timestamp.

### Category
```
deviceId,deviceKey,timestamp,dataChnId,{Key Value}
```
The Key value will correspond to the Key name that you’ve set.

### Integer
```
deviceId,deviceKey,timestamp,dataChnId,{Integer}
```

### Float
```
deviceId,deviceKey,timestamp,dataChnId,{Float}
```

### Hex
```
deviceId,deviceKey,timestamp,dataChnId,{Hex value}
```
Hex is referred to hexadecimal value which only takes value from A-D and 0-9.

### String
```
deviceId,deviceKey,timestamp,dataChnId,{string}
```

### GPS
```
deviceId,deviceKey,timestamp,dataChnId,{latitude},{longitude},{altitude}
```

The range of latitude is from -90 to 90. 0 to 90 stands for North and 0 to -90 stands for South.

The range of longitude is from -180 to 180. 0 to 180 stands for East and 0 to -180 stands for West.

The range of altitude is from 0 to 20000 in meter.

### GPIO
```
deviceId,deviceKey,timestamp,dataChnId,{0 ot 1}
```
0 stands for Low, and 1 stands for High.

### PWM
```
deviceId,deviceKey,timestamp,dataChnId,{value},{period}

```

### Analog
```
deviceId,deviceKey,timestamp,dataChnId,{value}

```

### Gamepad
```
deviceId,deviceKey,timestamp,dataChnId,{up/down/right/left/A/B value| press(1) or release(0)}

```

### Image
```
deviceId,deviceKey,timestamp,dataChnId,{image file base64 encoding string value}

```
