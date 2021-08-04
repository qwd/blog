---
title: GeoAPI v2发布
excerpt: 全新的GeoAPI v2版本已经上线。GeoAPI v2大幅增加了数据内容，提高了获取数据的灵活性，简化了层级并拥有一切可能的扩展性。
image: /assets/upload/geoapi-v2.jpg
tag: dev
ref: apiv7
---

![GeoAPI v2](/assets/upload/geoapi-v2.jpg)

随着[Web API v7版本](/post/webapi-v7-released/)的发布，GeoAPI也迎来了最新版本（v2）。

在GeoAPI v2版本中，我们增加了两个新的API：

- POI信息的查询：用于查询景点、港口等POI信息
- POI范围查询：可以根据坐标点半径查询所有POI信息

在API数据中，我们也额外增加了更多实用的数据，以便开发者可以更好的将地理信息与天气数据结合，例如

- `isDst`: 所查询城市是否处于夏令时
- `utcOffset`: 城市与UTC时间的偏移小时数 
- `rank`: 城市的评分

另外，与Web API v7一样，GeoAPI v2同样支持全新的多语言和全球自动路由功能，并且在全球各个城市的名称上，我们也提供的本地语言名称和多语言名称。

更多详情，查看GeoAPI v2的开发文档：<https://dev.qweather.com/docs/api/geo/>
