# Settings

> Galileo Offline Maps is available in a ready-to-use state and app settings should be considered as an optional and more advanced way of using the App. Settings let you configure app options, purchase additional features and manage routing geo data representation.

## Map Source {#MapSources}

To switch to another map to display, select **Map Source** menu in app settings. There are two types of maps you can use within the app: offline and online maps.

#### Offline maps

Vector map source is set by default. Once you’ve downloaded the map \(**Internet connection required**\), it will be available offline.  
Vector maps are detailed, smooth, fast and provide high-quality image rendered in real time on the device. It takes up less storage space than raster maps.

**Note**: you can also use your own maps in .sqlitedb and .mbtiles formats, previously created on a computer and then imported into your device. Such maps can be viewed offline even when your mobile device has no internet connection. However, any personal raster/tile maps will use considerably more space than vector maps you may install.

Read also: [Offline Maps Import](/04-tips-and-tricks-and-troubleshooting.md).

#### Online maps

There is a list of built-in raster map sources available online:

* HikeBikeMap
* Humanitarian OSM
* OpenBusMap
* OpenCycleMap
* OpenStreetMap
* Stamen – Terrain \(USA only\)
* Stamen – Toner

Caching is always enabled – the app saves all recently viewed map images in your cache and keeps them available for offline usage. To save maps, navigate to the area you are going to visit and zoom-in to the lowest viewable level of detail while you have access to the Internet. The level of saved detail will reflect the zoom level you viewed.

Read also: [Cache Info](/03-settings.md#cacheInfo).

**Note**: map download speed can vary while using online sources, and depends on the speed of your Internet connection and the speed of the server from where the map is downloaded.

In addition to built-in online raster maps, Galileo Offline Maps also supports custom online maps. You can add any source of maps you like using a special XML file that contains formatted description from the map provider.

Read also: [Custom Map Sources](/04-tips-and-tricks-and-troubleshooting.md#customMapSources).


## Vector Maps Settings {#VectorMapsSettings}

### Download Maps

Free vector maps by country are available for download within the App:

<img src="/assets/download_map_3.png" width="375" height="667" />

To **download the map of the selected country**, tap the ![](/assets/icon_download_map.png) button next to the country name in _Available Maps_ list.  

To **pause a download**, tap the cell with the country name tap it again to resume a download.  

To **go to the downloaded map**, tap the ![](/assets/icon_show_on_map.png) button.  

To **remove the map,** swipe your finger across the country name from right to left, then tap the **Delete** button, or use the **Edit** button.

As OpenStreetMap data is constantly updated by thousands of volunteers around the world, map updates are available from time to time within the app. In the Galileo app all vector map updates are free and distributed automatically. If there is an update for a previously downloaded map, you will see the **Update** button beside the map.

To **update all your downloaded maps**, tap the **Update All** button.

### Font and Language {#FontAndLanguage}

#### Font size

You can configure Galileo to display all text on a vector map at various font size. To increase, decrease, or change the default font size, go to app Settings &gt; Font and Languages:

<img src="/assets/font_and_language.png" width="375" height="515" />

#### Preferred language order

In some regions, objects on the map in addition to local names have names in other languages. The map will show the names of the user designated the first language in this list if it has been defined by the user. This feature may be useful for multilingual countries, such as Belgium where Dutch, French and German share official language status.

Tap **Edit** button on the top right of the screen, to rearrange or delete languages from the list.

### Map Features \(**Points of Interest\)** {#mapFeatures}

In addition to the basic appearance settings, you can select the **POIs** you wish to display on the vector map. Select only the **POIs** that you want to display to keep the map tidy and uncluttered:

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

<img src="/assets/settings_appearance.png" width="375" height="311" />

### Show Trip Computer {#showTripComputer}

To hide trip computer panel from the map view, turn off this option.

Read also: [Trip Computer](01-launching-the-application.md#tripComputer)

### Show Coordinates {#showCoordinates}

To enable the real-time display of coordinates on the map, turn this option on. If enabled, “crosshairs” will appear in the map’s center with coordinates and zoom level in the selected format.

<img src="/assets/show_coordinates.png" width="270" height="42" />

### Show Zoom Buttons {#showZoomButtons}

To make zoom control buttons display on the map, turn this option on. It will appear with plus and minus zoom buttons.

<img src="/assets/zoom_buttons.png" width="59" height="122" />


### Show Bookmark Name

To display a bookmark name on the map, turn this option on. The bookmark view will change and the name of the bookmark will appear. The bookmark name can be changed to your preference:

<img src="/assets/bookmark_name_2.png" width="375" height="189" />

### Screen Auto-Lock {#screenAutoLock}

The device screen will be turned off automatically after a specified period of time to save power. Turn this option off If you don’t want the screen to lock while using the Galileo.

### New Buttons Layout

Turn this option on to display the major application functions. The functions will be aligned to the right of the screen for single finger selection.

<img src="/assets/new_buttons_layout.png" width="375" height="424" />

### Default Settings {#defaultSyles}

<img src="/assets/default_settings.png" width="375" height="377" />


#### Default track style

Selected style is a default line style for the newly recorded and imported GPS tracks (solid color/speed gradient/altitude gradient).

#### Show Direction arrows

Enables/disables display of arrows on the track:

<img src="/assets/direction_arrows_1.png" width="375" height="311" />

<img src="/assets/direction_arrows_2.png" width="375" height="311" />


#### GPS filtering {#GpsFiltering}

<img src="/assets/gps_filtering.png" width="375" height="138" />

Filters will be applied for new and imported tracks.

#### Accuracy Threshold

Filter by the minimum accuracy of the received points. Points that are on the outside of the filter value will not be displayed in the track.

#### Distance Threshold

Filter by the minimum distance between points of a recorded track. Points that are closer than the distance specified in the filter will not be displayed in the track.

Read more: [Track Details](02-features.md#TrackDetails)


#### Default bookmark category

The category you select will become the default icon for newly created and imported bookmarks:

<img src="/assets/default_bookmark.png" width="375" height="474" />


## Advanced Settings {#advanced}

### Sync {#sync}

Galileo Offline Maps allows you to synchronize all your data to make your collections visible and available through all your iOS devices using your Facebook or iCloud account.

Galileo Offline Maps allows you to synchronize all your geo data collections available throughout all of your iOS devices. This is accomplished using your Facebook or iCloud account. App uses Facebook/iCloud login only can be done, this does not let the Galileo post or share your data.

To enable the synchronization feature, go to the app Settings &gt; Sync and select the desired synchronizing option. Use the same login on all your devices to keep the data synchronized.

**Tip**: synchronization is a beta feature, so we recommend you backup your collections in advance to avoid unexpected data loss.

<img src="/assets/sync.png" width="375" height="297" />

### Navigation {#navigation}

#### Navigation Mode

Select the mode in which the route will be built.

* Online - internet connection required to build a route:

<img src="/assets/settings_navigation_1.png" width="375" height="297" />

* Online First - if there's no internet connection, the rout will be build using an offline navigation data (**downloaded navigation data required**):

<img src="/assets/settings_navigation_3.png" width="375" height="297" />

* Offline -  no internet connection required to build a route (**downloaded navigation data required**):

<img src="/assets/settings_navigation_2.png" width="375" height="297" />


#### Voice Instructions

The default language for voice instructions you hear while navigating a route depends on the language your device is set to use.  
To change the language, select one from the Voice Instructions list:

**Note**: as the App uses text-to-speech \(TTS\) engine instead of pre-recorded audio, correct pronunciation depends on the TTS engine.

**Tip**: If you connect your iOS device to the Bluetooth-capable stereo system in a car, you will hear voice instructions over your car speakers.

### Data Backup {#dataBackup}

Backing up data is a great way to minimize accidental data loss and restore the most important geodata on your iOS device.

#### Create backup

Tap **Back Up My Collections** button on Settings &gt; Data Backup screen to backup the collections within the App.  
When the backup finished successfully, you'll see the name of the device along with the date and time the backup was created:

<img src="/assets/data_backup.png" width="359" height="306" />

**Note**: Created backup only includes data from My Collections \(bookmarks and GPS tracks\), and it doesn't include downloaded and cached tiles.

#### Save backup

Backups are stored on your device and will be removed automatically when the App is removed. To prevent data loss, we recommend that you backup regularly.

The best way to keep your backups available across all your iOS devices is to use the Files App. Within the Files App you can set up your other cloud services as well \(Box, Dropbox, OneDrive, Adobe Creative Cloud, Google Drive, etc\).

To save the backup, tap the ![](/assets/icon_share.png) icon, then select Save to Files option.

Read also: [**Use the Files App on your iPhone, iPad, and iPod touch**](https://support.apple.com/en-us/HT206481).

<img src="/assets/data_backup_share.png" width="360" height="640" />

#### Restore from a backup

Tap the backup you created earlier in the list on the Data Backup screen to restore, or select .gbackup file from the Files app or from other cloud service \(e.g. in Dropbox App\), then tap the ![](/assets/icon_export.png) icon and select **Copy to Galileo** option.

<img src="/assets/data_backup_restore.png" width="360" height="640" />

**Note**: Restoring from backup will remove all current bookmarks and GPS tracks in My Collections.

### Cache info {#cacheInfo}

#### Map Refresh

To set how often to refresh cached map tiles for online maps, go to Settings &gt; Cache Info. All tiles older than selected time will be downloaded while browsing online.

**Note**: The map refresh setting only applies to raster maps and not the vector maps.

#### Cache Info

All loaded map tiles will be automatically saved to your device's storage and can be managed in Settings &gt; Cache Info, so you can delete the tiles you no longer need if you want to free up storage space.

<img src="/assets/cache_info.png" width="375" height="422" />

### Units Format {#unitsFormat}

To set the units system and coordinates format you would like to use with Galileo Offline Maps, go to Settings &gt; Units Format.

#### Units system

The following units of measure for distance and speed are available to select from:

* **km** — for kilometres & km/h,
* **mi** — for miles & mph,
* **NM** — for nautical miles & kts.

#### Coordinates format

In Galileo Offline Maps you can choose to represent your coordinates in various formats. The coordinate format you select will be used to display all coordinates within the App. Here is an example of different coordinate formats for New York city follows:

* +40.730598, -73.986580 \(DDD.DDDDD\)
* 40°43'50.1" N, 73°59'11.6" W \(DDD°MM' SS.S"\)
* 40°43.835' N, 73°59.194' W \(DDD°MM.MMM’\)
* 40.73060° N, 73.98658° W \(DDD.DDDDD°\)
* 18TWL 85577 09345 \(MGRS\)

## Help {#Help}

### Contact Us

Feel free to ask for further assistance or to report any problems you find at info@galileo-app.com or choose the Contact Support option directly within the app settings \(**Internet connection required**\).

