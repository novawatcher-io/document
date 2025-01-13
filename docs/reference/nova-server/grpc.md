# grpc 

## 配置说明

grpc 服务器 主要用来收集agent容器数据、进程数据、cpu拓扑图收集器配置。

|    `字段`   |    `类型`    |  `是否必填`  |  `默认值`  |  `含义`  |
| ---------- | ----------- | ----------- | --------- | -------- |
| address |  string |    必填    |  :10050  | 数据收集器端口 |
| server_list | array  |    必填    |  127.0.0.1:10051  | 集群其他服务器列表 |

## Agent 信息上报

```
message DoAgent {
    int32                     Id                = 1   [json_name = "id"];                  // 自增标识                                          
    uint64                    ObjectId          = 2   [json_name = "object_id"];           // agent uuid                                        
    string                    CompanyUuid       = 3   [json_name = "company_uuid"];        // 公司uuid                                          
    string                    Name              = 4   [json_name = "name"];                // agent名字                                         
    int32                     OperateState      = 5   [json_name = "operate_state"];       // 操作状态 1-启动中 2-停止中 3-启动失败 4-停止失败  
    google.protobuf.Timestamp OperateTime       = 6   [json_name = "operate_time"];        // 操作时间                                          
    string                    Version           = 7   [json_name = "version"];             // agent版本                                         
    string                    ConfigUuid        = 8   [json_name = "config_uuid"];         // 配置版本                                          
    string                    Ipv4              = 9   [json_name = "ipv_4"];               // ipv4地址                                          
    string                    Ipv6              = 10  [json_name = "ipv_6"];               // ipv6地址                                          
    google.protobuf.Timestamp LastHeartbeatTime = 11  [json_name = "last_heartbeat_time"]; // 上次心跳时间                                      
    google.protobuf.Timestamp UpdateConfigTime  = 12  [json_name = "update_config_time"];  // 更新配置时间                                      
    google.protobuf.Timestamp Created           = 13  [json_name = "created"];             // 创建时间                                          
    int32                     IsDelete          = 14  [json_name = "is_delete"];           // 1-删除                                            
}
```

Agent 配置版本信息，用来下发配置

```
message DoAgentConfig {
    int32                     Id            = 1   [json_name = "id"];             // 自增标识   
    string                    Uuid          = 2   [json_name = "uuid"];           // 配置 uuid  
    string                    CompanyUuid   = 3   [json_name = "company_uuid"];   // 公司 uuid  
    string                    ConfigVersion = 4   [json_name = "config_version"]; // 配置版本   
    string                    Content       = 5   [json_name = "content"];        // 配置内容   
    google.protobuf.Timestamp Created       = 6   [json_name = "created"];        // 创建时间   
    google.protobuf.Timestamp Updated       = 7   [json_name = "updated"];        // 更新时间   
}
```

WatcherMen托管的进程信息

```
message DoAgentProcess {
    int32                     Id            = 1   [json_name = "id"];              // 自增标识            
    uint64                    AgentObjectId = 2   [json_name = "agent_object_id"]; // agent uuid          
    int32                     State         = 3   [json_name = "state"];           // 状态 1-运行 2-停止  
    string                    Name          = 4   [json_name = "name"];            // 名字                
    string                    Version       = 5   [json_name = "version"];         // 版本                
    google.protobuf.Timestamp StartTime     = 6   [json_name = "start_time"];      // 启动时间            
    google.protobuf.Timestamp Created       = 7   [json_name = "created"];         // 创建时间            
    int32                     IsDelete      = 8   [json_name = "is_delete"];       // 1-删除              
}
```

Agent 上报的主机配置信息

```
syntax = "proto3";
package deepagent.node.v1;
option go_package = "deepagent.node.v1";

message CpuFeatureCacheKeyValue { map<string, string> values = 1; }

// CPU 特性
message CpuFeature {
  string arch = 1;
  string brand = 2;
  string family = 3;
  string model = 4;
  string stepping = 5;
  string uarch = 6;
  string implementer = 7;
  string architecture = 8;
  string variant = 9;
  string part = 10;
  string revision = 11;
  string platform = 12;
  string machine = 13;
  string cpu = 14;
  string instruction = 15;
  string microarchitecture = 16;
  string processors = 17;
  string vendor = 18;
  repeated string flags = 19;
  repeated CpuFeatureCacheKeyValue caches = 20;
}

message LoadAverage {
  // 1分钟内的平均负载
  float one = 1;
  // 5分钟内的平均负载
  float five = 2;
  // 15分钟内的平均负载
  float fifteen = 3;
  // running processes
  int32 running = 4;
  // total processes
  int32 total = 5;
}

message CPUUsage { LoadAverage load = 1; }

// 环境变量键值对
message EnvVariable {
  string key = 1;
  string value = 2;
}

// 机器虚拟内存信息
message VirtualMemoryInfo {
  // total virtual memory, /proc/meminfo/MemTotal
  uint64 total = 1;
  // free virtual memory, the sum of LowFree+HighFree, /proc/meminfo/MemFree
  uint64 free = 2;
  // used virtual memory, /proc/meminfo/SwapCached
  uint64 swap_cached = 3;
  // total used memory, = total - (free + Buffers(not reportd) + swap_cached)
  uint64 used = 4;
}

// 进程内存使用情况
// read from /proc/[pid]/statm
message ProcessMemoryUsage {
  // total program size, /proc/[pid]/statm/[1]
  uint64 vm_size = 1;
  // resident set size(rss), /proc/[pid]/statm/[2]
  uint64 resident = 2;
  // shared, /proc/[pid]/statm/[3]
  uint64 shared = 3;
  // text, /proc/[pid]/statm/[4]
  uint64 text = 4;
  // lib, /proc/[pid]/statm/[5]
  uint64 lib = 5;
  // data + stack, /proc/[pid]/statm/[6]
  uint64 data = 6;
  // dirty pages, /proc/[pid]/statm/[7]
  uint64 dirty = 7;
  // todo: vm_size / total memory size
  float vm_pct = 9;
  // swap memory size, /proc/[pid]/status/VmSwap
  int64 swap = 10;
}

// R is running,
// S is sleeping,
// D is sleeping in an uninterruptible wait,
// Z is zombie,
// T is traced or stopped
enum ProcessState {
  Unknown = 0;          // to satisfy proto3 requirement
  Running = 82;         // ASCII 'R'
  Sleeping = 83;        // ASCII 'S'
  Uninterruptible = 68; // ASCII 'D'
  Zombie = 90;          // ASCII 'Z'
  Traced = 84;          // ASCII 'T'
}

// 进程信息
message ProcessInfo {
  // 进程id, /proc/[pid]
  uint64 pid = 1;
  // 进程名字, /proc/[pid]/status/Name
  string name = 2;
  // 进程路径, /proc/[pid]/exe
  string path = 3;
  // 启动命令, /proc/[pid]/cmdline
  string cmdline = 4;
  // 工作目录, /proc/[pid]/cwd
  string work_dir = 5;
  // 父进程id, /proc/[pid]/status/PPid
  uint64 ppid = 6;
  // 用户id, /proc/[pid]/status/Uid
  int32 uid = 7;
  // 用户名, 通过 getpwuid 获取
  string user_name = 8;
  // 组id, /proc/[pid]/status/Gid
  int32 gid = 9;
  // 进程状态, /proc/[pid]/status/State
  ProcessState state = 10;
  // 运行时长(单位为秒), /proc/uptime - (/proc/[pid]/stat/start_time[22]) / sysconf(_SC_CLK_TCK)
  double running_time = 11;
  // todo: /proc/[pid]/cgroup
  string container_id = 12;
  // 打开的文件描述符数量, /proc/[pid]/status/FDSize
  uint64 open_fd_count = 13;
  // 被动上下文切换次数, /proc/[pid]/status/nonvoluntary_ctxt_switches
  uint64 involuntary_ctx_switches = 14;
  // 主动上下文切换次数, /proc/[pid]/status/voluntary_ctxt_switches
  uint64 voluntary_ctx_switches = 15;
  // 优先级, /proc/[pid]/stat/[19]
  uint64 cpu_nice = 16;
  // 线程数量, /proc/[pid]/status/Threads
  uint64 threads_num = 17;
  // 环境变量, /proc/[pid]/environ
  repeated EnvVariable env_variables = 18;
  // 内存使用率, /proc/[pid]/statm
  ProcessMemoryUsage memory_usage = 19;

  // 读取字节数, /proc/[pid]/io/read_bytes
  uint64 iostat_read_bytes = 20;
  // 写入字节数, /proc/[pid]/io/write_bytes
  uint64 iostat_write_bytes = 21;
  // todo: 读取字节速率, diff(iostat_read_bytes) / sample_period
  double iostat_read_bytes_rate = 22;
  // todo: 写入字节速率, diff(iostat_write_bytes) / sample_period
  double iostat_write_bytes_rate = 23;

  // 用户态 cpu 使用时间, (/proc/[pid]/stat/utime[14]) / sysconf(_SC_CLK_TCK)
  uint64 cpu_user_time = 24;
  // 内核态 cpu 使用时间, (/proc/[pid]/stat/stime[15]) / sysconf(_SC_CLK_TCK)
  uint64 cpu_system_time = 25;
  // 用户态cpu 使用率, this.cpu_user_time / (/proc/uptime - this.running_time)
  double cpu_user_pct = 26;
  // Kernel CPU 使用率百分比, (this.cpu_system_time) / (/proc/uptime - this.running_time)
  double cpu_system_pct = 27;
  // CPU总体使用率: this.cpu_user_pct + this.cpu_system_pct
  double cpu_total_pct = 28;

  // 进程启动时间点, time(null) - running_time
  int64 start_time = 29;
}

// 容器
message ContainerInfo {
  // 容器id
  string id = 1;
  // 容器名字
  string name = 2;
  // 容器运行的镜像, 例如: ubuntu:latest
  string image_tag = 3;
  // 容器运行的镜像id
  string image_id = 4;
  // 容器运行的命令
  string command = 5;
  // 容器网络接受的字节数
  uint64 rx_bytes = 6;
  // 容器网络发送的字节数
  uint64 tx_bytes = 7;
  // 容器启动时间点
  uint64 start_time = 8;
  // 容器磁盘使用情况
  uint64 space_usage = 9;
}

// 磁盘信息, 不能单独借助/proc 完成
message DiskInfo {
  // 磁盘名字
  string name = 1;
  // 磁盘类型
  string type = 2;
  // 磁盘大小
  uint64 size = 3;
  // 磁盘已使用大小
  uint64 used = 4;
  // 磁盘可用大小
  uint64 free = 5;
  // 磁盘使用率
  uint64 usage = 6;
  // 磁盘挂载点
  string mount = 7;
  // 磁盘文件系统
  string fs = 8;
  // 磁盘inode使用率
  uint64 inode_usage = 9;
  // 磁盘inode总数
  uint64 inode_total = 10;
  // 磁盘生产商
  string vendor = 11;
}

// 机器信息
message NodeInfo {
  string company_uuid = 1;
  // 唯一的数据id
  uint64 host_object_id = 2;
  // 主机名字
  string host_name = 3;
  // CPU核心功能
  CpuFeature cpu_feature = 4;
  // linux内核操作系统
  string system_os = 5;
  // 内核版本
  string system_version = 6;
  // 主机类型是kvm还是虚拟机
  string system_type = 7;
  // 属于的集群
  string cluster = 8;
  // 所属平台
  string platform = 9;
  // 磁盘信息
  repeated DiskInfo disk_infos = 12;
  // 虚拟内存信息
  VirtualMemoryInfo virtual_memory_info = 13;
  // ipv4
  string ipv4 = 14;
  // ipv6
  string ipv6 = 15;
}

message NodeUsage {
  // 唯一的数据id
  uint64 host_object_id = 1;
  // cpu使用率
  uint64 cpu_value = 2;
  // memory使用率
  VirtualMemoryInfo memroy_usage = 3;
}

message NodeRes { int32 id = 1; }

message ProcessInfoRequest {
  uint64 host_object_id = 1;
  uint64 series_id = 2;
  repeated ProcessInfo processes = 3;
  string hostname = 4;
}

service NodeCollectorService {
  // 注册node信息
  rpc Register(NodeInfo) returns (NodeRes) {}
  // 更新node信息
  rpc Update(NodeUsage) returns (NodeRes) {}
  // 更新进程信息
  rpc ReportProcess(ProcessInfoRequest) returns (NodeRes) {}
}

```