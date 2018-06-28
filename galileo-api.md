Galileo supports an API that enables developers to open the Galileo app or web page through an external URL. The URL can be accessed from within another mobile application or a mobile web page.

The base URL to use Waze Deep Links is:

`https://galileo-app.com/map`

The Galileo application can then locate an address, mark an address on the map, or start a navigation session to an address or destination, depending on which parameters you pass to this URL.

* Start navigation
* Perform search
* Show bookmark on some location

##Start navigation {#navigation}

Example: `https://galileo-app.com/map?a=nav&lat=53.9&lon=27.4[&type=bike]`

| param  | value                 | description            |
|--------|-----------------------|------------------------|
| a      | nav                   | Action is navigation   |
| lat    | from -90.0 to 90.0    | Destination latitude   |
| lon    | from -180.0 to 180.0  | Destination longitude  |
| type*  | car, bike, walk       | Costing function. Default value is 'car' |

*Optional params

Example: `https://galileo-app.com/map?a=nav&lat=1.234&lon=1.234`

##Perform search {#search}

| param  | value                 | description            |
|--------|-----------------------|------------------------|
| a      | search                | Action is search       |
| q      | query text            | It could be object name, coordinates or address |
| lat*   | latitude | Location where search should be performed. Typically it's user location.
| lon*   | longitude | 

Example: `https://galileo-app.com/map?a=search&q=Минск`

##Show pin {#bookmark}

| param  | value                 | description            |
|--------|-----------------------|------------------------|
| a      | pin                   | Action is pin          |
| lat    | from -90 to 90        | pin latitude  |
| lon    | from -180 to 180      | pin longitude |  
| zoom*  | 3 - 22 | Map zoom. Default value is 15 |
| title* | Some nice title | It will be displayed on ballon
| descr* | Pin description | Description is only visible when user opens details screen |

*Optional params

##Example

