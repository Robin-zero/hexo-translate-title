## hexo-translate-title-plus
使用Google翻译，百度翻译和有道翻译将Hexo中的汉字标题转成英文标题，配置完成后直接翻译，无需手工修改标题内容

**注：由于原作者一直未更新最新的版本到 npm 仓库，特 fork 此项目，发布后供自己使用，也欢迎大家一起使用！**

## 安装与使用

[![NPM](https://nodei.co/npm/hexo-translate-title-plus.png?compact=true)](https://npmjs.org/package/hexo-translate-title-plus)

### 安装

```bash
npm install hexo-translate-title-plus --save
```

### 使用

#### 1.配置hexo根项目下的`_config.yml`

```yml
translate_title:
  translate_way: google  # google,youdao,baidu_with_appid,baidu_no_appid
  youdao_api_key: '' # Your youdao_api_key
  youdao_keyfrom: xxxx-blog # Your youdao_keyfrom
  is_need_proxy: false     # true | false
  proxy_url: http://localhost:50018 # Your proxy_url
  baidu_appid: '' # Your baidu_appid
  baidu_appkey: '' # Your baidu_appkey
  rewrite: false # is rewrite true | false 
```
**注意**：

> * 判断是否需要配置google本地代理，因为我在本地是开启时才能访问google翻译的，如果没有被墙，请将`_config.yml` 下的`is_need_proxy: true`改为false。如果设置为true,请设置本地代理地址
> * 目前google翻译，youdao翻译均可直接使用，百度翻译**使用APPID版本，无APPID版本均已完成**，APPID版本需要在[百度翻译开放平台](http://api.fanyi.baidu.com/)
> * 如果担心百度翻译开发平台的APP_ID和APP_KEY有泄漏风险，建议在百度翻译开发平台-》管理控制台的服务器地址一栏，填写好服务器IP即可

#### 2.修改hexo根目录下的`_config.yml`

修改

> permalink: :year/:month:day/:translate_title.html

将`:title`修改为`:translate_title`即可，前面的路径也可按照自己的要求变更，例如 permalink: blog/:translate_title.html

## 改进之处
1. 使用了ES6的很多新特性，例如变量声明使用了const和let， 函数体使用async/await同步操作等
2. 原有百度翻译API发生变化，重写了百度翻译的翻译逻辑
3. 对于翻译的标题内容，去除标点符号，空格转换为横线连接，并剔除重复单词

## 版本历程

### V1.0.12
1. 添加`rewrite` 参数，默认为`false`，判断如果存在`translate_title`则不进行翻译，如果为`true`则强制翻译，慎用！

### V1.0.11
1.添加`request`库依赖，`hexo`安装时候会报错

### V1.0.10
1. ~~修复引用错误，将`request`库引用注释掉~~

### V1.0.9

1. 修复[issue#8](https://github.com/cometlj/hexo-translate-title/issues/8)中提出的问题，在设置相同翻译器情况下，如果`translate_title`中有值，并且和翻译接口获取的翻译内容一致时，不做生成静态页和写入md文件操作。

### V1.0.8

版本对标-npm

### V1.0.7

1. 合并 [ChaosTong](https://github.com/ChaosTong) 同学提交的PR,修正在在选择有appid版本百度翻译接口时，`hexo s`启动服务器时会一直调用翻译接口bug。

### v1.0.6

1. 新增百度无appid功能，不需要申请百度翻译开放平台账号即可直接使用

### v1.0.5

1. 添加async/await函数，引入`request-promise`请求操作库


## TODO

1. google 获取TKK的时候，是参照[这篇文章](http://blog.csdn.net/life169/article/details/52153929)里面的JS计算方式(谢谢作者！)，但是更换为初次获取`http://translate.google.cn/`TKK值，参与计算获取tk时会计算出错，原因待查中。
2. 百度无appid版本仍然需要固化token和header中的Cookie值，尚未完成动态获取及拼接Cookie值的操作，对端百度翻译接口会返回`Error 998-Cookie超时`的错误，目前没有什么好的解决方法，如果有哪位朋友知道的欢迎issue给我😄

## 翻译效果评估
Google翻译 > Baidu翻译 > 有道翻译

## DEMO
[R 喵呜的小窝](https://rshow.top/)

## License
MIT
