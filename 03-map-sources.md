# Map sources

## Examples of use

### GeoJSON {#geojson}

**GeoJSON** is an open standard format designed for representing simple geographical features, along with their non-spatial attributes. More details at: https://geojson.org

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

<img src="/assets/feature_collection-01.jpg" width="360" height="640"/>

Import the file https://gurumaps.app/example/feature_collection.geojson to see on the map, forests, trees and rivers near Baranovichi. You can import any of your GeoJSON files in Guru Maps and use them as overlays on top of the base map.

### GeoJSON + MapCSS {#geojson_mapcss}

**MapCSS** is a CSS-like language for map stylesheets. It's used to define how data from GeoJSON should be displayed on map.

```css
node[natural=tree] {
    icon-image: "circle.svgpb."
    icon-tint: red;
    image-allow-overlap: true;
}
node[natural=tree][leaf_cycle=evergreen] {
    icon-tint: green;
}
```

<img src="/assets/feature_collection-02.jpg" width="360" height="640"/>

Together with the `feature_collection.geojson` file from the previous step, import the file https://gurumaps.app/example/feature_collection.mapcss. Here is its content:


After importing, only trees will remain visible on the map. Evergreen trees will be marked with green circles and all other trees will be marked with red circles.

For any `.geojson`, you can add your own `.mapcss` style to customize when, how and which data should be shown.

### Map Source `.ms` for vector data {#msForVector}

Import the file http://gurumaps.app/example/vector_source1.ms. Here's the contents:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customMapSource overlay="true">
    <name>GeoJSON from url</name>
    <geojson url="https://gurumaps.app/example/feature_collection.geojson"/>
</customMapSource>
```

It automatically downloads the data from `https://gurumaps.app/example/feature_collection.geojson` after the import.

Consider the file http://gurumaps.app/example/vector_source2.ms.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customMapSource overlay="true">
    <name>GeoJSON with autoupdate</name>
    <geojson url="https://gurumaps.app/example/feature_collection.geojson" updateInterval="5"/>
    <style url="https://gurumaps.app/example/feature_collection.mapcss"/>
</customMapSource>
```

Tags `<geojson>` and `<style>` may contain `url` attribute with an address to the data and `updateInterval` attribute with update check interval in minutes, as well as data or a block `<![CDATA[ ]]>` with **GeoJSON** data inside. For example http://gurumaps.app/example/vector_source3.ms.

<img src="/assets/feature_collection-03.jpg" width="360" height="640"/>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customMapSource overlay="true">
    <name>GeoJSON and Style embed in MS</name>
    <minZoom>3</minZoom>
    <maxZoom>9</maxZoom>
    <geojson>
{
    "type": "Feature."
    "properties." {},
    "geometry." {
        "type": "MultiPolygon."
        The "coordinates." [[[ [0.0, 0.0], [10.0, 0.0], [10.0, 10.0], [0.0, 10.0] ],
                        [ [2.0, 2.0], [ 8.0, 2.0], [ 8.0, 8.0], [2.0, 8.0] ]],
                        [[ [30.0,0.0], [40.0, 0.0], [40.0, 10.0], [30.0,10.0] ],
                        [ [32.0,2.0], [38.0, 2.0], [38.0, 8.0], [32.0, 8.0] ]]]}
}
    </geojson>
    <style>
        area|z3-{fill-color: green; width:1pt; color:red;}
    </style>
</customMapSource>
```

GeoJSON data and style are contained within a `.ms` file and are independent of external sources. 

### Raster map `.sqlitedb` or `.mbtiles` and Map Source {#msForRasterOffline}

For raster maps you can define additional parameters in `.ms` file. For example, you can make a `map.sqlitedb` raster map an overlay by adding the following content to `map.ms`: 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customMapSource overlay="true">
</customMapSource>
```

Note `.sqlitedb` file and `.ms` file share common name `map`.

In addition, you can specify the `<name>` of the map, `<minZoom>` the minimum and `<maxZoom>` maximum zoom level when data should be downloaded, and `overzoom` whether to show the enlarged tiles if the user zoomes closer max zoom.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customMapSource overlay="true" overzoom="true">
    <name>Raster map with extra params</name>
    <minZoom>8</minZoom>
    <maxZoom>12</maxZoom>
</customMapSource>
```

### Online map sources {#msForRaster}

Let's check https://ms.gurumaps.app/ms/OpenStreetMap.ms

```xml
<?xml version="1.0" encoding="UTF-8"?>
    <customMapSource>
    <name>OpenStreetMap</name>
    <url>http://{$serverpart}.tile.openstreetmap.org/{$z}/{$x}/{$y}.png</url>
    <serverParts>a b c</serverParts>
</customMapSource>
```

If `<url>` tag is set, map source will download online raster tiles. The following parts will be inserted into the template from `<url>`:

* `{$serverpart}` - random server name from `<serverParts>`.
* `{$x}`, `{$y}`, `{$z}` - tile address
* `{$quad}` - [Quad tile address](https://wiki.openstreetmap.org/wiki/QuadTiles)
* `{$bbox}` - Tile bbox in SRID 3857. Typically used for WMS servers.
* `{$invX}`, `{$invY}` - inverted coordinates. `N-x` and `N-y`, where `N` is the number of tiles on the current scale.

You can find more online raster map source examples at: https://ms.gurumaps.app