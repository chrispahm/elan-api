# ELAN NRW InVeKos API
Provides cropping data and geometries for the plots of a single farm through the agricultural direct aid program.
The API is a (scraping) wrapper for the InVeKos `download-portal` of the [Landwirtschaftskammer Nordrhein-Westfalen](https://www.landwirtschaftskammer.de/).

## Installation
```
npm install elan-api
```

## Usage example
```js
const elanGet = require('elan-api')

elanGet('farmNo', 'password', {
  type: 'Verzeichnis',
  year: '2018'
})
.then(res => {
  // res is a string with the contents of the Flaechenverzeichnis.xml file provided by ELAN
})
.catch(err => {
  // connection errors, credentials etc...
})
```

## Methods
The module exports one method. It takes the following arguments:

| Name    | Type   | Example                           | Description                                                                                                                                                                                                                                                                                                                                                          |
|:--------|:-------|:----------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| farmNo  | string | `'123456789'`                     | The 12 digit *Betriebsnummer* (farm number), **without** the 3 starting digits (276, indicating NRW)                                                                                                                                                                                                                                                                 |
| pass    | string | `'123456'`                        | The 6 digit pin code associated to the *Betriebsnummer*                                                                                                                                                                                                                                                                                                              |
| options | object | `{ type: 'Verzeichnis', year: '2018' }` | *Optional*. The options may contain a *type* (string) and and/or a *year* (string) property. The *type* may either be 'Verzeichnis' (returns *Flaechenverzeichnis.xml*) or *Geometrien* (returns 'Teilschlaggeometrien.xml'). If *type* is ommited, 'plots' will be returned. If the *year* property is omitted, the method will return the latest available InVeKos data. |

## Testing
In order to test, you need to place a `credentials.json` file in the spec folder. Also results from the *Verzeichnis* and *Geometrien* calls need to be saved as geometries.gml and respectively verzeichnis.xml in the test folder.
The JSON needs to have the following structure, where the dummy values have to be replaced with a valid farmNo and password:

```json
{
  "farmno": "123456789",
  "pass": "123456"
}
```

Once the file is created, you can run `npm test` in order to run the unit tests.

## Contribution
Please feel free to submit an issue or a pull request.

## License
MIT
