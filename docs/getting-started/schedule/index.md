---
title: "调度管理-调度流程-青岛星观信息网络"
keywords: "工业制造, 调度流程, 作业, 工业物联"
description: "调度流程在调度系统中扮演着重要的作用，它可以按照设定的条件，对设备和云平台之间传递的消息进行各种计算、处理、流转等操作。"
---

# 调度流程

调度流程在调度系统中扮演着重要的作用，它可以按照设定的条件，对设备和云平台之间传递的消息进行各种计算、处理、流转等操作。

例如用规则可以实现以下场景：


 - 当设备上报属性达到某个条件时，向另一个设备下发属性或命令。
 - 当设备上报事件时，向另一个设备下发属性或命令。
 - 对设备上报的 Modbus TCP 二进制消息进行解析，生成相应的设备属性。

## 创建调度流程

按住工序，拖拽到画布，组成一个调度流程

![process_method](/docs-assets/img/schedule/process_method.png)


创建调度流程非常简单，需要了解以下基本概念：

### 节点类型

#### 开始节点

定义某一个流程的开始节点，一个调度流程只能有一个开始节点，是所有流程的开始

![begin_node](/docs-assets/img/schedule/begin_node.png)

#### 工序节点

每个工序里面可以有多个工序内容,工序控制当设备上报属性达到某个条件时，向另一个设备下发属性或命令。

![process_node](/docs-assets/img/schedule/process_node.png)

##### 工序节点使用

点击工序节点，设置工序

![process_node_click](/docs-assets/img/schedule/process_node_click.png)

点击添加工序，添加一个工序内容


![add_process_context](/docs-assets/img/schedule/add_process_context.png)

设置好工序内容以后,点击保存设置好工序

![save_process_context](/docs-assets/img/schedule/save_process_context.png)

拖拽设置好 工序操作数据流流程

![save_process_topo](/docs-assets/img/schedule/save_process_topo.png)

单击保存按钮保存好工序流程

![save_schedule](/docs-assets/img/schedule/save_schedule.png)
