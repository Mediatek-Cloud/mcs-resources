# Connect device

This tutorial demonstrates how to connect device to receive command from MCS.


### Step 1. Call the RESTful API:

GET https://api.mediatek.com/mcs/v2/devices/{deviceId}/connections to obtain the response value for Socket Server IP and Port.
Command server respond format:

```
{
    "ip": "ServerIp",
    "port": "serverPort"
}

```
### Step 2. Open a TCP connection using the given IP and port and send a heartbeat message.


Heartbeat format:

```
    deviceId,deviceKey,timestamp

```
After the TCP long connection is established, you can give command to the device through the MSC platform.

The command Format:
```
    deviceId,deviceKey,timestamp,dataChnId,commandValue

```

You've connected the device.

Please refer to the command server format in the API reference page for more details on the formats of data channel types.
