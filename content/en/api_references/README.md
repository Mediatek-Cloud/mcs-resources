# API references

MediaTek Cloud Sandbox (MCS) provides RESTful APIs for building applications and services that are able to make meaningful communications with MCS including data point uploads and retrievals as well as commands via TCP socket. MCS also provides eady-to-read visual charts based on the uploaded data, including time-series data for real time applications. 


## Request URL

Standard MCS RESTful API request has the following URL construct:

```
https://api.mediatek.com/v2
```


## Parameters

The parameters that are part of URL are used to identify a specific resource. 

```
https://api.mediatek.com/v2/devices/{deviceId}/retrieveDataPoints
```

In the example above, the **device ID** is specified in the URL.


Also, the perementers can be in the message body of a POST request. The request body must be formatted as either JSON or CSV. For each POST request, please specify the **content-type** in the header. 

* `content-type: application/json` stands for JSON format.
* `content-type: text/csv` stands for CSV format.


## Client Errors

MediaTek Cloud Sandbox (MCS) uses the standard HTTP status code to indicate if an API request is successful or failed. The HTTP status codes users may encounter are:

**200 OK** - The request is successful.

**201 Created**- The request has been fulfilled and a new resource is being created.

**202 Accepted** - The request has been accepted for processing, but the process has not been completed yet.

**204 No Content** - The server processed the request successfully, but isn’t returning any content. This is usually used as a response for a successful delete request.

**400 Bad Request** - The server cannot process the request due to an unexpected parameter received from the client. 

**401 Unauthorized** -Authorization has failed or it hasn’t been provided. A header for Authorization is required.

**403 Forbidden** - The server is refusing to respond to a valid request.

**404 Not Found** - The requested resource could not be found.

**405 Method Not Allowed** - The request was made from a resource that used a method which is not supported.

**500, 502 Server Error** - MCS server has encountered an error.


## HTTP Verbs

The MCS RESTful APIs can be accessed with following HTTP methods:

**GET** - To retrieve resources.

**POST** - To create resources.

**PUT** - To update resources.

**DELETE** - To delete resources.


## Authentication

Except for data point uploads and retrievals APIs, all requests sent to the API server need to be authenticated. A Bearer token for **Authorization** key in the HTTP header is required. If it is not provided, the server will respond with an **Unauthorized** message.


## Resource IDs

When a prototype or a data channel is created, or when a device is added, a unique ID is assigned to each prototype, data channel or device. This unique ID is not editable, but it can be used to access data with which it is associated. However, the key cannot access data from any other resource.

For example, to GET data from a specific data channel of a test device, you will need to use a data channel ID for the data channel of the test device.


## Resources

Following is a shortlist of useful terms of MCS:

### Data Channels

The data channel is a logical placeholder in the cloud for data generated from a specific component of a physical device, or a command from the cloud to be pushed into a specific component of the connected physical device. In other words, data channel is designed for one-way or two-way communications between the cloud and the connected physical device.

MCS provides RESTful APIs to easily retrieve data from the data channels and update the data channel.

### Devices

There are two types of devices which you can create in MCS: test device and Beta device. The test device enables you to test the functionality of the prototype before it is Beta-released. The Beta device can be created after a prototype is Beta-released and it’s used by the end user.

MCS provides RESTful APIs for you and the end user. For example, APIs that enable data retrieval from a device and that allow remote control using the device.

### Prototype

A prototype is a service that’s delivered as a result. The MSC provides several APIs to make use of the prototype. The developer can add data channels in a prototype and test the prototype by creating a test device before releasing it.
