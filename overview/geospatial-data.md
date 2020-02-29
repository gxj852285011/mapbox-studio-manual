---
title: Geospatial data
description: Learn how uploading data works in Mapbox Studio.
order: 4
prependJs:
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import YouAreHere from '../../components/illustrations/you-are-here'"
  - "import Browser from '@mapbox/dr-ui/browser';"
  - "import Video from '@mapbox/dr-ui/video';"
  - "import ChevronousText from '@mapbox/mr-ui/chevronous-text';"
  - "import TilesetUpload from '../../video/tileset-upload.mp4';"
contentType: guide
---

<p className="txt-l">使用Mapbox Studio，您可以上传并管理添加到地图的自定义数据。.</p>

{{
  <YouAreHere
    activeItems={["Upload", "Dataset", "Tileset"]}
  />
}}

##可上传数据类型

将自定义数据上传到Mapbox帐户时可以选择[**Datasets**](https://www.mapbox.com/help/define-dataset) 和 [**tilesets**](https://www.mapbox.com/help/define-tileset) 两种格式。如果要上传数据并在添加到地图之前对其进行编辑，请作为**Datasets**进行上传。如果您要上传数据以直接添加到地图中，请上传**tilesets**格式。

{{<Note>}}
如果要上传栅格数据，则必须作为切片数据进行上传。
{{</Note>}}

###上传您可以编辑的数据（datasets）

当您上传**dataset**时，可以在Mapbox Studio Studio [dataset 编辑器](https://www.mapbox.com/studio/datasets/)对数据进行编辑，添加或删除要素几何（点，线和面）和属性（属性）。完成编辑后，需要将其保存并导出为图块集以将其添加到样式中。

{{
  <Browser>
    <img src="/studio-manual/img/studio/dataset-modify-feature.gif" alt="" />
  </Browser>
}}

### 上传数据到地图(tilesets)

**Tilesets**是矢量或栅格数据的轻量级集合，已针对渲染进行了优化，并且不可编辑，但可以在Mapbox Studio样式编辑器中设置样式。当您将矢量数据作为图块集上传时，它会被简化并切成可直接用于您的样式的矢量图块。数据转换为图块集后，将无法再对其进行编辑。

{{
  <Browser>
    <Video
      src={TilesetUpload}
      title="Working with an uploaded tileset in the style editor"
    />
  </Browser>
}}

## 准备要上传的数据

Mapbox Studio 允许您上传用于地图样式的个人自定义数据。您可以在 [Tilesets page](/studio-manual/reference/tilesets/#upload-file)上传文件。

为了顺利进行上传，它需要确保符合以下条件：

-地理空间数据已投影到 [Web Mercator](https://en.wikipedia.org/wiki/Web_Mercator) (EPSG:3857).
- [GeoJSON](https://www.mapbox.com/help/define-geojson/) 文件语法验证为正确。
- 不必要的属性已被删除。

### 使用API上传

您也可以使用 [Mapbox Uploads API](https://www.mapbox.com/api-documentation/maps/#uploads) 上传如何条件的文件，该文件会转换为 tileset。借助 Uploads API，Mapbox 将为您提供了一个能被启动和监视临时S3存储桶。

### 可接受的文件类型和传输限制

数据集和图块集上传的可接受文件类型和传输限制包括：
|File type|Datasets|Tilesets|Transfer limits
|---|:---:|:---:|:---:|
| [CSV](https://www.mapbox.com/help/define-csv) | {{<Icon name='check' inline={true} />}} | {{<Icon name='check' inline={true} />}} |  datasets 为 5 MB, tilesets 为 1 GB |
| [GeoJSON](https://www.mapbox.com/help/define-geojson) | {{<Icon name='check' inline={true} />}} | {{<Icon name='check' inline={true} />}}</span> |  datasets 为 5 MB, tilesets 为 1 GB |
| [MBTiles](https://www.mapbox.com/help/define-mbtiles) | | {{<Icon name='check' inline={true} />}} | 25 GB
| [KML](https://www.mapbox.com/help/define-kml) | | {{<Icon name='check' inline={true} />}} | 15 层之内不超过 260MB
| [GPX](https://www.mapbox.com/help/define-gpx) | | {{<Icon name='check' inline={true} />}} | 260 MB |
| [Shapefile](https://www.mapbox.com/help/define-shapefile) | | {{<Icon name='check' inline={true} />}} |  `.shp` 和 `.dbf` 文件未压缩的情况下不超过260 MB ，且您必须将 shapefile 作为压缩.zip文件上传。 |
| [GeoTIFF](https://www.mapbox.com/help/define-tiff) | | {{<Icon name='check' inline={true} />}} | 10 GB |

如果您的文件大小超过了这些限制，或者遇到错误，请参阅我们的 [故障排除指南](https://www.mapbox.com/help/uploads/).

{{<Note>}}
可以无限制地将多个文件上传到同一数据——每次需要加载5 MB。&mdash; 的大小不受限制，但是Mapbox Studio数据集编辑器只能显示20 MB及以下的数据集。这些数据集仍然可以从Mapbox Studio下载并通过 [Datasets API](https://www.mapbox.com/api-documentation/maps/#datasets) 访问。
{{</Note>}}

###缩放级别和简化

在 Mapbox Studio 完成上传后，它被渲染成一个 [tileset](https://www.mapbox.com/help/define-tileset/)。创建图块集后，偶尔会以较低的缩放级别简化数据，以降低数据的复杂性，并确保每个图块都小于一定大小。Mapbox Studio这样做是为了使您的地图在不关注细节的地方更快的加载。

上传的图块集也具有缩放范围。此缩放范围是可视要素的总缩放范围，该范围在 [tileset 信息页](/studio-manual/reference/tilesets/#tileset-information-page) 上列出。如果您需要在不同的缩放范围内看到图块集，可以 [手动进行调整](https://www.mapbox.com/help/adjust-tileset-zoom-extent/).

{{<Note>}}
矢量图块的缩放范围会影响生成图块的缩放级别。这是因为数据的缩放级别不同而导致的：矢量tilesets可样式多达22级缩放级别，对于高于缩放范围的缩放级别将使用可用的最大缩放图块设置样式。
{{</Note>}}

## 有关tilesets的更多信息

有关如何在Mapbox Studio中上传和管理图块的更多信息，请参见Tileset。

{{
  <a href='/studio-manual/reference/tilesets/' className="unprose txt-bold link">
    <ChevronousText text="Read about tilesets" />
  </a>
}}

## 有关 datasets 的更多信息

有关如何在 Mapbox Studio 中上传、管理和编辑数据集的更多信息，请参见“Datasets”部分。

{{
  <a href='/studio-manual/reference/datasets' className="unprose txt-bold link">
    <ChevronousText text="Read about datasets" />
  </a>
}}

## 解决常见的上传错误

上传有问题吗？试试我们的故障排除指南。

{{
  <a href='/studio-manual/help/#troubleshooting' className="unprose txt-bold link">
    <ChevronousText text="View troubleshooting guides" />
  </a>
}}
