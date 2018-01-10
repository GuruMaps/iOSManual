 # Settings

> Galileo Offline Maps is available in a ready-to-use state and app settings should be considered as optional and more advanced way of using the app. Settings lets you configure app options, purchase additional features and manage geo data representation.

## Map Sources {#MapSources}

To switch to another map to display, select **Map Source** menu in app settings. There are two types of maps you can use within the app: offline and online maps.

#### Offline maps
						
Vector map source is set by default. Once you’ve downloaded it (**internet connection required**), it will be available offline.
Vector maps are detailed, smooth, fast and provide high quality image rendered in real time on the device. It takes up less storage space than raster maps.

**Note**: you can also use your own maps in .sqlitedb and .mbtiles formats, previously created on computer and then imported into your device. Such maps can be viewed offline even when your mobile device has no internet connection.

	 						 						
#### Online maps
						
There is a list of built-in raster map sources available online:
				 						
* HikeBikeMap
* Humanitarian OSM
* OpenBusMap
* OpenCycleMap
* OpenStreetMap
* Stamen – Terrain (USA only)
* Stamen – Toner
						 						
Caching is always enabled – the app saves all recently viewed map images in your cache and keeps them available for offline usage. To save maps, navigate to the area you are going to visit and zoom-in while you have access to the Internet.
						 						
**Note**: map download speed can vary while using an online sources, and depends on the speed of your Internet connection and the speed of the server from where the map is downloaded.

In addition to built-in online raster maps, Galileo Offline Maps also supports custom online maps. You can add any map source you like using a special XML file that contains description of map provider.

## Network Mode {#NetworkMode}

This setting lets you configure how the app is allowed to connect to the network:

![](/assets/network_mode.png)

* **WiFi+3G** is set by default and uses a combination of two networks: if a Wi-Fi connection to the Internet is not available, the app connects over to the cellular data network, if available.
* **WiFi** in case you want the app to load data only over the Wi-Fi network, if available.
* **Offline** allows to use the app completely offline and not to worry about roaming charges. Even if you have full internet connection, the app will act like it is ‘off’.


## Vector Maps Settings {#VectorMapsSettings}

This section describes the vector maps related settings within the app.

### Download Maps

Vector maps are available and free for download within the app:
 
![](/assets/download_map_3.png)

To **download a map of the selected country** tap the ![](/assets/icon_download_map.png) button next to the country name in Available Maps list.
To **pause a download**, tap the cell with the country name tap it again to resume a download,
To **go to downloaded map** tap the  button,
to **remove a map** swipe your finger across the country name from right to left, then tap the Delete button, or use the Edit button.

As OpenStreetMap data is constantly updated by thousands of volunteers around the world, map updates are available from time to time within the app. In Galileo app all vector map updates are free and distributed automatically. If there is an update for downloaded map, you will see Update button near the downloaded map name.

To **update all your downloaded maps** tap the “Update All” button.


### Font and Language {#FontAndLanguage}

#### Font size 

You can configure Galileo to display all text on a vector map at a comfortable font size. To increase, decrease, or change the default font size, go to app Settings > Font and Languages:

![](/assets/font_and_language.png)

#### Preferred language order

In some regions objects on the map in addition to local names have names in other languages. Map will show the names on the first language in this list if exists. It may be useful for multilingual countries, such as Belgium where Dutch, French and German share official language status.


### Map Features {#mapFeatures}

In addition to the basic appearance settings, you can select the objects you wish to display on the vector map. Select only the objects that you want to display to keep the map tidy and uncluttered:

* Restaurants, cafes, fast foods
* Bars, pubs, clubs
* Beauty salons, hairdressers
* Entertainment, arts and culture
* Monuments, places of worship
* Tourist attractions
* Hotels, hostels, campsites
* Banks, ATMs, currency exchanges
* Parking, gas and service stations
* Hospitals, clinics, pharmacy
* Shopping malls, supermarkets
* Police, post offices, embassies
* Universities, colleges, schools
* Public transport stops
* Train and metro stations
* Building names and numbers


## Appearance Settings {#appearance}

The following group of settings is used to configure how the main map looks: 

![](/assets/settings_appearance.png) 

### Show Trip Computer {#showTripComputer}
 
To hide trip monitor panel from the map view, turn off this option.

### Show Coordinates {#showCoordinates}

To enable the real-time display of coordinates on the map, turn on this option. If enabled, crosshairs will appear in the center of the map and coordinates for the crosshairs will be beneath the map scale bar in selected format as well as the current zoom level:

![](/assets/show_coordinates.png)


### Show Zoom Buttons {#showZoomButtons}

To make visible zoom control buttons on the map, turn this option on. If enabled, plus and minus zoom buttons will appear on the map:

![](/assets/zoom_buttons.png)

### Show Bookmark Name

To make visible bookmark name on the map, turn this option on. If enabled, bookmark will change its view and the name of bookmark will appear:

![](/assets/bookmark_name_2.png)

### Screen Auto-Lock {#screenAutoLock}

The screen of your device will be turned off automatically after a specified period of time to save on power.
Turn this option off if you want your device not to lock the screen while using the Galileo app.

### New Buttons Layout 

Turn this option on to get all the major interface options aligned to the right to be accessed quickly with one finger:

![](/assets/new_buttons_layout.png)


### Default Styles {#defaultStyles}

To set a color for GPS tracks and category for bookmarks used by default, go to app Settings &gt; Default Styles.  

#### Default track style

Selected style is a default line style for the newly recorded and imported GPS tracks:

_1. By color:_

![](/assets/track_appearance_1.png)

_2. By speed:_

![](/assets/track_appearance_2.png)

_3. By altitude:_

![](/assets/track_appearance_3.png)


#### Default bookmark category

Selected category is a default icon for newly created and imported bookmarks:


## Advanced Settings {#advanced}

### Sync {#sync}

Galileo Offline Maps allows you to synchronize all your data to make your collections visible and available through all your iOS devices using your Facebook or iCloud account.
App uses Facebook/iCloud login only for authentication, this does not let the Galileo post or share your data.
To enable synchronization feature, go to the app Settings > Sync and select the appropriate way to authenticate.
**Note**: use the same login on all your devices to keep the data synchronized.

![](/assets/sync.png)


### Navigation {#navigation}

The default language of voice instructions you hear while navigating a route depends on the language your device is set to use. 
To change the language, select one from the Voice Instructions list:

![](/assets/settings_navigation.png)

### Data Backup {#dataBackup}

Backing up data is a great way to minimize accidental data loss and restore the most important geodata on your device.

#### Create backup

Tap Back Up My Collections button on Settings &gt; Data Backup screen to backup the collections within the app.  
**Note**: created backup only includes data from My Collections \(bookmarks and GPS tracks\), and it doesn't include downloaded and cached tiles.  
When the backup finished successfully, you'll see the name of the device along with the date and time the backup was created:

![](/assets/data_backup.png)

#### Save backup

Backups are stored on your device and will be removed automatically when the app is removed. To prevent data loss, we recommend to save your backups regularly.

The best way to keep your backups available across all your iOS devices is to use the Files app. There you can set up your other cloud services (Box, Dropbox, OneDrive, Adobe Creative Cloud, Google Drive, etc) to access them in the Files app too.

![](/assets/data_backup_share.png)

#### Restore from a backup

Tap the backup you created earlier in the list on Data Backup screen to restore from, or select .gbackup file from the Files app or from other cloud service.

![](/assets/data_backup_restore.png)

**Note**: restoring from backup will remove all current bookmarks and GPS tracks in My Collections.

### Cache info {#cacheInfo}

#### Map Refresh

To set how often to refresh cached map tiles, go to Settings &gt; Cache Info. All tiles older than selected time will be downloaded while browsing online.

#### Cache Info

All loaded map tiles will be automatically saved to your device's storage and can be managed in Settings &gt; Cache Info, so you can delete the tiles you no longer need if you want to free up storage space:

![](/assets/cache_info.png)


### GPS Filtering {#gpsFiltering}

Galileo Offline Maps app supports GPS data filtering in Settings &gt; GPS Filtering.  

![](/assets/gps_filtering.png)

#### Accuracy Threshold

Filter by the minimum accuracy at which the new points will be accepted. New points will be added to GPS track while recording if the accuracy is lower than selected (recommended value is 150 m).

**Example**: You are recording your GPS track while walking around your neighbourhood and you have entered a supermarket. Tall walls, roofs and other obstructions can block the signal from GPS satellites and the device cannot determine your location accurately enough. You may enable the accuracy filter to set the required accuracy and ignore inaccurate GPS data. If the received signal has lower than the required accuracy, that point will not be recorded in the track.

#### Distance Threshold

Filter by the minimum distance travelled before a new point will be recorded. New points will be added to GPS track while recording if the distance between them is greater than selected (recommended value is 5 m).

**Example**: You are recording your GPS track while jogging, then you meet a friend and stop to talk to him. As the GPS sends location coordinates every second, too many points will be recorded on the same spot while you are talking, and the recorded track will take up more space. You may enable the distance filter to ignore GPS points if they are too close to each other. New points will start recording as you exceed the distance selected in the filter.


### Units Format {#unitsFormat}

To set the units system and coordinates format you would like to use within the Galileo Offline Maps, go to Settings &gt; Units Format. 
 
#### Units system

The following units of measure for distance and speed are available to select from:

* **km** — for kilometres & km/h,
* **mi** — for miles & mph,
* **NM** — for nautical miles & kts.

#### Coordinates format

In Galileo Offline Maps you can choose to represent your coordinates in any way you like. The coordinate format you select will be used to display all coordinates within the app. Here is an example of different coordinate formats for New York city follows:

* +40.730598, -73.986580 \(DDD.DDDDD\)
* 40°43'50.1" N, 73°59'11.6" W \(DDD°MM' SS.S"\)
* 40°43.835' N, 73°59.194' W \(DDD°MM.MMM’\)
* 40.73060° N, 73.98658° W \(DDD.DDDDD°\)
* 18TWL 85577 09345 \(MGRS\)

## Help {#Help}

### Contact Us

If you have faced a problem - here you can contact Support via email (**internet connection required**).

