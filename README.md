# NewWxComment

`NewWxComment`[https://github.com/yicm/NewWxComment](https://github.com/yicm/NewWxComment)是一个微信小程序的评论组件，结合BaaS提供商[LeanCloud](https://leancloud.cn/)，无需其他另外的个人或者云服务器，就可以免费使用。解决了需要个人去注册域名、备案、购买云服务器的繁杂问题。且兼容`Valine`[https://github.com/xCss/Valine](https://github.com/xCss/Valine)评论，打通PC端和移动端评论，特别适合使用Valine评论系统且想同时开发小程序文章评论的同学们。

> ps: 打造这个插件的目的在于本人想要打造一个类似hexo通用博客框架，且是一个移动端的框架，首先采用微信小程序实现，现已完成博文编译器的开发，评论插件的开发(打通PC端Valine插件)，微信小程序的经典主题开发（未发布）,期待发布经典主题后，有更多开发者加入，开发更多的插件和主题，一起打通PC端和"现在移动端"，实现移动端的个人博客；

> Hexo博客编译器已开源[https://github.com/yicm/HMP](https://github.com/yicm/HMP)，直接打通静态博客和微信小程序，Demo可微信搜索`小白AI博客`查看。

> 先提前“剧透”下经典主题首页，倾心打造：

![image](https://raw.githubusercontent.com/yicm/NewWxComment/master/screenshots/Xiaobaiai.jpg)


# 特色

- 独立插件，独立放入小程序项目即可使用
- 打通Valine评论系统，统一PC端和小程序端
- 友好的UI界面和交互界面
- 与微信用户信息绑定，显示微信用户头像和昵称
- 支持文章阅读量统计功能
- 支持评论回复功能，即子评论
- 支持emoji表情显示😉
- 支持评论分页加载
- 支持评论分页参数设置
- 内置获取微信用户公共信息授权
- 支持light/dark两种主题
- 机型兼容友好，包括全面屏iphone11等

# 已测试通过机型

- iphone6s plus
- iphone11/xr
- ipad4 pro
- redmi6 pro

# 屏幕截图

下图为`NewWxComment`嵌入式到具体博客中显示的效果。PC端评论效果可以访问网站[https://xiaobaiai.net](https://xiaobaiai.net)

![image](https://raw.githubusercontent.com/yicm/NewWxComment/master/screenshots/NewWxComment.png)

# 快速入手

> 注意：下面的前三步也可以参考Valine评论插件方法，如果是Valine已经设置好了，直接跳过前三步；

1. 注册LeanCloud账号，并创建过LeanCloud应用；

2. 登陆LeanCloud账号，打开链接[https://leancloud.cn/docs/weapp-domains.html](https://leancloud.cn/docs/weapp-domains.html)，将显示域名配置到你的微信小程序服务器配置中；

3. 设置小程序的 AppID 与 AppSecret
    3.1 登录 微信公众平台，在`设置` > `开发设置` 中获得 AppID 与 AppSecret
    3.2 前往 LeanCloud `控制台` > `组件` > `社交`，保存「微信小程序」的 AppID 与 AppSecret

4. 克隆Demo项目NewWxComment(Demo项目已附带NewWxComment组件)

```
$ git clone https://github.com/yicm/NewWxComment.git
```

5. 将LeanCloud自己的AppID和AppKey复制到NewWxComment.js对应位置；

```
AV.init({
    appId: 'your leancloud appid',
    appKey: 'your leancloud appkey',
});
```

6. 在小程序index.wxml和index.json文件中已经引入NewWxComment组件

index.wxml

```
<NewWxComment id="NewWxComment" articleTitle="关于我" articleURL="/2019/20190727172958.html" contentLen='1' articleID="/2019/20190727172958.html"></NewWxComment>
```

index.json

```
"usingComponents": {
    "NewWxComment": "/component/NewWxComment/NewWxComment"
}
```

index.js中添加触底才获取评论数据：

```
// 到底触发获取评论数据函数
// 添加触发拉取评论函数
onReachBottom: function() {
    let newWxComment = this.selectComponent('#NewWxComment');
    newWxComment.onReachBottom();
}
```
如果评论格数显示不正常，检查app.js `container`样式：

```
.container {
    padding: 0 24rpx;
    background-color: #fff;
    font-family: Microsoft YaHei, Helvetica, Arial, sans-serif;
}
```

NewWxComment组件属性说明：

```bash
articleTitle: 待评论页文章标题
articleURL: 待评论页文章链接(不包含网站域名)
homeURL: 小程序首页路径
pageSize: 评论每页加载条数，默认值5
contentMinLen: 评论最小长度要求，默认值2
contentMaxLen: 评论最大长度限制，默认值300
articleID: 待评论文章唯一ID
websiteURL: PC端网站域名(若无可不填)，默认值`https://xiaobaiai.net`
theme: 主题设置，仅支持 light 或者 dark 两个属性值
```

# Demo

小程序`小白AI博客`引用NewWxComment组件示例：

![](https://gitee.com/yicm/Images/raw/master/xiaobaiai/news/10004_2.jpg)

# TODO

- 支持点赞列表
- 支持作者回复高亮标志
- 支持垃圾评论过滤
- 支持海报分享
- 支持赞赏
- ...

# License

[Mulan PSL v1](http://license.coscl.org.cn/MulanPSL)


