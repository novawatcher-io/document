---
title: "青岛星观信息网络-网关管理-agent管理"
keywords: "青岛星观信息网络, Agent管理, 物联网网关管理, 配置下发, 网关托管"
description: "青岛星观信息网络Agent管理是运行在物联网设备用在物联网网关管理的一套软件程序。它充当了配置下发和网关托管的中间件。。"
---
# agent管理

本文旨在为您介绍如何查看工业物联网网关的详细信息，包括基本信息和网关入口。

## Agent列表

通过点击 网关管理 > agent管理,可以看到Agent列表。

![agent_list](/docs-assets/img/gateway/agent_list.png)

## 新建Agent

通过点击 网关管理 > agent管理,单击新建Agent 创建一个网关管理的node节点.

![add_agent](/docs-assets/img/gateway/add_agent.png)

## 编辑和删除agent

![agent_op](/docs-assets/img/gateway/agent_op.png)

## 生成配置


通过点击 网关管理 > agent管理,单击Agent 创建一个网关配置.

通过新建一个agent配置，可以生成物联网网关的配置信息，然后网关启动之后读取生成的配置信息，采集设备数据

![agent_config_list](/docs-assets/img/gateway/agent_config_list.png)

点击新建配置，可以重新生成一个新的配置，然后输入配置版本，保存配置，如果想下发到网关，需要重启网关

![agent_config_save](/docs-assets/img/gateway/agent_config_save.png)

## 进程管理

通过进程管理，可以点击管控网关进程的启停

![manage_process](/docs-assets/img/gateway/manage_process.png)

选中进程之后，点击按钮用来启动和停止进程

![op_process](/docs-assets/img/gateway/op_process.png)