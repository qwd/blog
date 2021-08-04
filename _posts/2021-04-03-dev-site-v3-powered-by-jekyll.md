---
title: 使用Jekyll创建和风天气开发平台
tag: story
image: /assets/upload/jekyll-and-dev-qweather.png
---

![和风天气开发平台网站](/assets/upload/jekyll-and-dev-qweather.png)

最近我们对[和风天气开发平台](https://dev.qweather.com)进行了新的改版，几乎重构了所有文档和网页，功能上支持了中英文双语，并使用大量模版减轻文档编辑的工作。和风天开发平台依旧使用[Jekyll](https://jekyllrb.com/)创建并托管在[Github](https://github.com/qwd/dev-site)。
<!-- more -->

对于选择静态网页生成工具，我们使用过Jekyll、Hexo和Hugo，Jekyll和Hexo非常简单容易上手，Hugo学习成本稍微高一点，但是胜在速度非常非常快，这篇文章并非是这三款工具的对比，只是简单介绍一些我们使用Jekyll创建和风天气开发平台的一些感受。

假设你已经安装好了Jekyll，那么现在可以通过`git clone https://github.com/qwd/dev-site.git`下载和风天气开发平台网站的源代码。为了便于理解，我简单介绍一下和风天气开发平台的目录结构：

```
根目录
├── _data //数据文件目录，包括文档中使用的一些参数说明、API地址、中英文翻译等等
│   ├── api-endpoint.yml  //API地址列表
│   ├── t.yml  //中英文翻译
│   ├── p.yml  //API传入参数
│   └── ...  //其他数据文件
├── _docs_en //英文文档目录
├── _docs_zh //中文文档目录
├── _includes //这个怎么翻译呢？可以理解为一些模版、代码片段
│   ├── doc-bc.html  //文档页面包屑导航
│   ├── footer.html  //页脚
│   ├── right-sidebar.html  //侧边栏
│   └── ...  //其他includes
├── _layouts  //页面模版
│   ├── html.html  //基础模版
│   ├── docs.html  //文档页模版
│   └── ...  //其他模版
├── _sass  //scss样式文件
├── _snippets  //API返回结果的json样例
├── assets  //资源文件，包括样式、图片等
│   ├── css  //css文件，自动通过_sass中的样式文件生成
│   ├── favicon  //所有favicon
│   ├── images  //图片
│   └── ...  //其他资源文件
├── _pages_en //英文静态页面
├── _pages_zh  //中文静态页面
│   ├── 404.html  //404页面
│   ├── index.html  //首页
│   ├── help  //帮助目录
│   └── ...  //其他静态页面
├── _config.yml  //配置文件
├── build.sh  //一键build脚本
├── favicon.ico  //favicon.ico
├── robots.txt  //robots.txt
└── sitemap.xml  //忘了为什么要自己写一个sitemap，你完全可以用jekyll-sitemap这个插件自动生成
```

这次改版，我们的目标主要有：

- 支持多语言
- 简化编辑工作，易于批量修改
- 不使用Github Pages不支持的插件

## 支持多语言

与Hugo不同，Jekyll原生并没有任何多语言的支持和选项，只能通过插件实现，但由于网站是托管在Github Pages上，又不想每次编译后在发布，所以还是要自己想办法啊。让Jekyll支持多语言，只需要做四件事：

1. 在每篇文章添加一个front matter
2. 设置页面语言
3. 添加一个多语言文件
4. 在任何页面上可以切换对应语言

### Front Matter

我们在每篇需要多语言的文章中增加一个相同的标识，比如和风天气开发平台网站上使用的是`ref`，如果A文章（中文）是`ref: qweather`，那么对应这篇文章的英文版本B文章则也是`ref: qweather`，现在就将中英文版本的同一篇文章通过`ref`关联起来了。

### 设置页面语言

我们还是使用front matter来确定每个页面是哪种语言，你可以在一个页面中直接添加一个front matter，比如`lang: zh`，不过一般来说你会有很多页面，那么简单的方式就是在_config.yml中批量添加这个front matter，例如和风天气开发平台的[_config.yml](https://github.com/qwd/dev-site/blob/master/_config.yml)：

```yaml
- scope:
    path: pages_zh
    type: pages
  values:
    layout: html
    lang: zh
    permalink: "/:basename/"
- scope:
    path: pages_en
    type: pages
  values:
    layout: html
    lang: en
    permalink: "/en/:basename/"
```

这样在pages_zh下的所有页面的`lang`都被设置为`zh`，在pages_en下的所有页面的`lang`都被设置为`en`。稍后我们可以通过`page.lang`来判断这个页面是什么语言。

### 添加一个多语言文件

文章的中英文版本通过front matter搞定了，那么一些模版文字，例如导航目录、页脚等等如何处理呢？我们在_data目录下创建一个t.yml文件（文件名随便，一个字母只是为了方便敲代码），将这些非文章内使用的多语言写进去，这其实就是一个多语言文件。

你可以这样写：

```yaml
en:
  home: Home
  about: About
  register: Register
  login: Login
zh: 
  home: 首页
  about: 关于
  register: 注册
  login: 登录
```

也可以这样写：

```yaml
home: 
  en: Home
  zh: 首页
about:
  en: About
  zh: 关于
register: 
  en: Register
  zh: 注册
login: 
  en: Login
  zh: 登录
```

如果我们有一个模版，就可以直接使用上边的参数来替代实际的文字，例如

```html
<nav>
  <ul>
    <li>{% raw %}{{ site.data.t[page.lang].home }}{% endraw %}</li>
    <li>{% raw %}{{ site.data.t[page.lang].about }}{% endraw %}</li>
    <li>{% raw %}{{ site.data.t[page.lang].register }}{% endraw %}</li>
    <li>{% raw %}{{ site.data.t[page.lang].login }}{% endraw %}</li>
  </ul>
</nav>
```

其中`[page.lang]`这个变量就是判断当前页面是什么语言，然后获取对应的内容。

### 切换对应语言

现在我们能够通过`page.lang`和`ref`知道当前页面是什么语言，也知道了对应的多语言页面是哪一个，那么如何进行切换呢？请参考和风天气开发平台中的[lang-selector.html](https://github.com/qwd/dev-site/blob/master/_includes/lang-selector.html)

```liquid
{% raw %}
{%- assign node = site.documents | where: "ref", page.ref | sort: 'lang' %}
{%- for item in node %}
<a {%- if page.lang == item.lang %} class="active"{%- endif %} href="{{ item.url }}">{{ site.data.t[item.lang].langcode }}</a>
{%- endfor %}
{% endraw %}
```

原理也很简单，找出`ref`相同的文章，循环出这些文章的链接，如果当前页面的链接和其中循环结果相同，则增加一个`active`的样式。

## 简化编辑，易于修改

在上一个版本中，每个API文档都是一个字一个字敲出来的，如果有变动或者错误，需要一个文件一个文件的修改，即便是批量修改也需要大量时间去找规则然后还要去校验。这个版本中，我们将大量重复或者规范的文档内容都做成了数据文件和模版文件，修改和添加只需要更改对应的少数文件即可，对编写文档的技术人员来说，增加了不少摸鱼时间XD

例如所有API的请求参数都存放在[_data/p.yml](https://github.com/qwd/dev-site/blob/master/_data/p.yml)文件中，请求参数的模版在[_includes/params.html](https://github.com/qwd/dev-site/blob/master/_includes/params.html)，最终一篇天气预报API的markdown文档只有如下内容，而实际上展示的内容[有这么多](https://dev.qweather.com/docs/api/weather/weather-now/)。

```markdown

全球城市未来15天天气预报，包括：日出日落、月升月落、最高最低温度、天气白天和夜间状况、风力、风速、风向、相对湿度、大气压强、降水量、降水概率、露点温度、紫外线强度、能见度等。

### 请求URL

{% raw %}{% include api-url.html flag="weather-daily" %}{% endraw %}

### 请求参数

请求参数包括必选和可选参数，如不填写可选参数将使用其默认值，参数之间使用`&`进行分隔。

{% raw %}{% include params.html p="location key lang unit" %}{% endraw %}

### 返回数据

{% raw %}{% include api-snippet.html flag="weather-daily" %}{% endraw %}

{% raw %}{% include api-response.html group="weather" type="daily" prefix="daily" %}{% endraw %}

```

## 不使用Github Pages不支持的插件

Github Pages上支持的Jekyll插件基本上可以说是这也不支持，那也不支持，所以像上述的多语言就需要自己去写，在这次和风天气开发平台v3的改版中，就面临需要处理几个功能：

- Table of Contents
- SEO tag
- Anchor链接

### Table of Contents

一般的技术文档都非常需要TOC，而markdown本身无法生成TOC，我们大概花了一天的时间想去自己写一个TOC模版，但是没有成功，然后就搜索到了[Jekyll-toc](https://github.com/allejo/jekyll-toc)这个纯Liquid版的TOC，还支持各种参数定义，非常的膜拜。

### SEO tag

Jekyll-seo-tag这个插件是Github Pages支持的，可以生成网页标题、描述、Open Graph、JSON-LD等等SEO友好的标签，但是，由于网站是多语言的，Jekyll-seo-tag无法针对多语言生成适合的标签，于是我们自己写了一个[SEO模版](https://github.com/qwd/dev-site/blob/master/_includes/seo.html)，当然这个模版仅限和风天气开发平台网站使用，并非放之四海皆准的插件，仅供参考。

### Anchor链接

既然可以通过在页面中实现TOC，说明可以用类似的方法获取到H2、H3之类的标签，那么自然也可以获取到对应的anchor链接。经过反复的实验（并没有），结果喜人，因为还是TOC的作者[allejo](https://github.com/allejo/)搞出了[jekyll-anchor-headings](https://github.com/allejo/jekyll-anchor-headings)，又一个纯Liquid的模版，再次膜拜。

## 总结

以上就是使用Jekyll创建和风天气开发平台v3版本的几点经验分享，感谢收看🙏