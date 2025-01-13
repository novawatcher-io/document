# trace-agent 介绍

## 简介

trace-agent 是一个用于监控集群中各个节点的工具. 它会定期采集节点的指标数据, 并将数据上报到指定的OLTP Exporter地址.

## 构建

参考 [构建文档](build.md) 构建 trace-agent.

## 启动

```shell
./nova-agent -c /path/to/config.json
```

### 配置

参考 [配置文档](config.md) 配置 trace-agent.

## 上报内容

参考 [上报内容文档](report/index.md) 查看 trace-agent 上报的内容.
