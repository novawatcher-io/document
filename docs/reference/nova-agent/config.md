# trace-agent 配置

## 配置说明

| 配置项目                    | 说明                                                          |
| --------------------------- | ------------------------------------------------------------- |
| `cluster`                   | 集群名称                                                      |
| `company_uuid`              | 公司UUID                                                      |
| `docker_unix_domain_socket` | Docker的Unix Domain Socket路径                                |
| `log_level`                 | 日志级别, 可选项: ["trace", "debug", "info", "warn", "error"] |
| `node_report_addr`          | 上报地址, GRPC部分                                            |
| `oltp_exporter_addr`        | OLTP Exporter地址                                             |
| `sampling_period`           | 指标采集周期                                                  |

## 实例配置文件

```json
{
  "cluster": "default",
  "company_uuid": "217057afc5769cbeea96766334f7e7ec",
  "docker_unix_domain_socket": "/run/docker.sock",
  "log_level": "debug",
  "node_report_addr": {
    "host": "81.71.98.26",
    "port": 10050
  },
  "oltp_exporter_addr": {
    "host": "81.71.98.26",
    "port": 4317
  },
  "sampling_period": 2
}
```

## 使用配置

```shell
./nova-agent -c /path/to/config.json
```
