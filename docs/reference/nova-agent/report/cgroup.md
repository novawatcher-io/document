# CGroup 指标

这篇文章是对[Linux CGroup V2](https://www.kernel.org/doc/html/latest/admin-guide/cgroup-v2.html)的信息采集的详绨描述。

## 字段解释

### CGroupMount

| 字段        | 类型                                                | 描述          |
| ----------- | --------------------------------------------------- | ------------- |
| mount_point | string                                              | CGroup挂载点  |
| cgroup      | [CGroupController](#cgroupcontroller)               | CGroup控制器  |
| cpu         | [CGroupCPUController](#cgroupcpucontroller)         | CPU控制器     |
| cpuset      | [CGroupCPUSetController](#cgroupcpusetcontroller)   | CPUSet控制器  |
| hugetlb     | [CGroupHugeTLBController](#cgrouphugetlbcontroller) | HugeTLB控制器 |
| io          | [CGroupIOController](#cgroupiocontroller)           | IO控制器      |
| memory      | [CGroupMemoryController](#cgroupmemorycontroller)   | Memory控制器  |
| misc        | [CGroupMiscController](#cgroupmisccontroller)       | Misc控制器    |
| pids        | [CGroupPidsController](#cgrouppidscontroller)       | Pids控制器    |
| rdma        | [CGroupRDMAController](#cgrouprdmacontroller)       | RDMA控制器    |
| children    | [CGroupMount](#cgroupmount)                         | 子CGroup      |

### CGroupController

| 字段            | 类型                        | 来源                   |
| --------------- | --------------------------- | ---------------------- |
| controllers     | repeated string             | cgroup.controllers     |
| events          | [CGroupEvent](#cgroupevent) | cgroup.events          |
| freeze          | int32                       | cgroup.freeze          |
| max_depth       | oneof                       | cgroup.max.depth       |
| max_descendants | oneof                       | cgroup.max.descendants |
| pressure        | int32                       | cgroup.pressure        |
| procs           | repeated int32              | cgroup.procs           |
| stat            | [CGroupStat](#cgroupstat)   | cgroup.stat            |
| threads         | repeated int32              | cgroup.threads         |
| type            | string                      | cgroup.type            |

#### CGroupEvent

| 字段      | 类型  | 描述      |
| --------- | ----- | --------- |
| populated | int32 | populated |
| frozen    | int32 | frozen    |

#### CGroupStat
| 字段                 | 类型  | 描述         |
| -------------------- | ----- | ------------ |
| nr_descendants       | int32 | 后代数量     |
| nr_dying_descendants | int32 | 死亡后代数量 |


### CGroupCPUController

| 字段        | 类型                            | 来源            |
| ----------- | ------------------------------- | --------------- |
| idle        | int32                           | cpu.idle        |
| max         | [CGroupCPUMax](#cgroupcpumax)   | cpu.max         |
| max_burst   | int32                           | cpu.max.burst   |
| pressure    | [Pressure](#pressure)           | cpu.pressure    |
| stat        | [CGroupCPUStat](#cgroupcpustat) | cpu.stat        |
| stat_local  | [CGroupCPUStat](#cgroupcpustat) | cpu.stat.local  |
| uclamp_max  | int32/string                    | cpu.uclamp.max  |
| uclamp_min  | float                           | cpu.uclamp.min  |
| weight      | int32                           | cpu.weight      |
| weight_nice | int32                           | cpu.weight.nice |

#### CGroupCPUMax

| 字段   | 类型         | 描述   |
| ------ | ------------ | ------ |
| max    | int32/string | 最大值 |
| period | string       | 最大值 |


### Pressure

| 字段 | 类型        | 描述 |
| ---- | ----------- | ---- |
| some | [PSI](#psi) | some |
| full | [PSI](#psi) | full |

#### PSI

| 字段   | 类型  | 描述   |
| ------ | ----- | ------ |
| avg10  | float | avg10  |
| avg60  | float | avg60  |
| avg300 | float | avg300 |
| total  | float | total  |


#### CGroupCPUStat
| 字段                       | 类型  | 描述                       |
| -------------------------- | ----- | -------------------------- |
| usage_usec                 | int64 | usage_usec                 |
| user_usec                  | int64 | user_usec                  |
| system_usec                | int64 | system_usec                |
| core_sched_force_idle_usec | int64 | core_sched_force_idle_usec |
| nr_periods                 | int32 | nr_periods                 |
| nr_throttled               | int32 | nr_throttled               |
| throttled_usec             | int64 | throttled_usec             |
| nr_bursts                  | int32 | nr_bursts                  |
| burst_usec                 | int64 | burst_usec                 |

### CGroupCPUSetController

| 字段                     | 类型    | 来源                            |
| ------------------------ | ------- | ------------------------------- |
| cpus                     | int32[] | cpuset.cpus                     |
| cpus_effective           | int32[] | cpuset.cpus.effective           |
| cpus_exclusive           | int32[] | cpuset.cpus.exclusive           |
| cpus_exclusive_effective | int32[] | cpuset.cpus.exclusive.effective |
| cpus_partition           | string  | cpuset.cpus.partition           |
| mems                     | int32[] | cpuset.mems                     |
| mems_effective           | int32[] | cpuset.mems.effective           |

### CGroupHugeTLBController

| 字段 | 类型                                           | 描述          |
| ---- | ---------------------------------------------- | ------------- |
| tlb  | map<string, [TLBControlInfo](#tlbcontrolinfo)> | HugeTLB控制器 |


### TLBControlInfo

如下字段中, 'XXX' 是一个占位符, 一般来说指代如下的文件.

* `hugetlb.1GB.current`
* `hugetlb.2MB.current`
* `...`

| 字段         | 类型                    | 来源                     |
| ------------ | ----------------------- | ------------------------ |
| current      | int32                   | hugetlb.XXX.current      |
| events       | [TLBEvents](#tlbevents) | hugetlb.XXX.events       |
| events_local | [TLBEvents](#tlbevents) | hugetlb.XXX.events.local |
| max          | int32/string            | hugetlb.XXX.max          |
| rsvd_current | int32                   | hugetlb.XXX.rsvd.current |
| rsvd_max     | int32/string            | hugetlb.XXX.rsvd.max     |

#### TLBEvents

| 字段   | 类型         | 描述   |
| ------ | ------------ | ------ |
| max    | int32/string | max    |
| period | int32        | period |


### CGroupIOController

| 字段       | 类型                          | 来源          |
| ---------- | ----------------------------- | ------------- |
| max        | [CGroupIOMax](#cgroupiomax)   | io.max        |
| pressure   | [Pressure](#pressure)         | io.pressure   |
| prio_class | int32                         | io.prio.class |
| stat       | [CGroupIOStat](#cgroupiostat) | io.stat       |
| weight     | int32                         | io.weight     |

#### CGroupIOMax

| 字段  | 类型         | 描述                 |
| ----- | ------------ | -------------------- |
| major | int32        | 主设备号             |
| minor | int32        | 次设备号             |
| rbps  | int32/string | 每秒最大读取速度     |
| wbps  | int32/string | 每秒最大写入速度     |
| riops | int32/string | 每秒最大读取操作次数 |
| wiops | int32/string | 每秒最大写入操作次数 |

#### CGroupIOStat

| 字段        | 类型  | 描述         |
| ----------- | ----- | ------------ |
| MajorDevice | int32 | 主设备号     |
| MinorDevice | int32 | 次设备号     |
| rbytes      | int64 | 读取字节数量 |
| wbytes      | int64 | 写入字节数量 |
| rios        | int64 | 读取操作次数 |
| wios        | int64 | 写入操作次数 |
| dbytes      | int64 | 丢弃字节数量 |
| dios        | int64 | 丢弃读写次数 |

### CGroupMemoryController

| 字段            | 类型                                            | 来源                   |
| --------------- | ----------------------------------------------- | ---------------------- |
| current         | int32                                           | memory.current         |
| events          | [CGroupMemoryEvent](#cgroupmemoryevent)         | memory.events          |
| events_local    | [CGroupMemoryEvent](#cgroupmemoryevent)         | memory.events.local    |
| high            | int32/string                                    | memory.high            |
| low             | int32                                           | memory.low             |
| max             | int32/string                                    | memory.max             |
| min             | int32                                           | memory.min             |
| numa_stat       | [CGroupNumaStat](#cgroupnumastat)               | memory.numa_stat       |
| oom_group       | int32                                           | memory.oom.group       |
| peak            | int32                                           | memory.peak            |
| pressure        | [Pressure](#pressure)                           | memory.pressure        |
| stat            | [CGroupMemoryStat](#cgroupmemorystat)           | memory.stat            |
| swap_current    | int64                                           | memory.swap.current    |
| swap_events     | [CGroupMemorySwapEvent](#cgroupmemoryswapevent) | memory.swap.events     |
| swap_high       | int32/string                                    | memory.swap.high       |
| swap_max        | int32/string                                    | memory.swap.max        |
| swap_peak       | int64                                           | memory.swap.peak       |
| zswap_current   | int64                                           | memory.zswap.current   |
| zswap_max       | int32/string                                    | memory.zswap.max       |
| zswap_writeback | int32                                           | memory.zswap.writeback |

#### CGroupMemoryEvent
| 字段           | 类型  | 描述           |
| -------------- | ----- | -------------- |
| low            | int32 | low            |
| high           | int32 | high           |
| max            | int32 | max            |
| oom            | int32 | oom            |
| oom_kill       | int32 | oom_kill       |
| oom_group_kill | int32 | oom_group_kill |


#### CGroupNumaStat
todo

#### CGroupMemoryStat
todo

#### CGroupMemorySwapEvent

| 字段 | 类型  | 描述 |
| ---- | ----- | ---- |
| high | int64 | high |
| max  | int64 | max  |
| fail | int64 | fail |

### CGroupMiscController
todo

### CGroupPidsController
| 字段    | 类型         | 来源         |
| ------- | ------------ | ------------ |
| current | int32        | pids.current |
| events  | int32        | pids.events  |
| max     | int32/string | pids.max     |
| peak    | int32        | pids.peak    |

### CGroupRDMAController
todo
