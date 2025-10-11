# 告警客户端配置

 > 通过点击 告警管理 > 告警策略 > 告警客户端配置,对客户端进行配置.


| 表单名         | 类型 | 描述 |
|-------------|  | --- |
| 模版名称       | 字符串	| 定义告警客户端名称 |
| 方法       |	选择数据 |	● GET ● POST ● PUT |
| HTTP地址      |	字符串 |	服务器地址例如: http://localhost:8080 |                                                                                             |
| 超时时间 |	数字 |	单位时间是秒，设置http 客户端最大超时时间 |
| 渲染模版 |	字符串 |	上报渲染的模板内容 |


## 模板渲染内容


渲染模板推荐配置:

```text
{
    "alerts":
          [
          {{$first := true}}
          {{range .Events}}
          {{$time := ._meta.timestamp}}
          {{$reason := ._meta.reason}}
          {{range ._meta.SelectAlert}}
          {{if $first}}{{$first = false}}{{else}},{{end}}
          {
                "labels": {
                  "device_id": "{{.DeviceId}}",
                  "template_id": "{{.TemplateId}}",
                  "data_id": "{{.DataId}}",
                  "alert_id": "{{.AlertId}}",
                  "group_id": "{{.GroupId}}",
                  "context": "{{.Context}}",
                  "message": "{{.Message}}"
                },
                "annotations": {
                  "reason": "{{$reason}}"
                },
                "startsAt": "{{$time}}",
                "endsAt": "{{$time}}"
          }
          {{end}}
          {{end}}
          ],
          {{$first := true}}
          {{range .Events}}
          {{if $first}}
          "commonLabels": {
            "module": "{{._meta.additions.module}}",
            "alertname": "{{._meta.additions.alertname}}",
            "cluster": "{{._meta.additions.cluster}}"
          }
          {{$first = false}}
          {{else}}
          {{end}}
          {{end}}
}
```

alert字段解释：

| `字段`              | `是否内置` | `含义`                  |
|-------------------|--------|-----------------------|
| _meta             | 是      | alert元数据              |
| _meta.pipelineName |       | 表示pipeline名称              |
| _meta.sourceName  |       | 表示source名称              |
| _meta.timestamp   |       | 表示日志时间戳              |
| reason            | 是      | 匹配成功原因                |
| fields            | 否      | field字段，由其余配置添加       |
| _additions        | 否      | 由配置指定                 |
| DeviceId         | 是      | 设备id                 |
| AlertId         | 是      | 告警策略id                 |
| GroupId         | 是      | 无用字段                 |
| Context         | 是      | 告警上下文                 |
| Message         | 是      | 报警信息                 |

## 创建客户端

通过创建告警客户端，把网关的数据发送到服务器，创建完成后通过绑定告警策略,下发到客户端生效

![add_alert_template](/doc/assets/img/alert/add_alert_template.png)

填写表单，保存客户端


![add_alert_template_form](/doc/assets/img/alert/add_alert_template_form.png)

## 修改客户端

点击修改按钮，修改客户端

![update_alert_template](/doc/assets/img/alert/update_alert_template.png)

## 删除客户端

点击删除按钮，删除客户端

![delete_alert_template](/doc/assets/img/alert/delete_alert_template.png)