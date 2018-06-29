Galileo supports an API that enables developers to open the Galileo app or web page through an external URL. The URL can be accessed from within another mobile application or a mobile web page.

The base URL to use Waze Deep Links is:

`https://galileo-app.com/map`

The Galileo application can then locate an address, mark an address on the map, or start a navigation session to an address or destination, depending on which parameters you pass to this URL.

* Start navigation
* Perform search
* Show bookmark on some location

All examples based on same URL `https://galileo-app.com/map?a={nav,search,pin}` where  action name is stored inside `a` param. And everything after it is an action params.

##Preview route or start navigation {#navigation}

Example: `https://galileo-app.com/map?a=nav&dest=53.9,27.4&type=bike`

| param    | value                 | description             |
|----------|-----------------------|-------------------------|
| a        | {route, nav}           | Action `route` opens route preview, `nav` starts navigation right away |
| dest     | lat,lon                 | Destination coordinates |
| dep*     | lat,lon                 | Departure coordinates. By default is user location. |
| type*    | {car, bike, walk}       | Costing function. Default value is `car` |

*Optional params

##Perform search {#search}

Example: `https://galileo-app.com/map?a=search&q=Минск`

| param  | value                 | description            |
|--------|-----------------------|------------------------|
| a      | search                | Action is search       |
| q      | query text            | It could be object name, coordinates or address |

*Optional params

##Show pin {#bookmark}

| param  | value                 | description            |
|--------|-----------------------|------------------------|
| a      | pin                   | Action is pin          |
| loc    | lat,lon               | Pin location           |
| zoom*  | 3 - 22 | Map zoom. Default value is `15` |
| title* | Some nice title | It will be displayed on ballon
| descr* | Pin description | Description is only visible when user opens details screen |

*Optional params

##Example

```
  if ([[UIApplication sharedApplication] canOpenURL:[NSURL URLWithString:@"galileo://"]]) {
      // Galileo is installed. Launch Galileo and start navigation
      NSString *urlStr = [NSString stringWithFormat:@"https://galileo-app.com/map?a=nav&dest=%f,%f", latitude,  longitude];
      [[UIApplication sharedApplication] openURL:[NSURL URLWithString:urlStr]];
  } else {
    // Galileo is not installed. Launch AppStore to install Galileo app
    [[UIApplication sharedApplication] openURL:[NSURL URLWithString:@"http://itunes.apple.com/us/app/id321745474"]];
  }
```