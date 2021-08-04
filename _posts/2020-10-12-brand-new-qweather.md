---
title: 和风的新名字QWeather
excerpt: 从今天起，和风天气的域名和英文名称正式变更为QWeather，我们将继续提供更好的更漂亮的天气服务
image: /assets/upload/hew2qw.png
tag: news
ref: newqw
---

有件事情要和大家宣布一下，随着我们官方APP：QWeather上线运营一年并收获了数百万用户后，我们决定将QWeather作为和风天气新的品牌名称和网站域名，这也避免了一些用户对于HeWeather和QWeather两个名字的困扰，无论是我们的APP还是气象数据服务，从现在开始都统一为 **QWeather**。

![heweather2qweather](/assets/upload/hew2qw.png)

随着新名字的启用，我们也将开启新的征程，例如:

* 官方微博上线了，请[@和风天气](https://weibo.cn/qweather)点赞吧
* 微信订阅号上线了
* 3年前天气数据服务部署在我们全球10大数据中心之后，现在APP和网站也已经完全实现全球化部署，并支持多语言访问
* 重构的了我们的数据服务，平均响应速度提高了10%，各类API接口的带宽占用降低了15%

更改名称对于大部分QWeather APP和QWeather网站的用户来说这些变化都是没有感知的，但是对于我们的开发者来说，由于我们将变更所有的域名为 `qweather.com`，因此需要注意一些事情：（当然，以下所有变化都将在你方便的时候进行一次调整即可）

* 新的开发者平台为 <https://dev.qweather.com> ，你仍然可以在Github上查看这个网站的源码
* 我们在Github地址变更为 <https://github.com/qwd/>
* 在使用我们天气数据的地方需要变更数据来源的标识，参考<https://www.qweather.com/about/brand>
* SDK发布了新的版本，除了进一步提高了SDK性能以外，其中一些方法名将变更为QWeather
* API地址将变更为：

    | API名称         | API新地址                       | 文档                                                  |
    | --------------- | ------------------------------- | ----------------------------------------------------- |
    | 商业版API       | https://api.qweather.com        | [文档](https://dev.qweather.com/docs/api/)            |
    | 开发版API       | https://devapi.qweather.com     | [文档](https://dev.qweather.com/docs/api/)            |
    | 城市地理查询API | https://geoapi.qweather.com     | [文档](https://dev.qweather.com/docs/api/geo/)        |
    | 历史数据API     | https://datasetapi.qweather.com | [文档](https://dev.qweather.com/docs/api/historical/) |

最后剧透一下，更多重磅天气产品将陆续发布！