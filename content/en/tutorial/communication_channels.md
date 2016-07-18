# TCP and MQTT Connection

To start sending and receiving device data, you can choose from the **Command Server** to build up a TCP connection or **MQTT** to communicate with the MCS server. By connecting your device to Command Server or MCS MQTT Broker, you can giving commands to the device from the MCS console or mobile device or receiving data from the connected devices.

The **Command Server** is a **one-way TCP connumication**, it only supports the message or command giving from the MCS server to the connected device; while the **MQTT** is a **two-ways comunication**, you can both send message to the connected device or the device can send message to the MCS server.

MCS supports this two kinds of communication at the same time, but we highly recommand you only implement one kind of communication on a device.

## Command Server
 Command Server is a **one-way** communication, it ony send the command from the MCS to the connected device.

### Set Up Connection
 To build a connection bwtween the Command Server and your device, you have to first call the [Get connection API](https://mcs.mediatek.com/resources/latest/api_references/#get-connection) to get connection IP and port. Then by keep sending heartbeat to maintain the connection.


### Communication Format
 To send commands via Command Server to device, you can refer to the [Command Server format](https://mcs.mediatek.com/resources/latest/api_references/#command-server-format) to send correct command to different data channels.

 ### FOTA via Command Server

Once the device is connected and online via command server, and user pushed firmware to device. MCS server will send the following FOTA information to the device:

**deviceId, deviceKey, timestamp, FOTA, version, MD5, URL**

* deviceId: the deviceId of the device
* deviceKey: the deviceKey of the device
* timestamp: the timestamp when the firmware is pushed
* FOTA: a string
* version: the version of the firmware being passed
* MD5: the MD5 of the firmware being passed
* URL: the download URL of the firmware being passed

For more information about FOTA, please refer to [this link](../tutorial/managing_firmware).

## MQTT
MQTT is a **two-ways** connectivity protocol. It was designed as a lightweight publish and subscribe messaging transport. You can explore more information about the MQTT protocal [here](http://mqtt.org/). MCS follows standard MQTT protocal and supports basic MQTT features like offline message and retained message.

### Set Up Connection

MQTT Broker Host: mqtt.mcs.mediatek.com

Port: 1883(un-encrypted) or 8883(encrypted)

Please note, MCS is using **server site signed** mechanism while using the encypted port.

### Subscribe & Publish

After you've connected to the MCS MQTT broker. You can subscribe to specific device or data channel; you can also publish to specific data channel.

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

### Communication Format

The format that you will receive when **subcribe** to a channel or **publish** to MCS:
```
timestamp,dataChnId,value
```

For more information about the value format for MQTT, please refer to this [link](../api_references/mqtt_communication_format).

### Quality of Service (QoS)

QoS or Quality of Service is one of the key features of MQTT. Currently, MCS only supports QoS0 and QoS1.

* QoS 0: Send only once. This fire and forget method is the default messaging level that does not guarantee message delivery.
* QoS 1: Deliver at least once. This level guarantees that the message is delivered, but do not enforce one-time delivery.

### Retained Message & Offline Message

The MCS MQTT Broker also supports Retained message and Offline message as the MQTT standard defined.

* Retained message: This message will be sent everytime a client is subscribe to the topic. For example, a welcome message.
* Offline message: This message will be keep in the broker if the client is offline, and sent to the client when it goes online.

### Keep Alive

The keep alive is a time interval, the client device commits to by sending regular PING Request messages to the MQTT broker. The MQTT broker response with PING Response and this mechanism will allow both sides to determine if the other one is still alive and reachable. MCS MQTT follows the MQTT standard to maintain the keep alive between the client and broker.

### FOTA via MQTT

Please note, if you would like to send FOTA using the MQTT communication, you have to subscibe one of the topic to the wildcard level.

The format is as following:

```
mcs/:deviceId/:deviceKey/+
```

Once the device is connected and online via MQTT, and user pushed firmware to device. MCS server will send the following FOTA information to the device:

** timestamp, FOTA, version, MD5, URL**

* timestamp: the timestamp when the firmware is pushed
* FOTA: a string
* version: the version of the firmware being passed
* MD5: the MD5 of the firmware being passed
* URL: the download URL of the firmware being passed

For more information about FOTA, please refer to [this link](../tutorial/managing_firmware).



