# 本地开发

本文介绍如何在本地开发和调试NovaServer工程。

## 本地工程

#### golang开发环境

NovaServer使用Golang编写，请确保本地有[Golang](https://go.dev/dl)开发环境。

```bash
go version
```

#### 代码工程
请使用自己的github账号fork NovaServer工程。然后git clone到本地。

```bash
git clone git@github.com:<Account>/nova-server.git
```

## 本地环境

正常情况下，本地无特殊依赖。

## 验证与调试
NovaServer默认启动后，输可通过以下配置来运行 。  





!!! config  "config.yml"

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
