# react-native-share-instagram
Share your image with the Instagram app using `Intents` (iOS & Android)

## Getting started

`$ yarn add https://github.com/DenisDovganiuc/react-native-share-instagram`

## Automatic installation

`$ react-native link @micabe/react-native-share-instagram`


## Usage
```javascript
import RNReactNativeSharingWinstagram from 'react-native-sharing-winstagram';

RNReactNativeSharingWinstagram.shareWithInstagram(this.state.fileName, this.state.base64EncodedImageString, message => {
  if (message) alert(message)
}, error => {
  alert(error.message) // error callback for IOs only
})
```

### Troubleshouting

* Make sure you have authorised in `Info.plist` your app to communicate with the Instagram app (iOS):

```xml
<key>LSApplicationQueriesSchemes</key>
<array>
  <string>instagram</string>
</array>

<key>NSPhotoLibraryUsageDescription</key>
<string>This app requires access to the photo library to share on Instagram.</string>
```

* Make sure you done the following steps in your app to communicate with the Instagram app (Android):

1. Add a FileProvider `<provider>` tag in `AndroidManifest.xml` under `<application>` tag.
Specify a unique authority for the `android:authorities` attribute to avoid conflicts ( `${applicationId}.provider` ).

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    ...
    <application
        ...
        <provider
          android:name="android.support.v4.content.FileProvider"
          android:authorities="${applicationId}.provider"
          android:exported="false"
          android:grantUriPermissions="true">
          <meta-data
            android:name="android.support.FILE_PROVIDER_PATHS"
            android:resource="@xml/provider_paths"/>
        </provider>
    </application>
</manifest>
```

2. Then create a `provider_paths.xml` file in `res/xml` folder.
Folder may be needed to created if it doesn't exist.

```xml
<?xml version="1.0" encoding="utf-8"?>
<paths xmlns:android="http://schemas.android.com/apk/res/android">
    <external-path name="external_files" path="."/>
</paths>
```

3. Add the following lines of code into `MainApplication.java`.

```java
...
import com.reactlibrary.ShareApplication;
...

public class MainApplication ... implements ShareApplication {
  ...
  @Override
  public String getFileProviderAuthority() {
    return "${applicationId}.provider";
  }
  ...
}
```

### Advanced usage

* You can use the [react-native-fetch-blob](https://github.com/wkh237/react-native-fetch-blob) library to download your remote image and convert it to `.base64()`

### Contribution

* Test library to work with windows OS
