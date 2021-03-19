This page is intended for developers looking to extend existing functionality (like adding more themes or app icons)

### Contents  
- [Setting up the project](#xcode)
- [Adding more themes](#themes)
- [Adding more app icons](#icons)
- [Unlocking Plus options](#plus)

<a name="xcode">

## Setting up the project
Follow these steps to setup BookPlayer with your account:

* The first thing to do is remove the CarPlay entitlement, find the file `BookPlayer.entitlements` (BookPlayer › BookPlayer.entitlements) and remove the key `com.apple.developer.playable-content`

  <img width="682" alt="Screen Shot 2021-03-18 at 12 51 37" src="https://user-images.githubusercontent.com/14112819/111673298-d32c7280-87e8-11eb-8044-c0bf8e78f3eb.png">

* Now select the project file, select the target `BookPlayer` and go to the `Signing & Capabilities` tab, here you will:
  * Change the Bundle Identifier for one unique for your organization
  * Enable the `Automatically manage signing` checkbox
  * Select your team from the dropdown
  * Go to the section `App Groups`, make sure the selected group isn't red, if it is, just deselect it, and select it again (if they disappear, hit the refresh icon in the bottom of the empty list and then it'll show up again). Be careful when selecting again, if you have multiple values, the list will jump
  * Go to the section `iCloud`, make sure the container selected isn't red, if it is, just deselect it, and select it again (if they disappear, hit the refresh icon in the bottom of the empty list and then it'll show up again). Be careful when selecting again, if you have multiple values, the list will jump
* Copy your new Bundle Identifier, and this will be the base Bundle Identifier that will be used for the next steps in the following Targets:
  * BookPlayerWidget
    * Change the team from the dropdown
    * Make your bundle identifier the following → `<your-base-bundle-identifier>.BookPlayerWidget`
    * Deselect the App Group, refresh if necessary and select the previously created App Group in the first section
  * BookPlayerWatch
    * Change the team from the dropdown
    * Make your bundle identifier the following → `<your-base-bundle-identifier>.watchkitapp`
    * Deselect the App Group, refresh if necessary and select the previously created App Group in the first section
  * BookPlayerWatch Extension
    * Change the team from the dropdown
    * Make your bundle identifier the following → `<your-base-bundle-identifier>.watchkitapp.watchkitextension`
    * Deselect the App Group, refresh if necessary and select the previously created App Group in the first section
  * BookPlayerIntents
    * Change the team from the dropdown
    * Make your bundle identifier the following → `<your-base-bundle-identifier>.BookPlayerIntents`
  * BookPlayerWidgetUIExtension
    * Change the team from the dropdown
    * Make your bundle identifier the following → `<your-base-bundle-identifier>.BookPlayerWidgetUI`
    * Deselect the App Group, refresh if necessary and select the previously created App Group in the first section
  * BookPlayerKit
    * Change the team from the dropdown
    * Make your bundle identifier the following → `<your-base-bundle-identifier>.BookPlayerKit`
  * BookPlayerWatchKit
    * Change the team from the dropdown
    * Make your bundle identifier the following → `<your-base-bundle-identifier>.BookPlayerWatchKit`

Now for the final steps:
  * Open the file `Info.plist` from the `BookPlayerWatch Extension` folder, and drill down to the property `NSExtension → NSExtensionAttributes → WKAppBundleIdentifier` and update it with the value you used for the Bundle Identifier in the target `BookPlayerWatch`
  * Open the file `Info.plist` from the `BookPlayerWatch` folder, and change the property `WKCompanionAppBundleIdentifier` and update it with the value you used as your base bundle identifier.
  * Clean the Build folder just in case (⌘⇧K)

And you should be able to run the project now 💪 (if you find any problems, please feel free to open a ticket, or contact us via Discord)

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
| lightPrimaryHex | String | (Hex code) Light variant used for primary labels like titles |
| lightSecondaryHex | String | (Hex code) Light variant used for secondary labels like descriptions |
| lightAccentHex | String | (Hex code) Light variant used for actionable items |
| lightSeparatorHex | String | (Hex code) Light variant used for the line separators in tables |
| lightSystemBackgroundHex | String | (Hex code) Light variant used for the background of the library view |
| lightSecondarySystemBackgroundHex | String | (Hex code) Light variant used for the hovering mini player |
| lightTertiarySystemBackgroundHex | String | (Hex code) Light variant used for the progress pie |
| lightSystemGroupedBackgroundHex | String | (Hex code) Light variant used for the background of the settings view |
| lightSystemFillHex | String | (Hex code) Light variant used for the progress pie |
| lightSecondarySystemFillHex | String | (Hex code) Light variant used for the progress pie |
| lightTertiarySystemFillHex | String | (Hex code) Light variant not actually used but needed |
| lightQuaternarySystemFillHex | String | (Hex code) Light variant not actually used but needed |
| darkPrimaryHex | String | (Hex code) Dark variant used for primary labels like titles |
| darkSecondaryHex | String | (Hex code) Dark variant used for secondary labels like descriptions |
| darkAccentHex | String | (Hex code) Dark variant used for actionable items |
| darkSeparatorHex | String | (Hex code) Dark variant for the highlight color |
| darkSystemBackgroundHex | String | (Hex code) Dark variant used for the background of the library view |
| darkSecondarySystemBackgroundHex | String | (Hex code) Dark variant used for the hovering mini player |
| darkTertiarySystemBackgroundHex | String | (Hex code) Dark variant used for the progress pie |
| darkSystemGroupedBackgroundHex | String | (Hex code) Dark variant used for the background of the settings view |
| darkSystemFillHex | String | (Hex code) Dark variant used for the progress pie  |
| darkSecondarySystemFillHex | String | (Hex code) Dark variant used for the progress pie |
| darkTertiarySystemFillHex | String | (Hex code) Dark variant not actually used but needed |
| darkQuaternarySystemFillHex | String | (Hex code) Dark variant not actually used but needed |

<a name="icons"/>

## Adding App Icons
To add a new app icon, you need to:

1. Add a new entry in the file [Icons.json](https://github.com/TortugaPower/BookPlayer/blob/develop/BookPlayer/Library/Icons/Icons.json), which must provide the following fields:

| Field name | Type | Description |
| --- | --- | --- |
| id | String | The id of the icon |
| title | String | The name that you want displayed inside the app |
| imageName | String | The name of the image file |

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