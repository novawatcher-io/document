# Memory指标


## GRPC上报字段

| 字段名      | 字段类型 | 字段描述 | 来源                                                |
| ----------- | -------- | -------- | --------------------------------------------------- |
| total       | uint64   | 总内存   | /proc/meminfo/MemTotal                              |
| free        | uint64   | 剩余内存 | /proc/meminfo/MemFree                               |
| swap_cached | uint64   | 共享内存 | /proc/meminfo/SwapCached                            |
| used        | uint64   | 已用内存 | total - (free + Buffers(not reportd) + swap_cached) |
