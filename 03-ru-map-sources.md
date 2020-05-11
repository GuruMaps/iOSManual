# Источники карт

## Примеры использования

### GeoJSON

GeoJSON - это универсальный формат для обмена гео-информацией. Он простой и удобный 

Импортируйте файл https://gurumaps.app/example/feature_collection.geojson чтобы увидеть на карте, леса, деревья и реки рядом с Барановичами. Вы можете импорировать любой свой файл GeoJSON.

### GeoJSON + MapCSS

Вместе с файлом feature_collection.geojson из предыдущего шага импортируйте файл https://gurumaps.app/example/feature_collection.mapcss. Вот его содержимое:

```css
node[natural=tree] {
    icon-image: "circle.svgpb";
    icon-tint: red;
    image-allow-overlap: true;
}
node[natural=tree][leaf_cycle=evergreen] {
    icon-tint: green;
}
```

После импорта на карте останутся видны только деревья. Вечнозеленые будут отмечены зелеными кружками, а всех остальные деревья - красными.

Для любого geojson можно добавить свой стиль mapcss, чтобы настроить какие данные и как надо показывать.

### Map Source (.ms) for vector data

Импортируйте файл http://gurumaps.app/example/vector_source1.ms. Вот его содержимое:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customMapSource overlay="true">
    <name>GeoJSON from url</name>
    <geojson url="https://gurumaps.app/example/feature_collection.geojson"/>
</customMapSource>
```

Он автоматически скачает данные по адресу `https://gurumaps.app/example/feature_collection.geojson` после импорта.

Рассмотрим файл http://gurumaps.app/example/vector_source2.ms

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customMapSource overlay="true">
    <name>GeoJSON with autoupdate</name>
    <geojson url="https://gurumaps.app/example/feature_collection.geojson" updateInterval="5"/>
    <style url="https://gurumaps.app/example/feature_collection.mapcss"/>
</customMapSource>
```

Теги `geojson` и `style` могут содержать в себе аттрибуты `url` c адресом к данными и `updateInterval` с интервалом проверки обновлений в минутах, а так же данные или блок `<![CDATA[ ]]>` с данными внутри. Например в http://gurumaps.app/example/vector_source3.ms.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customMapSource overlay="true">
    <name>GeoJSON and Style embed in MS</name>
    <minZoom>3</minZoom>
    <maxZoom>9</maxZoom>
    <geojson>
{
    "type": "Feature",
    "properties": {},
    "geometry": {
        "type":"MultiPolygon",
        "coordinates": [[[ [0.0, 0.0], [10.0, 0.0], [10.0, 10.0], [0.0, 10.0] ],
                        [ [2.0, 2.0], [ 8.0, 2.0], [ 8.0,  8.0], [2.0,  8.0] ]],
                        [[ [30.0,0.0], [40.0, 0.0], [40.0, 10.0], [30.0,10.0] ],
                        [ [32.0,2.0], [38.0, 2.0], [38.0,  8.0], [32.0, 8.0] ]]]}
}
    </geojson>
    <style>
        area|z3-{fill-color: green; width:1pt; color:red;}
        line{width:1pt; color:yellow;}
    </style>
</customMapSource>
```

Данные GeoJSON и стиль содержатся внутри файла .ms и не зависит от внешних источников. 

### Raster map (.sqlitedb or .mbtiles) + Map Source

Для растровых карт вы можете определить дополнительные параметры в .ms файле. Так например растровую карту `map.sqlitedb` можно сделать оверлеем, добавив в `map.ms` следующее содержимое: 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customMapSource overlay="true">
</customMapSource>
```

Кроме того можно указать имя карты, минимальный и максимальный масштаб, когда из этой карты надо загружать данные, и следует ли показывать увеличенные тайлы, если пользователь приблизится сильнее.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customMapSource overlay="true" overzoom="true">
    <name>Raster map with extra params</name>
    <minZoom>8</minZoom>
    <maxZoom>12</maxZoom>
</customMapSource>
```

Чтобы `map.ms` файл был использован для карты `map.sqlitedb`, у них должно быть одинаковое имя. В нашем случае - это `map` но может быть любое другое.

### Онлайн источники карт

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customMapSource> 
    <name>Google Maps Satellite EN HD</name>
    <minZoom>0</minZoom>
    <maxZoom>20</maxZoom>
    <url>http://{$serverpart}.google.com/vt/lyrs=y@176103410&amp;x={$x}&amp;y={$y}&amp;z={$z}&amp;s=Galileo&amp;hl=en&amp;scale=2</url>
    <serverParts>mt0 mt1 mt2 mt3</serverParts>
</customMapSource> 
```

Если задан url - источник будет скачивать онлайн растровые тайлы. В шаблон из `<url>` будут вставлены следующие части:

* {$serverpart} - случайное имя сервера из `<serverParts>`
* {$x}, {$y}, {$z} - адрес тайла
* {$quad} - [Quad tile address](https://wiki.openstreetmap.org/wiki/QuadTiles)
* {$bbox} - Tile bbox in SRID 3857. Typically used for WMS servers.
* {$invX}, {$invY} - инвертированные координаты. N-x и N-y, где N число тайлов на текущем масштабе.

## Стиль карты

## Оверлеи

Оверлеи - это слои с дополнительной информацией, которые показаны поверх карты. Овелеем может быть GeoJSON файл, или растровый источник. Рассмотрим все по порядку.

## Векторные данные из GeoJSON

* Самый простой способ показать GeoJSON на карте - импортировать его в приложение.

[картинка с GeoJSON данными на карте]

* Вместе с GeoJSON можно импортировать и MapCSS файл, чтобы настроить правила отображения для GeoJSON.

### Данные в GeoJSON

Данные в GeoJSON содержат два основных поля, это `properties` и `geometry`. `properties` содержит теги и значения описывающие объект. Например, имя, тип, описание, число полос для дорог. По параметрам из `properties` стиль может выбрать каким цветом и на каком уровне приближения рисовать эти данные.  

```json
{
    "type": "Feature",
    "properties": {
        "@id": "node/524678909",
        "leaf_cycle": "evergreen",
        "leaf_type": "needleleaved",
        "natural": "tree",
        "species": "Pícea",
        "species:ru": "Ель"
    },
    "geometry": {
        "type": "Point",
        "coordinates": [
            26.0211965,
            53.1146981
        ]
    },
    "id": "node/524678909"
}
```

### MapCSS

Файл стиля MapCSS состоит из правил, которые применяются к каждому объекту сверху-вниз.

Например стиль:

```css
node[natural=tree] {
    icon-image: tree.svgpb;
}
```

отобразит картинку tree.svgpb для точек у которых тег natural имеет значение tree.

Каждое правило в стиле состоит из двух частей. Запроса `node[natural=tree]` и параметров `icon-image: tree.svgpb;`. Запрос выбирает к каким объектам надо применить параметры.

Рассмотрим сложный запрос:

```css
node,area|z15-[railway=station]
```

Он состоит из:

1. фильтра по типу `node,area`. Он может быть `node` для точек, `line` для линий, `area` для полигонов. Если надо указать несколько типов они разделяются запятой. Так же можно использовать `*`, если тип не важен.
2. фильтра масштаба `z15-`. Он указывает для каких масштабов должно срабатывать правило. Может быть только минимальным масштабом `z8-`, или интервалом `z3-9`. В таком случае правило будет применено для на масштабах с 3-го по 8 включительно.
3. фильтра параметров `[natural=tree]`. Такой фильтр оставит только объекты у которых тег `natural` имеет значение `tree`. Чтобы оставить только объекты у которых есть любое значение тега `natural` следует использовать фильтр `[natural]`. Чтобы оставить объекты у которых нету значения тега `natural` используется фильтр `[!natural]`

Параметры управляют отображением объектов на карте. Guru Maps поддерживает следующий набор параметров:

* Draw order params
  * layer
  * z-index
* Polygon params
  * fill-color  
  * fill-image
  * color - border color
  * width - border width
* Line params
  * color - line color
  * width - line width
  * casing-color
  * casing-width
  * dashes
  * dashes-color
  * dashes-width
  * linecap
    * none
    * square
    * round
  * linejoin
    * round
    * miter
    * bevel
    * auto
* Text params
  * text
  * font-weight
    * bolder
    * bold
    * normal
    * light
    * ligther
  * font-stroke-width
  * font-stroke-color
  * text-color
  * text-priority
  * text-allow-overlap
  * icon-image
  * icon-scale
  * icon-tint
  * icon-offset-x
  * icon-offset-y
  * image-allow-overlap
