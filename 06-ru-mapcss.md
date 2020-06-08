# MapCSS

Файл стиля MapCSS состоит из правил, которые применяются к каждому объекту сверху-вниз.

Например стиль:

```css
node[natural=tree] {
    icon-image: tree.svgpb;
}
```

отобразит картинку `tree.svgpb` для точек у которых тег `natural` имеет значение `tree`.

Каждое правило в стиле состоит из двух частей. Фильтра `node[natural=tree]` и параметров прорисовки `icon-image: tree.svgpb;`. Запрос выбирает к каким объектам надо применить параметры.

Эта документация описывает диалект MapCSS используемый в приложении Guru Maps. Часть параметров прорисовки не была реализована, добавлены макросы подстановки, используется другой список функций для вычисляемых операций. Стиль, используемый в Guru Maps, вы можете найти в [публичном репозитории](https://github.com/GalileoApp/MapStyle).

## Фильтры

Рассмотрим сложный фильтр:

```css
node,area|z15-[railway=station]
```

Он состоит из:

1. фильтра по типу `node,area`. Он может быть `node` для точек, `line` для линий, `area` для полигонов. Если надо указать несколько типов они разделяются запятой. Так же можно использовать `*`, если тип не важен.
2. фильтра масштаба `z15-`. Он указывает для каких масштабов должно срабатывать правило. Может быть только минимальным масштабом `z8-`, или интервалом `z3-9`. В таком случае правило будет применено для на масштабах с 3-го по 8 включительно.
3. фильтра параметров `[natural=tree]`. Такой фильтр оставит только объекты у которых тег `natural` имеет значение `tree`. Чтобы оставить только объекты у которых есть любое значение тега `natural` следует использовать фильтр `[natural]`. Чтобы оставить объекты у которых нет значения тега `natural` используется фильтр `[!natural]`

## Макросы подстановки

### @import

Вставляет содержимое указанного файла.

```css
@import "polygons.mapcss";
```

### @{name}

Вставляет значение макроса, во все места где он использован.

```css
// Define color using
@color_ground: #EAE3D3;

// then use it as
canvas
{
    fill-color: @color_ground;
}
```

## Параметры прорисовки

Параметры управляют отображением объектов на карте. Guru Maps поддерживает следующий набор параметров:

### Значения параметров

#### Толщина

Толщина линий может быть задана в пикселях `1px`, поинтах `2pt`, метрах `3m` или вычислена с помощью выражения `eval( zlinear( 13, 1px,1pt,max(2pt, 4m) ) );`. О выражениях, читайте в отдельной секции.

#### Цвет

Цвет может быть задан следующими форматами: `#RGB`, `#RRGGBB`, `#RRGGBBAA` или константой цвета из [списка CSS](https://www.w3schools.com/colors/colors_names.asp).

#### Текст

Текстом считается любая последовательность символов между одиночными или двойными кавычками.

```css
'string'
"another string"
```

### Параметры порядка прорисовки
  
#### `layer`

Номер слоя нужен для разделения разных уровней на карте.

```css
// for any object with tag 'layer', set it's 'layer' property, to the value of 'layer' tag
*|z9-[layer]
{
    layer: eval(tag(layer));
}
```
  
#### `z-index`

`z-index` устанавливает порядок прорисовки объектов одного типа внутри одного слоя.

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

### Параметры полигонов

#### `fill-color`

Цвет заливки полигона

```css
area|z5-[natural=water]
{
    fill-color: @color_water;
}
```

#### `fill-image`

Картинка заливки

```css
// fill image of military area desplayed on top of the other objects
area|z11-[landuse=military],
area|z11-[military=danger_area]
{
    z-index: 2;
    fill-image:"forbiddenArea.png";
}
```

#### `color` и `width` для полигона

Цвет и толщина обводки полигона

```css
area|z15-[building]
{
    z-index: 3;
    width: 1px;
    color: @color_landuse_residential_stroke;
}
```

### Параметры линии

#### `color` и `width` для линии

Цвет и толщина линии

```css
line|z13-[natural=tree_row]
{
    width: 3pt;
    color: @color_wood;
    z-index: -10;
}
```

#### `casing-color` и `casing-width`

Цвет и толщина обводки линии

```css
line|z8-[highway=motorway],
line|z11-[highway=motorway_link] {
    color: @color_motorway;
    casing-color: @color_motorway_casing;
    casing-width: 0.5pt;
}
```

#### `dashes`

Указывает длины закрашенных и пустых участков. Сумма цифр должна быть равна степени двойки. Величина цифры - это длинна участка линии в поинтах.

```css
line|z15-[highway=cycleway] {
    dashes: 2,2,2,2;
    dashes-color: @color_cycleway_dashes;
}
```

#### `dashes-color` и `dashes-width`

Цвет и толщина пунктира

```css
line|z15-[highway=steps] {
    dashes-color: @color_footway_dashes;
    dashes-width: eval( zlinear( 16, 3pt, 4pt ) );
}
```

#### `linecap`

Форма краев линий. Возможные значения: `none`, `square`, `round`.

#### `linejoin`

Форма соединения линий. Возможные значения `round`, `miter`, `bevel`, `auto`.

### Text params

#### `text`

Текст, который будет написан рядом с точкой, в центре линии или в центре полигона.

```css
node,area|z2-8[place=country]
{
    text: eval(locTag('name'));
    // other params skipped
}
```

#### `font-weight`

Толщина текста. Возможные значения: `bolder`, `bold`, `normal`, `light`, `ligther`.

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

Размер шрифта.

#### `font-stroke-width` and `font-stroke-color`

Толщина и цвет обводки текста.

#### `text-color`

Цвет текста

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

Когда много текста находится рядом, приоритет текста позволяет указать какой текст надо рисовать в первую очередь.

#### `text-allow-overlap`

Позволяет разрешить отображение текста с наложением. Несколько надписей одна поверх другой.

#### `icon-image`

Имя картинки которую надо показать в центре полигона или в точке. В настоящий момент внешние картинки не поддерживаются. Имена доступных картинок вы можете найти в [стиле Guru Maps](https://github.com/GalileoApp/MapStyle).

```css
node,area|z17-[_optOn=Culture][amenity=library] {
    icon-image:"library.svgpb";
    icon-scale:0.37;
    icon-tint: @color_icon_tint;
}
```

#### `icon-scale`

Масштаб картинки позволяет сделать картинку больше или меньше ее изначального размера.

#### `icon-tint`

Тинт позволяет перекрасить картинку в другой цвет. Цвета картинки меняются следующим образом. `#FFF` белый цвет остается белым, `#ССС` - станет осветленным `tint-color`, `#888` - станет идентичным цвету в `tint-color`, `#444` - затемненный `tint-color` и `#000` черный останется черным. На всех промежутках цвет будет плавно меняться между указанными цветами.

#### `icon-offset-x` и `icon-offset-y`

Позволяет сдвинуть картинку относительно точки привязки. По умолчанию центр картинки совпадает с точкой на карте, для которой картинка была показана. `icon-offset-y: 0;` позволяет показать пин на карте иголкой в точке, для которой он показан. Используются значения от 0 до 1. Где 0 это низ для `icon-offset-y` и левая сторона для `icon-offset-x`, а 1 - это верх и правая сторона соответственно.

#### `image-allow-overlap`

Разрешает наложение картинок одна на одну.

### Параметры описания

`details-text` и `details-description` используются для установки имени и описания у GeoJSON объектов. Текст установленный в `details-text` будет показн как имя, а текст установленный в `details-description` будет показан как описание. Если `details-text` или `details-description` не заполнен, то нажатие по таким объектам не обрабатывается. В этих параметрых можно использовать выражения.

```css
* {
    details-text: eval(tag('name'));
    details-description: eval(tag('description'));
}
```

### Выражения

Не только фильтры, но и параметры объекта могут зависеть от внешних факторов, вычисляться по формуле или изменяться в зависимости от масштаба.

Если значение параметра должно быть вычислено, оно всегда начинается с функции `eval()`.

Внутри выражения могут быть использованы следующие функции:

#### `min` и `max`

Возвращает минимальное или максимальное значение из параметров. Число параметров не ограничено.

#### `any`

Возвращает первое не `null` значение из параметров. Число параметров не ограничено.

#### `tag`

Возвращает значение тега, указанного в параметре или `null`, если значения нет.

#### `locTag`

Возвращает локализованное значения тега в зависимости от языковых настроек пользователя. Например если порядок порядок языков английский, русский, язык региона. Для `locTag(name)` будут проверены значения тегов `name:en`, `name:ru`, `name` и использованно первое найденное значение. Поддерживаемые языки: `be`, `cs`, `da`, `de`, `en`, `es`, `fr`, `it`, `ja`, `ko`, `nl`, `pl`, `ru`, `sv`, `uk`, `zh`. Перечисленные языки могут быть использованы в locTag. Другие языки должны быть написаны явно с помощью `tag()`.

#### `cond`

Первый параметр содержит логическое выражение, второй будет возвращен, если выражение истинно, третий, если выражение ложно.

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

Переводит значение в булевый тип. Если нет значения или оно равно `0`, `No`, `Off`, `False` без учета регистра - функция вернет `false`. В остальных случаях `true`.

#### `zlinear`

Плавно меняет значение по мере изменения масштаба. Первый параметр - начальный уровень масштаба. Далее любое число значений для всех масштабов начиная с начального.

```css
line|z13-[highway=residential]
{
    width: eval( zlinear( 13, 1px, 1pt, max(2pt, 4m) ) );
    color: @color_small_road;
    linecap: round;
}
```

В этом примере толщина дороги на 13 зуме 1 пиксель, на 14 зуме 1 поинт, на 15+ будет использована большая из толщин 2 поинта или 4 метра.

#### `metric`

Цифровое значение переданное в эту функцию считается в метрах.

```css
line|z12-[highway=tertiary]
{
    width: eval( zlinear( 12, 1px, 1pt, 1pt, max(3pt, metric(any(tag(lanes),2)*2)) ));
}
```

В этом примере число полос умножается на 2 - результат умножения считается расстоянием в метрах. max(3pt, metric()) вернет большее значение, ширину в метрах или в поинтах.

### Операторы выражений

В выражениях могут быть использованы следующие математические операторы: `+`, `-`, `*`, `\`, оператор слияния строк - `.`, операторы сравнения `<` - меньше,`>` - больше, `==` - точное равенство, `~=` - наличие подстроки в строке.
