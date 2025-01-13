# 容器指标



## 上报信息

| 字段           | 类型   | 说明             |
| -------------- | ------ | ---------------- |
| id             | string | 容器id           |
| name           | string | 容器名字         |
| state          | string | 容器状态         |
| command        | string | 容器运行的命令   |
| image_name     | string | 容器的镜像名字   |
| cpu_limit      | int64  | CPU限制          |
| cpu_user_pct   | double | CPU 用户态占比   |
| cpu_system_pct | double | CPU 内核态占比   |
| cpu_total_pct  | double | 容器cpu使用率    |
| rss_usage      | double | 容器内存使用率   |
| memory_limit   | int64  | 内存限制         |
| memory_cache   | int64  | 内存缓存         |
| memory_rss     | int64  | rss内存          |
| memory_pct     | double | 内存使用率       |
| rx_bytes       | uint64 | 容器读取的字节数 |
| rx_bps         | double | 容器读取的速率   |
| tx_bytes       | uint64 | 容器写入的字节数 |
| tx_bps         | double | 容器写入的速率   |
| net_rcvd_bps   | double | 容器网络接收速率 |
| net_sent_bps   | double | 容器网络发送速率 |
| start_time     | uint64 | 容器启动时间点   |
| running_time   | uint64 | 运行时间         |
| addresses      | string | 容器的地址       |
| host_ips       | string | 主机IP           |
| pid            | int32  | pid列表          |
| pod_ip         | string | pod ip           |
| pod_ports      | int32  | pod端口          |
| host           | string | 容器             |
| health         | int32  | 健康             |
| thread_count   | int32  | 线程数量         |
| thread_limit   | int32  | 线程限制         |
| kube_app       | string | todo             |
