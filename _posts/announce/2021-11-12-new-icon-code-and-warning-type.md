---
title: 天气图标和预警代码变更
ref: new-icon-code-and-warning-type
---

从2021年12月1日起（或使用SDK 4.7+），天气数据服务数据的变更：新增2种天气图标代码、新增月相图标以及预警类型ID的变更。

## 1. 新增天气图标代码

所有天气图标代码新增151和152两个代码，表示夜晚的多云和少云。新的天气图标代码说明请参考            <https://dev.qweather.com/docs/resource/icons/>

## 2. 新增月相图标代码和字段

在月升月落和月相/逐天预报接口中，新增`moonPhase.icon`字段，并且我们提供了月相的图标。

## 3. 预警类型ID的变更

从9月份开始，我们陆续扩大了天气预警的覆盖国家，目前已经支持40+个国家或地区，为了便于统一各国或地区的天气预警类型，我们对原有的预警类型进行了重新编码。新旧的预警类型代码均可参考 <https://dev.qweather.com/docs/resource/warning-info/>

并且在[和风天气图标](https://icons.qweather.com/)项目中，我们也提供了对应的预警类型图标。

## 何时变更？

### Web API

在2021年12月1日（含）起，所有新创建的免费开发版应用和商业版应用，将执行上述变更。

为了便于适配新的变更，针对2021年12月1日（不含）之前创建的应用，我们将陆续根据下列时间表进行升级：

|            | 开始升级      | 完成升级       |
| ---------- | ------------- | -------------- |
| 开发版应用 | 2021年12月1日 | 2021年12月31日 |
| 商业版应用 | 2022年3月1日  | 2022年3月3日   |

### iOS SDK/Android SDK

上述变更将在[iOS SDK 4.7+](https://dev.qweather.com/docs/ios-sdk/) 及 [Android SDK 4.7+](https://dev.qweather.com/docs/android-sdk/)版本中生效，无论你使用的是开发版应用或者商业版应用。

在2021年12月1日起新创建的应用，仅可使用iOS SDK/Android SDK 4.7+版本。

### 不想等陆续升级

请在2021年12月1日后创建新的应用和KEY，用新的KEY替换旧的KEY即可。

商业版用户也可以提交工单与我们联系，我们可提供额外的协助。

## 有何影响？

一般来说，没有特别重要的影响，但是请注意以下几件事情：

- 如果你用到了我们的天气图标或自己的图标，你可能需要同步一下最新的天气图标代码。
- 如果你需要使用月相图标，请使用月相接口中新增的icon字段。
- 如果你依赖于预警类型ID，即warning.type字段，那么你可能需要同步一下最新的预警类型。

## 需要帮助

请给我们提交工单，我们将协助你解决。
