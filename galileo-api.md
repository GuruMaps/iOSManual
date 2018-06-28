Galileo supports an API that enables developers to open the Galileo app or web page through an external URL. The URL can be accessed from within another mobile application or a mobile web page.

The base URL to use Waze Deep Links is:

`https://galileo-app.com/map`

The Galileo application can then locate an address, mark an address on the map, or start a navigation session to an address or destination, depending on which parameters you pass to this URL.

* Start navigation
* Perform search
* Show bookmark on some location

##Start navigation {#navigation}

| param  | value                 | description            |
|--------|-----------------------|------------------------|
| a      | nav                   | Action is navigation   |
| lat    | from -90.0 to 90.0    | Destination latitude   |
| lon    | from -180.0 to 180.0  | Destination longitude  |

Example: `https://galileo-app.com/map?a=nav&lat=1.234&lon=1.234`

```
[[UIApplication sharedApplication] openURL:
    [NSURL URLWithString:@"galileo://maps.yandex.ru/?ll=30.310182,59.951059&z=12&l=map"]];
```

##Perform search {#search}

##Show bookmark {#bookmark}