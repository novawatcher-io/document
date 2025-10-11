# 智能预警

使用神经网络算法对时序数据进行定期扫描,预测未来发生的数据趋势,如果未来预测的数据，超过配置阀值，则发出报警

## 配置

| 表单名         | 类型 | 描述 |
|-------------|  | --- |
| 预警名称       | 字符串	| 预警的名称 |
| 预警测点       |	字符串 |	预警测点,网关上报的时序数据 |
| 预测模型      |	字符串 |	对时序数据进行预测的神经网络模型:<br/> ● 预测-Arima <br/> ● 预测-STLForecaster <br/> ● 预测-NaiveForecaster <br/> ● 预测--ExponentialSmoothing |
| 聚合函数 |	字符串 |	对时序数据进行聚合的函数:<br/> ● SUM <br/> ● COUNT <br/> ● AVG <br/> ● MAX_VALUE <br/> ● MIN_VALUE |
| 预测时长 |	选择数据 |	查询数据的时间段:<br/> ● 1天前 <br/> ● 1周前 <br/> ● 1个月前 <br/> ● 3个月前 <br/> ● 半年前 <br/> ● 1年前 |
| 预测长度 |	数值 |	预测的时间段数据测点数 |
| 预测阀值 |	数值 |	比如说阀值为10,预测未来30个点位的数据，如果10个测点被规则租匹配到就发出告警 |
| 模型推理策略 |	选择数据 |	从告警管理中的告警AI推理选择一个策略。 |
| 通知处理 | 字符串 |	从告警管理中的告警处理配置选择一个策略。 |
| 规则组-键名 | 数值 |	我们使用混合相似度得分来评估两行文本之间的距离。 它是加权关键词相似度和向量余弦相似度。 如果查询和块之间的相似度小于此阈值，则该块将被过滤掉。默认设置为 0.2，也就是说文本块的混合相似度得分至少 20 才会被召回。 |
| 规则组-操作符 | 数值 |	● ><br/> ● =<br/> ● <。 |
| 规则组-测点值 | 数值 |	时序数据的数据值。 |
| 规则组-匹配类型 | 选择数据 |	● 全部成立<br/> ● 全部成立成立任意一个 |

## 新建预警策略

点击新建按钮，新增智能预警

![save_prediction](/docs-assets/img/ai/prediction/save_prediction.png)

填写表单，点击保存，保存预警策略

![save_prediction_form](/docs-assets/img/ai/prediction/save_prediction_form.png)

点击修改，修改预警策略

![update_prection](/docs-assets/img/ai/prediction/update_prection.png)

点击删除，删除预警策略

![delete_prection](/docs-assets/img/ai/prediction/delete_prection.png)