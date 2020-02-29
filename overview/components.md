---
title: Style components
description: Learn how components work in the Mapbox Studio style editor.
contentType: reference
order: 3
tag: beta
prependJs:
- "import Browser from '@mapbox/dr-ui/browser';"
- "import Note from '@mapbox/dr-ui/note';"
- "import Video from '@mapbox/dr-ui/video';"
- "import YouAreHere from '../../components/illustrations/you-are-here';"
- "import ComponentProperty from '../../video/overview-components-component-property.mp4';"
- "import Eject from '../../video/overview-components-eject.mp4';"
- "import LayerProperty from '../../video/overview-components-layer-property.mp4';"
- "import Override from '../../video/overview-components-override.mp4';"
- "import StyleComponentBetaNote from '../../components/temporary/style-component-beta-note.js';"
- "import RelatedPage from '@mapbox/dr-ui/related-page';"
---

<p className="txt-l">样式组件通过优化样式的常修改的属性并，使其能通过下拉选项中，滑块和切换进行修改，这让样式自定义变得更便捷好用。</p>

{{ <StyleComponentBetaNote /> }}

{{
  <YouAreHere
    activeItems={["Template style", "Custom style"]}
  />
}}

## 组件是什么？

**组件** 是以地图类要素的集合，具有相同的样式风格的一个单元。组件可以包括多种类型的特征（例如，填充，线条和符号）。比如道路网络和行政边界是组件的示例。每个组件包含多个**图层**。

**图层** 就是单一类型地图要素的一个集合。比如桥图层。在Mapbox Streets风格中，桥图层是Road网络组件中五十多个图层中的一种。组件不一定包含图层。非组件图层被称为 **自定义层**.

自定义图层是独立的自定义图层，不能添加到组件中或者通过组件设置样式。


## 使用组件为地图设置样式

 Property 在Mapbox Studio中有包括**图层属性**和**组件属性**两种不同的术语解释。两者均指样式化地图要素的选项，但它们的工作方式有所不同。

### 组件属性

**组件属性**是单个风格组件的选项之一。单个组件属性可以控制跨多个图层的多个图层属性。通常使用切换（打开或关闭），下拉菜单或带有刻度的滑动按钮来定义组件属性的值。
{{<RelatedPage contentType='video' title="How to style a map using components" vimeoId='378466157' vimeoThumbnail="/studio-manual/img/video/how-to-style-using-components.jpg">}}
了解如何在Mapbox Studio中使用样式组件。
{{</RelatedPage>}}

行政边界宽度是“ 行政边界”组件中组件属性的一个示例。行政边界宽度的值是通过沿滑动按钮来确定的。此组件属性是通过改变包括admin-0-boundary，admin-1-boundary，admin-0-boundary-bg，和admin-1-boundary-bg在内的图层中的要素宽度而实现的。 `admin-0-boundary`, `admin-1-boundary`, `admin-0-boundary-bg`, and `admin-1-boundary-bg`.

{{
    <Browser>
        <Video
            src={ComponentProperty}
            title="Adjust the Country boundaries width component property and see the width of boundaries change on the map."
        />
    </Browser>
    <br />
}}

{{<Note title="Component properties and the Mapbox Style Specification">}}
与图层属性不同，组件属性与[Mapbox样式规范](https://docs.mapbox.com/mapbox-gl-js/style-spec/) 不直接相关，并且运行时不能在Mapbox Studio外部进行编辑。
{{</Note>}}

####颜色和排版属性

在使用组件构建地图样式，通过修改底部**组件** 卡上的颜色和排版相关的属性选项来确定布局的**颜色**和**排版**。在 [颜色](/studio-manual/reference/styles/#colors) 和 [排版](/studio-manual/reference/styles/#typography) 的参考中了解更多信息。

### 图层属性

**图层属性**是诸多用于编辑单图层风格中的一种，通常比组件属性提供更细粒度的控制。线图层的宽度是图层属性的一个示例，width属性的值是代表像素的数字。

{{
    <Browser>
        <Video
            src={LayerProperty}
            title="Go to the Layers tab and click on the admin-0-boundary layer, set a manual override for the width property, clear the current value, and type in a different value."
        />
    </Browser>
    <br />
}}

图层属性直接与 [Mapbox样式规范中](https://docs.mapbox.com/mapbox-gl-js/style-spec/) 概述的绘画和布局属性对应。**自定义图层** 只能使用图层属性设置样式，而组件中的图层可以使用组件属性和图层属性替代的组合设置样式（详细信息如下）。

## 在组件的基础上进行定制

在使用组件属性设置样式的图层中，有两个选项可用于自定义图层属性。您可以**覆写**由组件属性设置的图层属性的值，也可以**释放**该组件。

### 覆写

当你**覆写**图层属性的某个值时，它只会影响图层中的一个属性，并且手动覆盖可以随时恢复。

{{
    <Browser>
        <Video
            src={Override}
            title="Set a manual override to set color across a zoom range."
        />
    </Browser>
    <br />
}}

覆盖适用于自定义特定不同图层中的具体属性。

###释放

当你**释放**一个组件，图层属性就不能在作为统一集合进行编辑。例如，以Mapbox Streets样式弹出道路网络组件，将导致你需要对超过50个图层的风格进行逐个定义。
释放组件后，图层将继续使用从初始组件属性继承的图层属性，直到你对其进行手动编辑。在此之后，所有图层就必须直接使用图层属性进行编辑。**一旦释放一个组件，就无法撤消**。

{{<RelatedPage contentType='video' title="How to eject a style component" vimeoId='378704089' vimeoThumbnail="/studio-manual/img/video/how-to-eject-a-style-component.jpg">}}
了解如何在Mapbox Studio中释放样式组件来更好地控制图层。
{{</RelatedPage>}}


当您想在同一组件中的多个层之间更改许多层属性时，弹出组件可能是合适的方式。当您要对组件中的图层重新排序或在单个组件中的图层之间放置自定义图层时，就不得不释放了。

{{
    <Browser>
        <Video
            src={Eject}
            title="Eject a component and view the resulting individual layers."
        />
    </Browser>
}}

###自定义组件

无法构建自定义组件或从现有组件中添加或删除各个图层。

##使用组件本身的样式

由带有组件的地图生成的JSON样式将遵循Mapbox样式规范，并且可以像 [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/), [iOS](https://docs.mapbox.com/ios/maps/overview/) 和 [Android](https://docs.mapbox.com/ios/maps/overview/),移动Maps SDK 以及我们的 [Static Images API](https://docs.mapbox.com/api/maps/#static-images) 任何其他Mapbox地图样式一样使用。

使用Mapbox GL JS或我们的移动Maps SDK时，您可以在运行时与各个图层进行交互，添加和删除以及更改**图层属性**，但是**组件**运行时属性是**无法改变的**。组件属性只能在Mapbox Studio样式编辑器中进行编辑。
