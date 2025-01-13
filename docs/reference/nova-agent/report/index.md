# trace-agent上报内容

采集指标:

- [CGroup指标](cgroup.md)
- [CPU指标](cpu.md)
- [磁盘使用指标](disk.md)
- [容器指标](docker.md)
- [GPU指标](gpu.md)
- [Memory指标](memory.md)
- [网络指标](network.md)
- [进程指标](process.md)


## OLTP指标
| 资源 | 指标             | 内容                           | 属性列表       | 是否完成 |
| ---- | ---------------- | ------------------------------ | -------------- | -------- |
| 系统 | 运行时间(Uptime) | 主机开启之后运行的时间         | host_object_id |
| 系统 | 文件描述符数量   | 监控系统中使用的文件描述符数量 | host_object_id |
| 内存 | 使用率           | 已使用内存/机器总内存          | host_object_id |
| 进程 | 进程数量         |                                | host_object_id |
