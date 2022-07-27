# Towxml

Fork from [Towxml 3.2.3](https://github.com/sbfkcel/towxml)

**Towxml** 是一个可将`HTML`、`Markdown`转为微信小程序`WXML`(WeiXin Markup Language)的渲染库。用于解决在微信小程序中`Markdown`、`HTML`不能直接渲染的问题。

## 使用方法

### 构建 towxml 功能包(含组件)

1. 安装构建依赖

`npm install 或 yarn`

2. 编辑配置文件 `towxml/config.js`

3. 根据自行要求，仅保留你需要的功能即可（配置中有详细注释）

运行 `npm run build` 或 `yarn run build` 即可;

新构建出来的文件在 `dist_towxml` 目录下，将 `dist_towxml` 目录复制到你的小程序项目中并将目录名称改为`towxml`即可。

### 配置说明

考虑到并不是所有人都需要用到，默认只开启部分功能，可自行构建以开启对应功能。towxml3.0 支持以下功能：

+ [echarts图表](https://github.com/sbfkcel/towxml/wiki/3.0-Echarts%E6%94%AF%E6%8C%81)，默认禁用，需自行构建以开启此功能
+ [LaTeX数学公式](https://github.com/sbfkcel/towxml/wiki/3.0-%E6%95%B0%E5%AD%97%E5%85%AC%E5%BC%8F&yuml%E6%B5%81%E7%A8%8B%E5%9B%BE%E6%94%AF%E6%8C%81#%E5%A6%82%E4%BD%95%E6%8F%92%E5%85%A5latex%E5%85%AC%E5%BC%8F)，默认禁用，需搭建解析服务并自行构建以开启此功能
+ [yuml图表](https://github.com/sbfkcel/towxml/wiki/3.0-%E6%95%B0%E5%AD%97%E5%85%AC%E5%BC%8F&yuml%E6%B5%81%E7%A8%8B%E5%9B%BE%E6%94%AF%E6%8C%81#%E5%A6%82%E4%BD%95%E6%8F%92%E5%85%A5yuml%E6%B5%81%E7%A8%8B%E5%9B%BE)，默认禁用，需要搭建解析服务并自行构建以开启此功能
+ highlight代码高亮，默认开启（默认仅开启bash、javascript、json、python、html、css、php、scss、shell），其它语言高亮支持需自行构建以开启

### 在项目中引用

1. 将构建出来的towxml并解压至小程序项目根目录下，即（小程序/towxml）

2. 引入库 /app.js

```
// app.js
const towxml = require('/towxml/index');

App({
  towxml, // 引入`towxml3.0`解析方法
})
```

3. 在页面配置文件中引入 towxml 组件 /pages/index/index.json

```json
{
  "usingComponents": {
    "towxml":"/towxml/towxml"
  }
}
```

4. 在页面中插入组件/pages/index/index.wxml

```html
<!--index.wxml-->
<view class="container">
  <towxml nodes="{{article}}" />
</view>
```

5. 解析内容并使用/pages/index/index.js

```javascript
//获取应用实例
const app = getApp();
Page({
  data: {
    isLoading: true, // 判断是否尚在加载中
    article: {}, // 内容数据
  },
  onLoad () {
    let result = app.towxml(`# Markdown`, 'markdown', {
      base: 'https://xxx.com', // 相对资源的base路径
      theme: 'dark', // 主题，默认`light`
      events: {
        // 为元素绑定的事件方法
        tap: (e) => {
          console.log('tap', e);
        },
      },
    });

    // 更新解析数据
    this.setData({
      article: result,
      isLoading: false,
    });
  },
});
```

app.towxml(str,type,options)有三个参数

+ str 必选，html或markdown字符串
+ type 必选，需要解析的内容类型html或markdown
+ options [object] 可选，可以该选项设置主题、绑定事件、设置base等
  - base [string] 可选，用于指定静态相对资源的base路径。例如：https://xx.com/static/
  - theme [string] 可选，默认:light，用于指定主题'light'或'dark'，或其它自定义
  - events [object] 可选，用于为元素绑定事件。key为事件名称，value则必须为一个函数。例如:{tap:e=>{console.log(e)}}



## 特色

Towxml 3.0 完整支持以下功能。当然在构建时可仅保留需要功能以减少体积大小和代码依赖。

- 支持echarts图表（3.0+）✨
- 支持LaTex数学公式（3.0+）✨
- 支持yuml流程图（3.0+）✨
- 支持按需构建（3.0+）✨
- 支持代码语法高亮、代码块行号显示
- 支持emoji表情:wink:
- 支持上标、下标、下划线、删除线、表格、视频、图片（几乎绝大部分html元素）……
- 支持typographer字符替换
- 支持多主题切换
- 支持Markdown TodoList
- 支持事件绑定（这样允许自行扩展功能哟，例如：点击页面中的某个元素，更新当前页面内容等...）
- 极致的中文排版优化
- 支持前后解析数据


## 截图

以下截图即`demo`项目（文件见wiki）编译的效果

![Towxml](https://raw.githack.com/sbfkcel/blog/gh-pages/wxml_demo/demo3.x.png)


<details>
  <summary>补充说明</summary>

  [**官方交流群：182874473（点击加入）**](https://jq.qq.com/?_wv=1027&k=54KTcZi)，进群答案：wiki和issues

  ## 如何使用？

  **注意：**`3.0`切勿直接拉取代码使用，请根据自行需要构建得到最终的代码。

  > 使用遇到问题先把  wiki 中的 demo 按步骤完整跑起来。


  ### Towxml3.0文档（beta）

  以下文档仅适用于Master分支代码。

  - [3.0 构建Towxml](https://github.com/sbfkcel/towxml/wiki/3.0-%E6%9E%84%E5%BB%BATowxml)
  - [3.0 让Demo跑起来](https://github.com/sbfkcel/towxml/wiki/3.0-%E8%AE%A9Demo%E8%B7%91%E8%B5%B7%E6%9D%A5)
  - [3.0 如何使用](https://github.com/sbfkcel/towxml/wiki/3.0-%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8)
  - [3.0 Echarts支持](https://github.com/sbfkcel/towxml/wiki/3.0-Echarts%E6%94%AF%E6%8C%81)
  - [3.0 LaTex数学公式、yuml流程图支持](https://github.com/sbfkcel/towxml/wiki/3.0-%E6%95%B0%E5%AD%97%E5%85%AC%E5%BC%8F&yuml%E6%B5%81%E7%A8%8B%E5%9B%BE%E6%94%AF%E6%8C%81)
  - [3.0 在uniapp中使用towxml（感谢 @anyfar）](https://github.com/sbfkcel/towxml/issues/116)


  ### FAQ
    - 公式渲染格式不对
      - 将内容写在变量中的，请注意[公式中的特殊符号转译](https://github.com/sbfkcel/towxml/issues/138)
      - 以http形式加载内容的参考demo

  ## 打赏

  如果用着不错，可以『打赏』支持。因为有你，开源更美好。

  |微信打赏|支付宝打赏|
  |:---:|:---:|
  |![支持开源，微信打赏。](https://www.vvadd.com/wxml_demo/qrcode_wechat.png?v=1)|![支持开源，微信打赏。](https://www.vvadd.com/wxml_demo/qrcode_alipay.png?v=1)|


  ## 应用展示

  这些小程序都使用了 towxml， [查看用户提交的案例](https://github.com/sbfkcel/towxml/issues/60) 。
</details>



## License
MIT

