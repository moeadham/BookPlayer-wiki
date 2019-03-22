This page is intended for developers looking to extend existing functionality (like adding more themes or app icons)

### Contents  
- [Adding more themes](#themes)
- [Adding more app icons](#icons)
- [Unlocking Plus options](#plus)

<a name="themes"/>

## Adding more themes
All the colors in the app, are derived from four main colors for the light variant, and four main colors for the dark variant. These colors are categorized as: 

- The primary color: used for titles.
- The secondary color: used for subtitles.
- The accent color: used as the tint for buttons and selected items.
- The background color.

To create a new theme, it's as simple as adding a new entry in the file [Themes.json](https://github.com/TortugaPower/BookPlayer/blob/develop/BookPlayer/Library/Themes/Themes.json), which must provide the following fields:

| Field name | Type | Description |
| --- | --- | --- |
| title | String | The name that you want displayed inside the app |
| defaultPrimary | String | (Hex code) Light variant for the primary color |
| defaultSecondary | String | (Hex code) Light variant for the secondary color |
| defaultAccent | String | (Hex code) Light variant for the highlight color |
| defaultBackground | String | (Hex code) Light variant for the background color |
| darkPrimary | String | (Hex code) Dark variant for the primary color |
| darkSecondary | String | (Hex code) Dark variant for the secondary color |
| darkAccent | String | (Hex code) Dark variant for the highlight color |
| darkBackground | String | (Hex code) Dark variant for the background color |

<a name="icons"/>

## Adding App Icons
To add a new app icon, you need to:

1. Add a new entry in the file [Icons.json](https://github.com/TortugaPower/BookPlayer/blob/develop/BookPlayer/Library/Icons/Icons.json), which must provide the following fields:

| Field name | Type | Description |
| --- | --- | --- |
| id | String | The id of the icon |
| title | String | The name that you want displayed inside the app |
| imageName | String | (Hex code) Light variant for the primary color |

2. Provide the necessary image assets for the [iPhone folder](https://github.com/TortugaPower/BookPlayer/blob/develop/BookPlayer/Library/Icons/assets/iPhone) and the [iPad folder](https://github.com/TortugaPower/BookPlayer/blob/develop/BookPlayer/Library/Icons/assets/iPad).
  - iPhone sizes: 120x120 (@2x), 180x180 (@3x)
  - iPad sizes: 152x152 (@2x), 167x167 (@3x)

3. Update the [Info.plist](https://github.com/TortugaPower/BookPlayer/blob/develop/BookPlayer/Info.plist) to let the OS know about these options.
  - There are two `CFBundleAlternateIcons` in the list, one for the iPhone icons, and another for the iPad icons
  - Create a new `Dictionary` key for both options. Use the `title` of the new icon as the name of the key
  - For these newly created `Dictionary` keys, add a new `Array` key for each of them. Use `CFBundleIconFiles` as the name of the new `Array` keys.
  - The final step, is to add one element to each of these new `Array` keys. This new element is a `String` type, and should have the `imageName` as its value

<a name="plus"/>

## Unlocking Plus options
The easiest way is to remove the `locked` key from the `json` objects inside the files [Info.plist](https://github.com/TortugaPower/BookPlayer/blob/develop/BookPlayer/Info.plist) and [Icons.json](https://github.com/TortugaPower/BookPlayer/blob/develop/BookPlayer/Library/Icons/Icons.json). When you launch the app, everything should be unlocked.

The other option is to modify the preferences file of the app, it usually is found in the following path inside the app container: `Library/Preferences/com.tortugapower.audiobookplayer.plist`. In this file, add the following entry
```xml
<key>userSettingsDonationMade</key>
<true/>
```