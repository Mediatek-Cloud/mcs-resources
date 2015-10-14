#激活装置

##描述

使用** HTTPs的GET **来激活装置


##请求的URL
使用以下API来激活您的装置

```
https://api.mediatek.com/mcs/v2/devices/activate/:activati​​onCode

```

##动作
HTTPs的GET


##参数
###头

内容类型：`应用/ json`


###返回类型
返回格式是JSON格式

##回覆

###回覆代码
200

###回覆头
对于JSON响应：
```
内容类型：`应用/ json`
```

###回覆内容

***回覆格式：JSON ***

JSON格式的回覆内容会包含以下几个栏位

|栏位名称|资料型态|描述|
| --- | --- | --- | --- |
|代码|字符串| HTTP状态代码|
| deviceKey |字符串|该deviceKey |
| DEVICEID |字符串|该DEVICEID |
| chipname |字符串|设备名称|
|消息|字符串|系统日志消息|


**范例：**

请求的URL
```
https://api.mediatek.com/mcs/v2/devices/activate/edb4b2eil152
```

请求头


内容类型：`应用/ json`


回覆内容

```
{
    “apiVersion”：“2.10.1”
    “代码”：200，
    “消息”：“申请成功”，
    “DEVICEID”：“JU5z4yVF”
    “deviceKey”：“yQGymH0IRWFSVC37”，
    “chipName”：“装置物联网雏形”
}

```


##错误回覆


當有錯誤發生時，回傳非200之其他回覆代碼。回覆內容為JSON格式並包含以下資訊：

|栏位名称|资料型态|描述|
| --- | --- | --- |
|代码|整数|错误代码|
|消息|字符串|错误说明|

**范例：**

```
{
    “apiVersion”：“2.10.1”
    “代码”：400，
    “消息”：“错误激活代码。”
    “错误”：
        {
            “代码”：400，
            “消息”：“400错误的请求”
        }
    ]
    “的StatusCode”：400，
    “选择”：{}
}
```