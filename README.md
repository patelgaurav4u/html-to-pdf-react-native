# html-to-pdf-react-native

Convert html strings to PDF documents using React Native 

#### Support for iOS new Webkit framework (WKWebView)


## Installation

1. Run `npm install html-to-pdf-react-native --save`

### Option 1: Automatic

2. Run `react-native link`

### Option 2: Manual

#### iOS

2. Open your project in XCode, right click on [Libraries](http://url.brentvatne.ca/jQp8) and select [Add Files to "Your Project Name](http://url.brentvatne.ca/1gqUD).
3. Add `libRNHTMLtoPDF.a` to `Build Phases -> Link Binary With Libraries`
   [(Screenshot)](http://url.brentvatne.ca/17Xfe).

#### Android
- Edit `android/settings.gradle` to included

```java
include ':html-to-pdf-react-native'
project(':html-to-pdf-react-native').projectDir = new File(rootProject.projectDir,'../node_modules/html-to-pdf-react-native/android')
```

- Edit `android/app/build.gradle` file to include

```java
dependencies {
  ....
  compile project(':html-to-pdf-react-native')

}
```

- Edit `MainApplication.java` to include

```java
// import the package
import com.gauravp.htmltopdf.RNHTMLtoPDFPackage;

// include package
new MainReactPackage(),
new RNHTMLtoPDFPackage()
```

## Usage
```javascript

import React, { Component } from 'react';

import {
  Text,
  TouchableHighlight,
  View,
} from 'react-native';

import RNHTMLtoPDF from 'html-to-pdf-react-native';

export default class Example extends Component {
  async createPDF() {
    let options = {
      html: '<h1>PDF TEST</h1>',
      fileName: 'test',
      directory: 'Documents',
    };

    let file = await RNHTMLtoPDF.convert(options)
    // console.log(file.filePath);
    alert(file.filePath);
  }

  render() {
    return(
      <View>
        <TouchableHighlight onPress={this.createPDF}>
          <Text>Create PDF</Text>
        </TouchableHighlight>
      </View>
    )
  }
}
```

## Options

| Param | Type | Default | Note |
|---|---|---|---|
| `html` | `string` |  | HTML string to be converted
| `fileName` | `string` | Random  | Custom Filename excluding .pdf extension
| `base64` | `boolean` | false  | return base64 string of pdf file (not recommended)
| `directory` | `string` |default cache directory| Directory where the file will be created (`Documents` folder in example above). Please note, on iOS `Documents` is the only custom value that is accepted.
| `height` | number | 792  | Set document height (points)
| `width` | number | 612  | Set document width (points)


#### iOS Only

| Param | Type | Default | Note |
|---|---|---|---|
| `paddingLeft` | number | 10  | Outer left padding (points)
| `paddingRight` | number | 10  | Outer right padding (points)
| `paddingTop` | number | 10  | Outer top padding (points)
| `paddingBottom` | number | 10  | Outer bottom padding (points)
| `padding` | number | 10 | Outer padding for any side (points), overrides any padding listed before
| `bgColor` | string | #F6F5F0 | Background color in Hexadecimal


#### Android Only

| Param | Type | Default | Note |
|---|---|---|---|
| `fonts` | Array | | Allow custom fonts `['/fonts/TimesNewRoman.ttf', '/fonts/Verdana.ttf']`
