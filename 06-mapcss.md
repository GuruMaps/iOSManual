# MapCSS

The MapCSS style file consists of rules that apply to each object from top to bottom.

For example, a style:

```css
node[natural=tree] {
    icon-image: tree.svgpb;
}
```

will display a picture of `tree.svgpb` for points where the tag `natural` has the value `tree`.

Each rule in the style consists of two parts. Filter `node[natural=tree]` and draw parameters `icon-image: tree.svgpb;`. The query chooses which objects to apply the parameters to.

This documentation describes the MapCSS dialect used in the Guru Maps application. Some drawing parameters have not been implemented, preprocessing macros have been added, and a different list of functions is used for the evaluated operations. The style used in Guru Maps can be found in the [repository](https://github.com/GalileoApp/MapStyle).

## Filters

Let's consider a sophisticated filter:

```css
node,area|z15-[railway=station]
```

It consists of:

1. filter by type `node,area`. It can be `node` for points, `line` for lines, `area` for polygons. If you need to specify several types, they are separated by a comma. You can also use `*` if the type is not important.
2. zoom filters `z15-`. It specifies for which zoom leves the rule should be triggered. It can be only the minimum zoom level `z8-`, or the interval `z3-9`. In this case the rule will be applied on zoom levels 3 to 8 inclusive.
3. parameter filters `[natural=tree]`. Such a filter will leave only objects that have the `natural` tag with the value `tree`. To leave only objects that have any value of the `natural` tag, you could use the filter `[natural]`. To leave the objects that don't have the `natural` tag, use the filter `[!natural]`.

## Preprocessing macros

### @import

Inserts the content of the specified file.

```css
@import "polygons.mapcss";
```

### @{name}

Inserts the value of the macro, in all places where it is used.

```css
// Define color using
@color_ground: #EAE3D3;

// then use it as
canvas
{
    fill-color: @color_ground;
}
```

## Draw parameters

The parameters control how to draw objects on the map.

### Parameter values

#### Width

Line thickness or `width` can be specified in pixels `1px`, points `2pt`, meters `3m` or calculated using the expression `eval( zlinear( 13, 1px,1pt,max(2pt, 4m)). );`. Read more about expressions in [separate section](#expressions).

### Color

Color can be specified in the following formats: `#RGB`, `#RRGGBB`, `#RGGBBAA` or a color constant from [CSS list] (https://www.w3schools.com/colors/colors_names.asp).

#### Text

Any sequence of characters between single or double quotes is considered text.

```css
'string'
"another string"
```

### Draw order parameters
  
#### `layer`

The layer number is needed to separate the different levels on the map.

```css
// for any object with tag 'layer', set it's 'layer' property, to the value of 'layer' tag
*|z9-[layer]
{
    layer: eval(tag(layer));
}
```
  
#### `z-index`

`z-index` sets the order of drawing objects of the same type inside one layer.

```css
area|z10-[natural=wood]
{
    z-index: -3;
    fill-color: @color_wood;
}

area[natural=oceanwater]
{
    z-index: -2;
    fill-color: @color_water;
}
```

### Polygon parameters

#### `fill-color`

Fill color of the polygon

```css
area|z5-[natural=water]
{
    fill-color: @color_water;
}
```

#### `fill-image`

Fill image of the polygon

```css
// fill image of military area desplayed on top of the other objects
area|z11-[landuse=military],
area|z11-[military=danger_area]
{
    z-index: 2;
    fill-image:"forbiddenArea.png";
}
```

#### `color` and `width` for polygon

Polygon border color and border width

```css
area|z15-[building]
{
    z-index: 3;
    width: 1px;
    color: @color_landuse_residential_stroke;
}
```

### Line parameters

#### `color` and `width` for line

Line color and width

```css
line|z13-[natural=tree_row]
{
    width: 3pt;
    color: @color_wood;
    z-index: -10;
}
```

#### `casing-color` and `casing-width`

Line casing color and casing width. Used mostly for roads.

```css
line|z8-[highway=motorway],
line|z11-[highway=motorway_link] {
    color: @color_motorway;
    casing-color: @color_motorway_casing;
    casing-width: 0.5pt;
}
```

#### `dashes`

Indicates the lengths of painted and blank segments. The sum of numbers must be equal to the power of 2 (4, 8, 16, 32, 64, etc.). Each number is the length of the line segment in points.

```css
line|z15-[highway=cycleway] {
    dashes: 2,2,2,2;
    dashes-color: @color_cycleway_dashes;
}
```

#### `dashes-color` and `dashes-width`

Line dashes color and dashes width. Used for trails, paths, stairs and borders.

```css
line|z15-[highway=steps] {
    dashes-color: @color_footway_dashes;
    dashes-width: eval( zlinear( 16, 3pt, 4pt ) );
}
```

#### `linecap`

The shape of the line edges. Possible values: `none`, `square`, `round`.

#### `linejoin`

Line joint form. Possible values `round`, `miter`, `bevel`, `auto`.

### Text params

#### `text`

The text to be written next to a point, in the center of the line or in the center of the polygon.

```css
node,area|z2-8[place=country]
{
    text: eval(locTag('name'));
    // other params skipped
}
```

#### `font-weight`

The thickness of the text or font weight. Possible values: `bolder`, `bold`, `normal`, `light`, `ligther`.

```css
node,area|z9-[place=town],
node,area|z10-[place=village],
node,area|z12-[place=hamlet]
{
    font-weight:light;
    font-size:11;
    font-stroke-width:2px;
    font-stroke-color: @color_label_stroke;
}
```

#### `font-size`

Font size.

#### `font-stroke-width` and `font-stroke-color`

Font stroke width and color.

#### `text-color`

Text color.

```css
node,area|z2-8[place=country]
{
    text: eval(locTag('name'));
    text-color: @color_name_text;
    text-priority: 10;
    // other tags skipped
}
```

#### `text-priority`

When there is a lot of text nearby, the text priority allows you to specify which text to draw first.

#### `text-allow-overlap`

Allows you to allow the display of text with overlapping. Several labels, one on top of the other.

#### `icon-image`

The name of the picture to be shown in the center of the polygon or at a point. At the moment, external images are not supported. You can find the names of available pictures in [Guru Maps style](https://github.com/GalileoApp/MapStyle).

```css
node,area|z17-[_optOn=Culture][amenity=library] {
    icon-image:"library.svgpb";
    icon-scale:0.37;
    icon-tint: @color_icon_tint;
}
```

#### `icon-scale`

The scale of the picture allows you to make the picture bigger or smaller than its original size.

#### `icon-tint`

A tint allows you to repaint the picture in a different color. The colours of the picture are changed in the following way. `#FFF` white remains white, `#CCC` becomes lightened `tint-color`, `#888` becomes identical to the color in `tint-color`, `#444` - darkened `tint-color` and `#000` black remains black. At all intervals, the color will change smoothly between the specified colors.

#### `icon-offset-x` and `icon-offset-y`

You can move the picture relative to the anchor point. By default, image is centered at the point on the map for which the image was shown. `icon-offset-y: 0;` for example, allows you to show the pin on the map with a needle at the point for which it was shown. Values from 0 to 1 are used. Where 0 is the bottom for `icon-offset-y` and the left side for `icon-offset-x` and 1 is the top and right side respectively.

#### `image-allow-overlap`

Enables one-to-one overlay of pictures.

### Details parameters

`details-text` and `details-description` are used to set a name and description for GeoJSON objects. The text set in `details-text` will be displayed as a name, and the text set in `details-description` will be displayed as a description. If `details-text` or `details-description` is not filled, tap on such objects is not processed. Expressions can be used in these parameters.

```css
* {
    details-text: eval(tag('name'));
    details-description: eval(tag('description'));
}
```

### Expressions {#expressions}

Not only filters, but also object parameters may depend on external factors, be calculated by formula or vary depending on the scale.

If the parameter's value should be calculated, it always starts with `eval()` function.

The following functions can be used inside:

#### `min` and `max`

Returns the minimum or maximum value from the parameters. The number of parameters is not limited.

#### `any`

Returns the first non `null` value from the parameters. The number of parameters is not limited.

#### `tag`

Возвращает значение тега, указанного в параметре или `null`, если значения нет.

#### `locTag`

Returns localized tag values depending on the language settings of the user. For example, if the order of languages is English, Russian and Native language. For `locTag(name)` will check `name:en`, `name:ru` and `name`, the first found value will be used. Languages supported by Guru Maps is: `be`, `cs`, `da`, `de`, `en`, `es`, `fr`, `it`, `ja`, `ko`, `nl`, `pl`, `ru`, `sv`, `uk`, `zh`. The languages listed can be checked by `locTag()`. Other languages should be written explicitly with `tag()`.

#### `cond`

The first parameter contains a logical expression, the second will be returned if the expression is true, the third if the expression is false.

```css
// check addr:housenumber
    text: eval( cond( tag('addr:housenumber'),
    // if there is addr:housenumber, then concatenate next condition
        tag('addr:housenumber') . cond( any( locTag('name'), tag('addr:housename') ),
            // if there is name or addr:housename - put them between ()
            ' (' . any( locTag('name'), tag('addr:housename') ) . ')',
            // empty line otherwise
            ''),
    // if there is no housenumber just use any from name or addr:housename
    any( locTag('name'), tag('addr:housename') ) ) );
```

#### `boolean`

Converts the value to Boolean type. If there is no value or it is equal to `0`, `No`, `Off`, `False` case insensitive - the function will return `false`. In other cases `true`.

#### `zlinear`

Smoothly changes the value as the zoom changes. The first parameter is the initial zoom level. Then any number of values for all zoom levels starting from the initial one.

```css
line|z13-[highway=residential]
{
    width: eval( zlinear( 13, 1px, 1pt, max(2pt, 4m) ) );
    color: @color_small_road;
    linecap: round;
}
```

In this example, the road width at 13 zoom level is 1 pixel, at 14 zoom level is 1 point, at 15+ zoom level will be used the greater of 2 points or 4 meters.

#### `metric`

The numeric parameter of this function changes type to meters.

```css
line|z12-[highway=tertiary]
{
    width: eval( zlinear( 12, 1px, 1pt, 1pt, max(3pt, metric(any(tag(lanes),2)*2)) ));
}
```

In this example, the number of lines is multiplied by 2 - the result is considered to be the distance in meters. max(3pt, metric()) will return a larger value, width in meters or in points.

### Expression operators

The following mathematical operators can be used in expressions: `+`, `-`, `*`, `\`, string fusion operator - `.`, comparison operators `<` - less, `>` - more, `==` - exact equality, `~=` - presence of substring in the string.