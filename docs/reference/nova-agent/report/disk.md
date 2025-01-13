# 磁盘指标

## OLTP指标

OLTP的上报属性: `host_object_id, device`

| 指标     | 内容                |
| -------- | ------------------- |
| 读取速率 | 磁盘每秒读取速度    |
| 写入速率 | 磁盘每秒写入速度    |
| 使用率   | 已用空间/磁盘总大小 |

## GRPC上报指标

| 字段        | 类型                  | 描述                 |
| ----------- | --------------------- | -------------------- |
| device      | string                | 磁盘设备             |
| type        | [DiskType](#disktype) | 磁盘类型             |
| mount_point | string                | 磁盘挂载点           |
| filesystem  | string                | 磁盘文件系统         |
| vendor      | string                | 磁盘生产商           |
| space_total | uint64                | 磁盘大小(byte)       |
| space_free  | uint64                | 磁盘可用大小(byte)   |
| space_used  | uint64                | 磁盘已使用大小(byte) |
| space_usage | double                | 磁盘使用率           |
| inode_total | uint64                | 磁盘inode总数        |
| inode_free  | uint64                | 磁盘inode可用数      |
| inode_used  | uint64                | 磁盘inode已使用数    |
| inode_usage | uint64                | 磁盘inode使用率      |

### DiskType

```protobuf
enum DiskType {
  Unkonwn = 0;
  SSD = 1;
  HDD = 2;
}
```
