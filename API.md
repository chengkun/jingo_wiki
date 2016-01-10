# API接口
## API V1.1采用RESTful风格。
有关格式相关的内容请参见 [JSON](https://en.wikipedia.org/wiki/JSON)

JSON格式中的数值规范：
 数值（number）也与C或者Java的数值非常相似。除去未曾使用的八进制与十六进制格式。除去一些编码细节。
```
 {value: 0.1} 合法格式
 {value: 00.0} 非法格式
```
 如果遇到406错误，请先检查是否上传数据格式有误
## 设备接口
设备代表一组传感器的集合，设备分为开发设备和终端设备两种。
创建设备
```
POST
/v1.1/devices
```
POST数据
```
{
  "title":"test",
  "about":"test api",
  "tags":"temperature,lab",
  "location":{
    "local":"Yangling",
    "latitude":0.444,
    "longitude":0.555
  }
}
```

|字段	 |类型 |可为空|备注|
|---- |-----|-----|---:|
|title|string|否	|标题|
|about	|string|	否	|简介|
|tags	|string|	否	|标签|
|location	|json|	否|	地理位置信息|
|location.local	|string	|否	|地理位置，如：山东青岛|
|location.latitude	|float	|否	|经度|
|location.longitude	|float	|否	|纬度|

返回值
JSON
```
{
  "device_id": 2
}
```
|字段	|类型	|可为空|备注|
|----|----|-----|----:|
|device_id	|int|	否	|设备ID|

访问授权
U-ApiKey: <your_api_key>

## 编辑设备
PUT
/v1.1/devices/<device_id>
PUT数据
{
  "title":"test",
  "about":"test api",
  "tags":"temperature,lab",
  "location":{
    "local":"Qingdao",
    "latitude":0.444,
    "longitude":0.555
  }
}
字段	类型	可为空	备注
title	string	否	标题
about	string	否	简介
tags	string	否	标签
location	json	否	地理位置信息
location.local	string	否	地理位置，如：山东青岛
location.latitude	float	否	经度
location.longitude	float	否	纬度
返回值
返回值为空
访问授权
U-ApiKey: <your_api_key>

## 罗列设备
GET
/v1.1/devices
返回值
JSON
[
  {
    "id": "2",
    "title": "test2",
    "about": "just a test"
  },
  {
    "id": "3",
    "title": "test3",
    "about": "just a test"
  }
]
返回值为一个JSON数组，数组内容为用户所有的设备列表
字段	类型	备注
id	int	设备ID
title	string	设备标题
about	string	设备简介
访问授权
U-ApiKey: <your_api_key>

## 查看设备
GET
/v1.1/devices/<device_id>
返回值
JOSN
{
  "title": "test3",
  "about": "just a test",
  "tags": "lab",
  "local": "Qingdao",
  "latitude": 0.444,
  "longitude": 0.555
}
字段	类型	可为空	备注
title	string	否	标题
about	string	否	简介
tags	string	否	标签
local	string	否	地理位置，如：山东青岛
latitude	float	否	经度
longitude	float	否	纬度
访问授权
U-ApiKey: <your_api_key>
删除设备
DELETE
/v1.1/devices/<device_id>
返回值
返回值为空
访问授权
U-ApiKey: <your_api_key>
传感器

## 创建传感器
POST
/v1.1/device/<device_id>/sensors
POST数据
{
  "type":"value",
  "title":"温度传感器测试",
  "about":"这是一个测试传感器",
  "tags":"数据,温度",
  "unit": {
     "name": "摄氏度",
     "symbol": "°C"
   }
}
字段	类型	可为空	备注
type	string	否	传感器类型：value, switcher, gps, gen, photo
title	string	否	标题
about	string	否	简介
tags	string	否	标签
unit	json	否	单位符号
unit.name	string	否	单位
unit.symbol	string	否	符号
返回值
JOSN
{
  "sensor_id": 2
}
字段	类型	可为空	备注
sensor_id	int	否	传感器ID
访问授权
U-ApiKey: <your_api_key>

## 编辑传感器
PUT
/v1.1/device/<device_id>/sensor/<sensor_id>
PUT数据
{
  "title":"温度传感器测试",
  "about":"这是一个测试传感器",
  "tags":"数据,温度",
  "unit": {
     "name": "摄氏度",
     "symbol": "°C"
   }
}
字段	类型	可为空	备注
title	string	否	标题
about	string	否	简介
tags	string	否	标签
unit	json	否	单位符号
unit.name	string	否	单位
unit.symbol	string	否	符号
返回值
返回值为空
访问授权
U-ApiKey: <your_api_key>

## 罗列传感器
GET
/v1.1/device/<device_id>/sensors
返回值
该设备的所有传感器列表信息
JOSN

[
  {
    "id": 2,
    "title": "test2",
    "about": "just a test",
    "type":0,
    "last_update": 1380009649,
    "last_data":"317",
    "last_data_gen":null
  },
  {
    "id": 3,
    "title": "test3",
    "about": "just a test",
    "type":6,
    "last_update": 1380009669,
    "last_data":null;,
    "last_data_gen":{"lat":23.8,"lng":54.5,"speed":45}
  }
]
字段	类型	备注
id	int	传感器ID
title	string	标题
about	string	简介
访问授权
U-ApiKey: <your_api_key>

## 查看传感器
对该地址发起GET请求将会获得指定ID的传感器的详细信息。
GET
/v1.1/device/<device_id>/sensor/<sensor_id>
返回值
该设备的详细信息
JOSN
数值型传感器
{
  "title":"test",
  "about":"just a test",
  "tags":"tag1,tag2",
  "unit_name": "temperature",
  "unit_symbol": "C"
}
字段	类型	备注
title	string	标题
about	string	简介
tags	string	标签
unit_name	string	单位名称
unit_symbol	string	单位符号

## 删除传感器
### 删除指定传感器
DELETE
/v1.1/device/<device_id>/sensor/<sensor_id>
返回值
返回值为空
访问授权
U-ApiKey: <your_api_key>

## 数据点

### 创建数据点
本章描述了如何为设备的传感器创建数据点。使用HTTP POST方法来使用本URL创建新的数据点。
创建单个数据点
为传感器创建一个数据点。
注意：微博型传感器不支持手动上传数据点。
POST
/v1.1/device/<device_id>/sensor/<sensor_id>/datapoints
POST数据

数值型传感器
{
  "timestamp":"2012-03-15T16:13:14",
  "value":294.34
}
字段	类型	备注
timestamp	string	时间，可为空
value	float	值
多数据点(同一传感器)
对同一传感器同时上传多个数据点。
注意：图片传感器和微博传感器不支持本操作。
POST
/v1.1/device/<device_id>/sensor/<sensor_id>/datapoints
数值型传感器
[
  {
    "timestamp":"2012-03-15T16:13:14",
    "value":294.34
  },
  {
    "timestamp":"2012-03-15T16:13:24",
    "value":284.34
  }
]
访问授权
U-ApiKey: <your_api_key>
返回值
返回值为空

### 多数据点（同一设备）
POST
/v1.1/device/<device_id>/datapoints
POST数据
[
  {"sensor_id": <sensor_id>, "value": 50},//数值型
  {"sensor_id": <sensor_id>, "value": {"lat":35.4567,"lng":46.1234,"speed":98.2, offset: true}}，//GPS型
  {"sensor_id": <sensor_id>, "value": {/*your code here*/}}，//泛型
]
注意：不支持图片型和微博型传感器
访问授权
U-ApiKey: <your_api_key>
返回值
{"<sensor_id>":"","<sensor_id>":""}
编辑数据点
PUT
/v1.1/device/<device_id>/sensor/<sensor_id>/datapoint/<key>
PUT数据
数值型传感器
{
  "value": 39.4
}
GPS型传感器
{
  "value": {"lat":35.4321,"lng":46.3451,"speed":98.2}
}
泛型传感器
{
  "value": {...}
}
返回值
空

## 查看数据点
GET
/v1.1/device/<device_id>/sensor/<sensor_id>/datapoint/<key>
返回值
key不为空
//数值型
{
  "value": 39.4
}
//GPS型
{
 "value": {"lat":35.4321,"lng":46.3451,"speed":98.2}
}
//泛型
{
 "value": {...}
}
//微博型
{
  "status_cnt":0,"follower_cnt":0,"msg_cnt":0
}
key为空
//数值型
{
  "timestamp":"2012-03-15T16:13:14",
  "value": 39.4,
  "sensor_id": 2132,
  "device_id": 2234
}
//GPS型
{
  "timestamp":"2012-03-15T16:13:14",
  "value": {"lat":35.4321,"lng":46.3451,"speed":98.2}
}
//泛型
{
  "key":"e10adc3949ba59abbe56e037f20f884e",
  "value": {...}
}
访问授权
U-ApiKey: <your_api_key>
删除数据点
DELETE
/v1.1/device/<device_id>/sensor/<sensor_id>/datapoint/<key>
返回值
 返回值为空
访问授权
U-ApiKey: <your_api_key>

## 历史数据
### 查看历史数据
用于查看指定时间段及指定采样间隔的历史数据。
GET
/v1.1/device/<device_id>/sensor/<sensor_id>.json?start=<start_timestamp>&end=<end_timestamp>&interval=<interval>&page=<page>
字段	类型	备注
device_id	int	设备ID
sensor_id	int	传感器ID
start_timestamp	string	开始时间，格式：2014-5-10T11：40
end_timestamp	string	开始时间，格式：2014-5-15T11：40
interval	int	间隔时间
page	int	分页，默认是1
interval（数据采样间隔）说明
Interval	说明
1	每秒
10	10秒
返回值
JSON
数值型传感器
[
  {"timestamp": "2012-06-15T14:00:00", "value":315},
  {"timestamp": "2012-06-15T14:00:10", "value":316},
  {"timestamp": "2012-06-15T14:00:20", "value":317},
  {"timestamp": "2012-06-15T14:00:30", "value":317},
  {"timestamp": "2012-06-15T14:00:40", "value":317}
]