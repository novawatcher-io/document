# 快速上手：节点日志采集

下面我们将演示一个最简单的采集节点日志文件的场景。

### 1. 下载可执行文件
请找一台Linux服务器节点，下载NovaServer二进制可执行文件

```shell
VERSION=v0.0.1
curl -LJ https://github.com/novawatcher-io/nova-server/releases/download/v1.2.0/nova-server-linux-amd64 -o nova-server
```

请将以上的<VERSION>替换成具体的版本号。

下载NovaAgent二进制可执行文件
```shell
VERSION=v0.0.1
curl -LJ https://github.com/novawatcher-io/nova-agent/releases/download/v1.2.0/nova-agent-linux-amd64 -o nova-agent
```
请将以上的<VERSION>替换成具体的版本号。

### 2. 添加配置文件

nova-server启动配置，复制以下内容为config.yml文件：
=== "pipelines.yml"
```yaml
app:
  aes_key: "6c84fb94eb046c0876f98777be46d6be"
  debug: true
server:
  address: ":8080"
  openapiPath: "/api.json"
  swaggerPath: "/swagger"
grpc:
  address: ":10050"
  server_list:
    - 127.0.0.1:10051
    - 127.0.0.1:10052
    - 127.0.0.1:10053

closeToken: true
logger:
  level: "all"
  stdout: true


database:
  default:
    link:    "mysql:root:root@tcp(localhost:3306)/deep_observe?loc=Local&parseTime=true"
    charset: "utf8mb4"
    debug: "true"
    dryRun: "false"
    maxIdle:  "10"
    maxOpen:  "10"
    maxLifetime:  "30"
    type: mysql
  clickhouse:
    link: "clickhouse:default:asd1234567@@tcp(81.71.98.26:9090)/otel"
    debug: true

trace-database:
  username: "default"
  password: "asd1234567@"
  database: "otel"
  type: "clickhouse"
  networks:
    - host: "localhost"
      port: 9090
```

nova-agent启动配置，复制以下内容为config.json文件：

```json
{
  "cluster": "default",
  "company_uuid": "e902c1e84b9f9b12bdf22936603acfda",
  "node_report_addr": {
    "host": "81.71.98.26",
    "port": 10050
  },
  "sampling_period": 2,
  "oltp_exporter_addr": {
    "host": "81.71.98.26",
    "port": 4317
  },
  "container_collector_config": {
    "enable": true,
    "container_runtime": "containerd",
    "container_unix_domain_socket": "/var/run/crio/crio.sock"
  },
  "trace_server_config": {
    "enable": false,
    "address": "0.0.0.0:11800"
  },
  "host_collect_config": {
    "enable": true
  },
  "close_stdout": false,
  "log_level": "debug",
  "log_file": "stdout",
  "prometheus_exposer_addr": "0.0.0.0:9000"
}
```

### 3. 运行

运行nova-server
```shell
./nova-server -c -gf.gcfg.file={$path}/config.yaml
```

运行nova-agent
```shell
./nova-agent -c config.json
```


