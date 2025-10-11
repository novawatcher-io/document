# 设备管理

在物联网控制台的左侧导航栏，选择资产管理 > 设备管理，单击添加脱流机，为温湿度传感器添加一个设备，如下图所示。

## 搜索设备列表

进入设备列表界面，搜索设备列表数据

![search_device](/doc/assets/img/doc/assets/device/search_device.png)


## 创建设备

单击新增按钮添加设备。

![add_device](/doc/assets/img/doc/assets/device/add_device.png)


填写表单:

| 表单名         | 类型 | 描述 |
|-------------|  | --- |
| 设备名称       | 字符串	| 设备的名字 |
| 设备编号       |	字符串 |	设备的编号，用来标记设备的唯一性 |
| 设备分组      |	选择数据 |	保留字段---用来对设备分组 |
| 建筑物 |	选择数据 |	保留字段----从建筑物管理里选的，用来绑定设备所在的建筑物 |
| 设备分类 |	选择数据 |	保留字段----对设备进行分类 |
| 设备类型 |	选择数据 |	保留字段----设备类型 |
| 设备行为 |	选择数据 |	保留字段----设备功能 |
| 控制模式 |	选择数据 |	保留字段----分为自动和手动模式 |
| 通信方式 | 选择数据 |	4G和局域网，当前只支持局域网，用来对局域网进行组局 |
| 网关 | 选择数据 |	绑定设备网关，使用哪一个网关对设备数据进行采集 |
| 协议类型 | 选择数据 |	设备的通信协议，当前只支持MODBUS TCP |
| 设备模板 | 选择数据 |	设备通信协议的标志 |

填写表单，保存数据，添加设备

![add_device_form](/doc/assets/img/doc/assets/device/add_device_form.png)

## 修改设备

在设备管理中，点击修改设备

![update_device](/doc/assets/img/doc/assets/device/update_device.png)

## 删除设备

在设备管理中，点击删除按钮，删除设备

![delete_device](/doc/assets/img/doc/assets/device/delete_device.png)
