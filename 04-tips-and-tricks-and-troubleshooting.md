# Tips and Tricks and Troubleshooting

> In this section we will go over some of advanced features as they pertain to specific areas of using an app.

## Custom Map Sources {#customMapSources}

The following examples show how the XML file for OpenStreetMap source may be defined.

### Simple custom map sources {#simpleCustomMapSources}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customMapSource>
<name>OpenStreetMap</name>
<url>http://{$serverpart}.tile.openstreetmap.org/{$z}/{$x}/{$y}.png</url>
<serverParts>a b c</serverParts>
</customMapSource>
```

### Custom multi-layer map sources

Map sources which consist of two or more layers can be defined, similar to single-layer custom map sources. The following example shows how the XML file for OpenSeaMap hybrid source may be defined:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customMapSource>
<name>OpenSeaMap</name>
<minZoom>0</minZoom>
<maxZoom>18</maxZoom>
<layers>
<layer>
<url>http://{$serverpart}.tile.openstreetmap.org/{$z}/{$x}/{$y}.png</url>
<serverParts>a b c</serverParts>
</layer>
<layer>
<minZoom>9</minZoom>
<maxZoom>18</maxZoom>
<url>http://tiles.openseamap.org/seamark/{$z}/{$x}/{$y}.png</url>
</layer>
</layers>
</customMapSource>
```

The most important tags of this definition are described below:

`<name>` – the name of the map source,
	
`<url>` – the path for the tiles of the map source with the specific placeholders in curly brackets:
							
{$z} – the zoom level,
{$x} – the X tile coordinate,
{$y} – the Y tile coordinate,
{$invX} – the inverted X tile coordinate,
{$invY} – the inverted Y tile coordinate,
{$serverpart} – (optional) in case of multiple servers for the map source.
`<serverParts>` – a space-separated list of parts that replace the {$serverpart} in `<url>` tag.
`<retina>` – tag for defining the size of Retina map tiles:
							
`<retina>1</retina>` – for 512х512 px (e.g. Google Maps HD),
`<retina>2</retina>` – for 256х256 px (e.g. CloudMade HD).


#### How to add

There are several ways to add custom online map source to the app:

1. Place the XML file in the app shared folder in iTunes.
2. Open the XML file attached in Email on your device using the "Open in Galileo" option.
3. Open the XML file from Dropbox on your device using the "Open in.." option.
	
As a result, the new map source will appear in Map Source list.

#### Troubleshooting

Sometimes you can see empty map areas (tiles), with the following warning messages on the map:

* "Tile loading error. Please check your Internet connection" – this appears when tiles are missing in the cache and app can't download them. Enable an Internet connection or go to ’online’ mode to load the missing tiles.
* "Tile loading error. Wrong response from the server" – the online server is not responding. Try to navigate to this area later to reload any missing tiles.

## Offline Maps Import {#offlineMapsImport}

Feature, available as an in-app purchase, allows you to import previously created custom offline maps in **.sqlitedb** or **.mbtiles** format.

#### Creating an offline map

The main idea is to create an offline map for the desired area in advance with one of the following tools on your computer using one of the following tools:

* [Mobile Atlas Creator](http://mobac.sourceforge.net/) (known also as MOBAC)
* [TileMill](https://tilemill-project.github.io/tilemill/)
* [SAS.Planet](http://sasgis.ru/sasplaneta/)

_Mobile Atlas Creator (MOBAC)_ – is free software that allows you to download maps from numerous map sources, and save them in the .sqlitedb format used by Galileo Offline Maps. This tool is compatible with Windows, Mac OS X and Linux.

Reference: to learn how to create offline maps in **.sqlitedb** format, please refer to the [MOBAC manual](http://mobac.sourceforge.net/quickstart/).
				
_TileMill (by MapBox)_ – is a desktop application for cartographers to quickly and easily design and create stunning offline maps in the .mbtiles format supported by Galileo Offline Maps. It is completely compatible with Mac OS X, Windows and Ubuntu.

Reference: to learn how to create offline maps in **.mbtiles** format, please refer to the [TileMill manual](https://tilemill-project.github.io/tilemill/docs/manual/).
					
SAS.Planet – is a program designed for viewing and downloading high-resolution satellite imagery and conventional maps in .sqlitedb format.
Reference: to learn how to create offline maps in **.sqlitedb** format, please refer to the [SAS.Planet manual](http://www.sasgis.org/wikisasiya/doku.php).

#### Importing offline maps

Once you have created an offline map, you should upload it to your device. There are two ways to import an offline map into your device: via iTunes or cloud service.
						
**Importing using iTunes**

Connect your device to your computer and perform these steps:
1. Launch the iTunes application and select your device.
2. Open File Sharing in the left sidebar and select Galileo in the Apps list.
3. Add the file with the offline map into the Galileo Documents.

![](/assets/Screen Shot 2018-01-05 at 11.31.58 AM.png)

**Importing from the Files app**

In addition to iTunes sync, there is another handy way to upload your offline maps using the iOS Files app:
1. Put the file with the created offline map, in .sqlitedb/.mbtiles format, in the Files/iCloud drive on your computer.
2. Open the Files app on your iOS device and wait until the file you placed there is synchronized automatically between the devices.
3. Select the offline map you would like to import and tap the  icon, then select "Copy to Galileo" option to initiate the import process.


#### Using offline maps

Go to Map Source in app settings and select the imported map name in the list and back to the map view. If you are not over the area with offline map, tap the green arrow indicating the direction to the offline map. Zoom in to see a detailed view of your offline map.

## Getting Exported Files

In order to access the exported collection, bookmark or GPS track using File Sharing:
						
1. Launch the iTunes application and select your device.
2. Open File Sharing in the left sidebar and select Galileo in the Apps list to view a list of the files exported within the app on your iOS device.
3. Select the file you want to copy to your computer from the Documents list and click the "Save to.." button.
4. Locate the folder on your computer to which you want to copy selected file and click the Open button. The selected files will be copied to your computer immediately.

					
#### Hidden Settings


Hidden settings are tweaks which have been developed to adapt the behaviour and appearance of the application to your specific way of use. To access them, just go to the system Settings, scroll down and find the Galileo in the app list.
The following additional settings are available for Galileo:

* **Allow overzoom on map**. If enabled, the map can be zoomed closer than the scale allows.
* **Allow map rotation**. If enabled, the app recognizes the map rotation using two fingers gesture.
* **Cluster bookmarks**. If enabled, the app groups bookmarks which are close to each other on the map.
* **GPS Activity Type**. Turn set GPS activity type up depending on your needs. To read more about the options follow this link: Activity Types.	
* **Write GPS log**. Turn on to log all received GPS coordinates in order to facilitate debugging during the development process.

