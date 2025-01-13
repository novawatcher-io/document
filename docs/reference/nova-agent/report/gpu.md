# GPU指标

## OLTP 上报指标

公共的上报属性: `company_uuid`, `host_object_id`, `gpu_uuid`


| 指标                     | 内容                    | 属性列表    |
| ------------------------ | ----------------------- | ----------- |
| gpu_usage                | GPU算力使用率           |             |
| gpu_memory_usage         | GPU内存使用率           |             |
| gpu_process_memory_usage | GPU内存使用率, 区分进程 | 额外增加pid |
| gpu_memory_used          | GPU已使用内存字节数     |             |
| gpu_memory_free          | GPU可用内存字节数       |             |
| gpu_temperature          | GPU温度                 |             |
| gpu_power_draw           | GPU当前输出功率         |             |
| gpu_core_clock           | GPU Core时钟频率        |             |
| gpu_pcie_tx_bandwidth    | GPU发送数据带宽         |             |
| gpu_pcie_rx_bandwidth    | GPU接收数据带宽         |             |
| gpu_ecc_errors           | GPU ECC 错误数量        |             |
