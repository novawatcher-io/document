# 进程指标

## GRPC上报指标

| 字段                     | 类型                 | 描述                    | 来源                                                                    |
| ------------------------ | -------------------- | ----------------------- | ----------------------------------------------------------------------- |
| pid                      | uint64               | 进程id                  | /proc/[pid]                                                             |
| name                     | string               | 进程名字                | /proc/[pid]/status/Name                                                 |
| path                     | string               | 进程路径                | /proc/[pid]/exe                                                         |
| cmdline                  | string               | 启动命令                | /proc/[pid]/cmdline                                                     |
| work_dir                 | string               | 工作目录                | /proc/[pid]/cwd                                                         |
| ppid                     | uint64               | 父进程id                | /proc/[pid]/status/PPid                                                 |
| uid                      | int32                | 用户id                  | /proc/[pid]/status/Uid                                                  |
| user_name                | string               | 用户名                  | 通过 getpwuid 获取                                                      |
| gid                      | int32                | 组id                    | /proc/[pid]/status/Gid                                                  |
| state                    | ProcessState         | 进程状态                | /proc/[pid]/status/State                                                |
| running_time             | double               | 运行时长(单位为秒)      | /proc/uptime - (/proc/[pid]/stat/start_time[22]) / sysconf(_SC_CLK_TCK) |
| container_id             | string               |                         | /proc/[pid]/cgroup                                                      |
| open_fd_count            | uint64               | 打开的文件描述符数量    | /proc/[pid]/status/FDSize                                               |
| involuntary_ctx_switches | uint64               | 被动上下文切换次数      | /proc/[pid]/status/nonvoluntary_ctxt_switches                           |
| voluntary_ctx_switches   | uint64               | 主动上下文切换次数      | /proc/[pid]/status/voluntary_ctxt_switches                              |
| cpu_nice                 | uint64               | 优先级                  | /proc/[pid]/stat/[19]                                                   |
| threads_num              | uint64               | 线程数量                | /proc/[pid]/status/Threads                                              |
| env_variables            | repeated EnvVariable | 环境变量                | /proc/[pid]/environ                                                     |
| memory_usage             | ProcessMemoryUsage   | 内存使用率              | /proc/[pid]/statm                                                       |
| iostat_read_bytes        | uint64               | 读取字节数              | /proc/[pid]/io/read_bytes                                               |
| iostat_write_bytes       | uint64               | 写入字节数              | /proc/[pid]/io/write_bytes                                              |
| iostat_read_bytes_rate   | double               | 读取字节速率            | diff(iostat_read_bytes) / sample_period                                 |
| iostat_write_bytes_rate  | double               | 写入字节速率            | diff(iostat_write_bytes) / sample_period                                |
| cpu_user_time            | uint64               | 用户态 cpu 使用时间     | (/proc/[pid]/stat/utime[14]) / sysconf(_SC_CLK_TCK)                     |
| cpu_system_time          | uint64               | 内核态 cpu 使用时间     | (/proc/[pid]/stat/stime[15]) / sysconf(_SC_CLK_TCK)                     |
| cpu_user_pct             | double               | 用户态cpu 使用率        | this.cpu_user_time / (/proc/uptime - this.running_time)                 |
| cpu_system_pct           | double               | Kernel CPU 使用率百分比 | (this.cpu_system_time) / (/proc/uptime - this.running_time)             |
| cpu_total_pct            | double               | CPU总体使用率           | this.cpu_user_pct + this.cpu_system_pct                                 |
| start_time               | int64                | 进程启动时间点          | time(null) - running_time                                               |
| is_kernel_thread         | bool                 | 是否是内核进程          |                                                                         |
| gpu_usage                | ProcessGPUUsage      | GPU Memory Usage        |                                                                         |
