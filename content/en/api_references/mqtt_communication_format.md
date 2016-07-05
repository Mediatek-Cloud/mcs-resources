# MQTT communication format

The MQTT communication format of each data type is defined here. This format is for both subscribe or publish.


The client device will get the data as the following format from the MQTT broker, and the user can write a parser in the device to parse the data needed. When publising, use the same format to publish the data back to the MCS MQTT broker.


## Prerequsite

Before the client device can receive or send the message to MQTT broker, the client device need to connect to the MCS MQTT broker and subscribe or publish to a topic.

### Set Up Connection

MQTT Broker Host: mqtt.mcs.mediatek.com

Port: 1883(un-encrypted) or 8883(encrypted)

Please note, MCS is using **server site signed** mechanism while using the encypted port.

### Subscribe & Publish

After you've connected to the MCS MQTT Broker. you can Subscribe to specific device or data channel; you can also publish to specific data channel.

For **subscription**, the topic is defined in the following format:

```
mcs/:deviceId/:deviceKey/:dataChnId
```

Or to subscribe all data channels in a device:

```
mcs/:deviceId/:deviceKey/+
```

For **publish**, the topic is defined in the following format:

```
mcs/:deviceId/:deviceKey/:dataChnId
```

## MQTT subscription and publish formats

** The timestamp is using the UNIX timestamp format.

### Switch

```
dataChnId,timestamp,{0 or 1}

```
0 stands for OFF, and 1 stands for ON.

For example:

switch01,, 1

To turn the switch01 to on state, and do not give the timestamp.

### Category
```
dataChnId,timestamp,{Key Value}
```
The Key value will correspond to the Key name that you’ve set.

### Integer
```
dataChnId,timestamp,{Integer}
```

### Float
```
dataChnId,timestamp,{Float}
```

### Hex
```
dataChnId,timestamp,{Hex value}
```
Hex is referred to hexadecimal value which only takes value from A-D and 0-9.

### String
```
dataChnId,timestamp,{string}
```

### GPS
```
dataChnId,timestamp,{latitude},{longitude},{altitude}
```

The range of latitude is from -90 to 90. 0 to 90 stands for North and 0 to -90 stands for South.

The range of longitude is from -180 to 180. 0 to 180 stands for East and 0 to -180 stands for West.

The range of altitude is from 0 to 20000 in meter.

### GPIO
```
dataChnId,timestamp,{0 ot 1}
```
0 stands for Low, and 1 stands for High.

### PWM
```
dataChnId,timestamp,{value},{period}

```

### Analog
```
dataChnId,timestamp,{value}

```

### Gamepad
```
dataChnId,timestamp,{up/down/right/left/A/B value| press(1) or release(0)}

```

### Image
```
dataChnId,timestamp,{image file base64 encoding string value}

```
