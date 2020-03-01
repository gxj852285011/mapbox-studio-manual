---
title: Publish your style
description: Learn how to publish map styles made in Mapbox Studio.
order: 5
prependJs:
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import constants from '../../constants.json';"
  - "import YouAreHere from '../../components/illustrations/you-are-here';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import AppropriateImage from '../../components/appropriate-image';"
contentType: guide
---

<p className="txt-l">当你完成数据添加和样式设置后，下一步就是将其添加到Web或移动应用程序中。本节内容为使用已发布样式进行发布的所有操作。</p>

{{
  <YouAreHere
    activeItems={["Publish"]}
  />
}}

##草稿与产品样式

对于您在Mapbox Studio中创建的每种样式，都有**草稿**和**产品样式URL**可用：
- 使用**草稿**样式URL可以快速迭代样式并获得相关反馈，而不会影响已在产品程序中已经开始使用的地图样式。
- 当你为产品程序中的终端用户准备好样式后，便可开始使用**产品**样式URL。

在样式编辑器中对样式进行编辑时，更新的样式将作为草稿保存在您的帐户中。**风格草稿网址**将包括所有的修改，以你的风格到这一点。在制作风格URL将只包括你击球之前已进行了修改 [**Publish**](#publish) 按钮。

{{<Note title="Do not use draft styles in production applications" theme="warning">}}
草稿样式的URLs用于原型设计和迭代——它们会存入缓存并且受到严格的速率限制。由于速率限制，在生产应用程序中使用草稿样式的URL可能会导致性能下降和终端用户的地图显示空白。因此，**草稿样式URL不应该在产品中使用**。
{{</Note>}}

<!-- add toggle video -->

##发布

当你在产品中使用样式之前，需要在样式编辑器中发布样式。在样式编辑器中对样式进行编辑时，更新的样式将作为草稿保存在您的帐户中。在没有按下 [**发布**](/studio-manual/reference/styles/#publish-style) 按钮之前，**在样式编辑器中进行的更改将不会反映在样式的生产版本中**。

{{
  <AppropriateImage
    imageId="overview-publish-share-production"
    alt="publish modal"
  />
}}


## 共享按钮

在样式编辑器内部，顶部工具栏中有一个**“共享”**按钮。此按钮将为你打开一个模态窗口，它包含了包括分享或使用你的草稿样式以及已经在产品中使用的样式的所有设置。

对于样式的草稿版本和生产版本，通常会有三种使用样式的选项：

- **共享**:  你可以与任何人共享的URL。
- **开发**: 方便地访问在各种平台上使用样式所需的资源
- **下载**: 下载具有JSON样式和所有必要资产的压缩文件夹。

阅读以下有关每个选项获得更多信息。

{{
  <AppropriateImage
    imageId="overview-publish-share-draft"
    alt="screenshot of the share and use modal"
  />
}}

### 共享网址

在**共享** URL提供了一个地图样式的临时地址。它为您提供了一种与他人共享地图并获得反馈的便捷方法，以便于在设计上进行协作或展示您的创意作品。单击剪贴板按钮{{}}，并将其粘贴到浏览器窗口中便可查看您的样式。

### 开发

为了让你能在web、移动或第三方程序中使用你的自定义样式风格，分享模式中为您提供了 URL 和 访问Token。[风格 URL](https://docs.mapbox.com/help/glossary/style-url/) 是根据你的地图风格生成的，结合访问 Token，它让您可以通过[Mapbox 的产品](https://docs.mapbox.com/)对其进行访问和调用。

#### 样式网址

例如`mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}`,一个完整的样式URL 由三个组件组成：

- `mapbox://styles`: 指向Mapbox的样式API
- `/mapbox`: 您的Mapbox用户名
- `/streets-v{{constants.VERSION_STREETS_STYLE}}`: 您样式的唯一ID

如果您使用的是样式的草稿版本， `/draft` 还将添加到样式URL的末尾。

{{<Note>}}
`mapbox://styles` 样式的符号是完整的样式API URL的别名 `https://api.mapbox.com/styles/v1/streets-v{constants.VERSION_STREETS_STYLE}`.
{{</Note>}}

####访问Token

Mapbox使用 [**访问Token**](https://docs.mapbox.com/help/glossary/access-token)将您账户中的产品及工具进行关联。每个帐户都有一个默认的公共访问Token，但是您也可以创建新的访问Token。您可以在 [帐户”页面](https://account.mapbox.com) 上找到访问Token。

####平台类

为您切换项目相关的平台提供相关资源。
##### Web程序

我们在**网页**使用Mapbox GL JS提供必要的资源以用于初始化地图风格。

[Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js) 是一个JavaScript库，用于创建具有Mapbox样式的交互式地图。该API利用GL驱动的地图的功能，包括平滑缩放，地图方位和俯仰以及可用于浏览器中的交互和样式设置的矢量数据。您可以使用在Mapbox Studio样式编辑器中创建的自定义样式，也可以使用我们提供的默认样式，并以编程方式添加包括GeoJSON、图像以及 [video](https://docs.mapbox.com/mapbox-gl-js/example/video-on-a-map/)在内的其他数据！

有关在Mapbox.js或Leaflet中使用Mapbox Studio样式的信息，请参见下面的 [Mapbox.js和Leafle相关](#mapboxjs-and-leaflet) 。

{{<Note title="Right-to-left support in Mapbox GL JS">}}
 Mapbox Studio会加相应的 [`mapbox-gl-rtl-text`](https://github.com/mapbox/mapbox-gl-rtl-text) 插件，默认情况下会添加对阿拉伯语和希伯来语文本的支持。该插件未与 Mapbox GL JS 捆绑在一起。必须使用 [`setRTLTextPlugin`](https://docs.mapbox.com/mapbox-gl-js/api/#setrtltextplugin)  在 Mapbox GL JS 中的方法进行设置。
{{</Note>}}

##### iOS，Android和Unity

在**iOS**，**安卓**，**Unity**中，我们提供了相关 SDK资源以便于您使用我们的移动地图。

#####第三方

我们为包括ArcGIS Online的，Tableau，CARTO和Fulcrum在内的第三方程序中提供了能让您使用自定义地图样式的相关资源

Mapbox模板样式和在Mapbox Studio中设计的自定义样式都带有 **WMTS端点**，可用于将样式添加到桌面GIS应用程序中。您可以将以下端点与任何自定义样式一起使用：

```
https://api.mapbox.com/styles/v1/YOUR_USERNAME/YOUR_STYLE_ID/wmts?access_token=YOUR_ACCESS_TOKEN
```
这个 **WMTS 端点** 可以让你在以下平台使用地图：

- **ArcMap**: 在ArcGIS Desktop 10+中可用。请参阅有关 [在ArcMap中将Mapbox图层添加为WMTS](https://docs.mapbox.com/help/tutorials/mapbox-arcgis-qgis/#add-mapbox-maps-in-arcmap) 的文档以开始使用。
- **QGIS**: QGIS 2.0+中提供此功能。请参阅有关 [在QGIS中将Mapbox图层添加为WMTS](https://docs.mapbox.com/help/tutorials/mapbox-arcgis-qgis/#add-mapbox-maps-in-qgis) 文档以开始使用。

### 下载

下载一个包含您样式的所有内容的zip文件，包括遵循 [Mapbox样式规范](https://docs.mapbox.com/mapbox-gl-js/style-spec/) 的JSON文档，包含该样式中使用的所有图标和图像以及该样式中使用的所有字体的 [sprite](https://docs.mapbox.com/help/glossary/sprite) 。你可以将其存储在本地，在文本编辑器中更改，上传到您的帐户或与其他Mapbox Studio 用户共享。

## Mapbox.js和Leaflet

您可以使用 [Mapbox 静态图块API](https://docs.mapbox.com/api/maps/#static-tiles) 将Mapbox Studio样式与其他Web映射库（如Mapbox.js和Leaflet）一起使用，根据Mapbox Studio的样式生成栅格图块。

### Mapbox.js

[Mapbox.js](https://docs.mapbox.com/mapbox.js) 是我们较早的JavaScript Web映射库，它扩展了当下流行的 [Leaflet.js](http://leafletjs.com) 库。你可以通过 Mapbox.js使用Mapbox Studio样式作为底图来创建交互式地图。请注意，使用Mapbox.js并不能提供Mapbox Studio样式可用的所有功能。
Mapbox.js {{constants.VERSION_MAPBOXJS}}及以上版本支持使用以下 `styleLayer`方法从Mapbox Studio添加样式：

```js
L.mapbox.styleLayer('mapbox://styles/YOUR_USERNAME/YOUR_STYLE_ID').addTo(map);
```

请参阅Mapbox.js文档中的 [完整示例](https://docs.mapbox.com/mapbox.js/example/v1.0.0/stylelayer/)。


### Leaflet

[Leaflet](https://leafletjs.com/) 是用于移动友好型交互式地图的开源JavaScript库。您可以使用带有以下 [`L.TileLayer`](https://leafletjs.com/reference-1.3.2.html#tilelayer) 类的端点将Mapbox Studio样式添加到Leaflet地图：

```
https://api.mapbox.com/styles/v1/YOUR_USERNAME/YOUR_STYLE_ID/tiles/256/{z}/{x}/{y}?access_token=YOUR_ACCESS_TOKEN
```


## 归属和服务条款

无论您是使用Mapbox Studio创建自定义样式还是使用Android SDK构建移动应用，所有Mapbox工具均受我们的 [归属条约](https://docs.mapbox.com/help/how-mapbox-works/attribution/) 和 [服务条款约束](https://www.mapbox.com/tos)。有关这两个要求的更多信息，请 [联系Mapbox支持](https://support.mapbox.com).
