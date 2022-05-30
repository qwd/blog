---
title: 天气预警level字段弃用
ref: warning-levle-is-deprecated
---

我们在2022年5月28日发布了API v7.10版本，在本次更新中，[天气预警](https://dev.qweather.com/docs/api/warning/weather-warning/)的`warning.level`字段已被标记为弃用状态，我们将采用新的`warning.severity`和`warning.severityColor`代替。

> 注意：API v7.10将采用灰度升级，最晚在2022年6月10日全部升级完成。

随着我们发布越来越多的国家和地区的天气预警，原`warning.level`已经无法满足需求，对于不同国家和地区，无法正确的表示当地预警的严重程度，因此我们引入了新的数据：

- **severity：**表示当前预警的严重等级，与**level**类似，但是使用更加规范的方式进行定义
- **severityColor：**表示当前预警的严重等级所优选的颜色，对于不同国家和地区，可能更加倾向于使用颜色而非文字来描述当前预警信息的严重程度，我们尊重和适配了这些国家和地区的习惯，通过增加**severityColor**字段来补充当前预警严重等级的信息。

查看[预警信息文档](https://dev.qweather.com/docs/resource/warning-info/)了解新增预警字段的详细描述。

### 如何升级

1. 对于获取中国预警信息，你可以直接使用`warning.severityColor`进行替代，同时通过`warning.severity`获取预警严重等级的文字描述，但是请注意下述第三条。
2. 对于获取其他国家和地区的预警信息，你可以通过`warning.severity`进行替代，同时通过`warning.severityColor`获取预警严重等级的对应颜色。
3. 请注意，`warning.severity`和`warning.severityColor`的返回数值**仅支持英文**。

### 不升级会怎么样

- 在2023年6月1日之前，你可以正常使用原`warning.level`，这不会有任何变化。
- 在2023年6月1日之后，原`warning.level`可能不会再返回数据。

因此建议请在2023年6月1日前完成升级。



