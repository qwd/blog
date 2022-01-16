---
title: Web API中必须使用Gzip压缩
ref: gzip-is-required-in-api
---

Web API v7版本返回的数据默认采用Gzip压缩，你可以选择禁止使用Gzip压缩。

从2022年3月1日起，我们将陆续在Web API v7中强制使用Gzip压缩，不再支持返回未经压缩的数据。因此如果你之前使用的是未压缩数据，请尽快在你的程序中对数据进行gzip解压缩的处理。
