This page is intended for developers looking to extend existing functionality (like adding more themes or app icons)

### Contents  
- [Setting up the project](#xcode)
- [Adding more themes](#themes)
- [Adding more app icons](#icons)
- [Unlocking Plus options](#plus)

<a name="xcode">

## Setting up the project

After cloning the repository in your device, follow these steps to have BookPlayer run for you:

- From Finder, open the project folder and navigate to the folder `BuildConfiguration`, this will have two files in it. Make a copy of `Debug.template.xcconfig` and rename it to `Debug.xcconfig`
- Open the project in Xcode, and open the file you just created `Debug.xcconfig`. You will find that it has multiple parameters to be filled

  <img width="561" alt="Screen Shot 2021-05-18 at 08 54 40" src="https://user-images.githubusercontent.com/14112819/118663969-b7c4f000-b7b6-11eb-8343-6428ee9d2fa9.png">
  
  _Note: if you open Xcode before these steps, you'll find that the `Debug` file in the project is in color red, do not delete it, removing the reference will cause problems when launching the app. If it got deleted, then with git, discard the changes made to the `project.pbxproj` and please do the previous steps first_

Up to this point, you can already run BookPlayer in your simulator, but if you want to run it in your device, then you'll need to access your account in the [Apple's developer website](https://developer.apple.com) and continue with the following points:

- First we'll need a development certificate for your machine, verify in the [Certificate list](https://developer.apple.com/account/resources/certificates/list) if you can spot the one for your current machine. If not, you can manually generate the certificate following [this guide](https://ioscodesigning.com/generating-code-signing-files/#generate-a-code-signing-certificate-manually), download it, and double click to install the certificate.
- Now, before creating the app identifier, it'll be easier for us, if we first create the App Groups container and the iCloud container:
  - Go to [register a new identifier](https://developer.apple.com/account/resources/identifiers/add/bundleId), select `App Groups` and press `Continue`
  - For the `Description`, you can use any value that will make it easier for you to identify that it's for BookPlayer. For the `Identifier`, as soon as you type something, you'll notice that `group` is automatically added to the field, add the bundle id that you'll use for the main app, and add the sufix `.files` at the end, so the final Identifier will look something like `group.com.test-bundle.id.files`

    <img width="1215" alt="Screen Shot 2021-05-18 at 09 27 50" src="https://user-images.githubusercontent.com/14112819/118669436-5a7f6d80-b7bb-11eb-9269-192ac84fe2d3.png">

  - Press `Continue` and you'll have created the App Group needed for the project
  - We'll now create the iCloud Container in a similar way, Go to [register a new identifier](https://developer.apple.com/account/resources/identifiers/add/bundleId), select `iCloud Containers` and press `Continue`
  - For the `Description`, you can use any value that will make it easier for you to identify that it's for BookPlayer. For the `Identifier`, as soon as you type something, you'll notice that `iCloud` is automatically added to the field, add the same bundle id that you used in the previous step, so the final Identifier will look something like `iCloud.com.test-bundle.id`

    <img width="1215" alt="Screen Shot 2021-05-18 at 09 31 46" src="https://user-images.githubusercontent.com/14112819/118670050-e5f8fe80-b7bb-11eb-812f-5df98dae4406.png">

  - Press `Continue` and you'll have created the iCloud Container needed for the project
- We'll now create the main App ID we'll use for the project, since it requires the App Groups and iCloud capabilities, it cannot contain wildcards
  - Go to [register a new identifier](https://developer.apple.com/account/resources/identifiers/add/bundleId), select `App Ids` and press `Continue`
  - Select `App` and press `Continue`
  - For the `Description`, you can use any value that will make it easier for you to identify that it's for BookPlayer. For the `Bundle ID`, make sure the option `Explicit` is selected, and we'll add the same bundle id that you used when creating the containers in the previous step, so the Bundle ID will look something like `com.test-bundle.id` (This is our base bundle id we'll use for future steps)
  - From the Capabilties list, make sure you select `App Groups`, `iCloud`, `SiriKit`, and `Sign In with Apple`
  - Press `Continue` and then `Confirm` to finish creating the main App Id for your configuration
  - From [the list of App IDs](https://developer.apple.com/account/resources/identifiers/list), select your newly created App Id, and now you'll configure the App Groups and iCloud Container we have already created

    <img width="1189" alt="Screen Shot 2021-05-18 at 09 44 02" src="https://user-images.githubusercontent.com/14112819/118672322-c4991200-b7bd-11eb-8f48-e9e6e9a9ae38.png">

  - Click `Configure` and select from the list, the container you created previously, then click `Save`. Make sure that you have configured both the `App Groups` and the `iCloud` capability for this App ID
- BookPlayer requires App IDs for all its current extensions, so we need to repeat the previous process for creating an App ID, with these minor observations:
  - Create a new App ID with the bundle id being the base bundle id + the suffix `.BookPlayerWidget` (for our example it would look something like `com.test-bundle.id.BookPlayerWidget`). This App ID needs to have the same App Group capability enabled and configured like the main App ID (no iCloud needed)
  - Create a new App ID with the bundle id being the base bundle id + the suffix `.watchkitapp` (for our example it would look something like `com.test-bundle.id.watchkitapp`). This App ID needs to have the same App Group capability enabled and configured like the main App ID (no iCloud needed)
  - Create a new App ID with the bundle id being the base bundle id + the suffix `.watchkitapp.widgets` (for our example it would look something like `com.test-bundle.id.watchkitapp.widgets`). This App ID needs to have the same App Group capability enabled and configured like the main App ID (no iCloud needed)
  - Create a new App ID with the bundle id being the base bundle id + the suffix `.BookPlayerWidgetUI` (for our example it would look something like `com.test-bundle.id.BookPlayerWidgetUI`). This App ID needs to have the same App Group capability enabled and configured like the main App ID (no iCloud needed)
  - Create a new App ID with the bundle id being the base bundle id + the suffix `.BookPlayerShareExtension` (for our example it would look something like `com.test-bundle.id.BookPlayerShareExtension`). This App ID needs to have the same App Group capability enabled and configured like the main App ID (no iCloud needed)  
  - If you don't have an App ID that is just a wildcard `*` then you'll need to create it, this will be used for the Intents extension, which doesn't require capabilities enabled
- The last thing we need to do in the Apple developer website, is to create a development provisioning profile for each one of the the App IDs we created in the previous step. Thankfully, this is straightforward:
  - Go to [Register a New Provisioning Profile](https://developer.apple.com/account/resources/profiles/add)
  - Select `iOS App Development` and press `Continue`
  - Select the App ID from the dropdown and press `Continue`
  - Select the Certificate for your machine (the one you created at the start of this process)
  - Select your registered device where you'll run BookPlayer and press `Continue`. If you haven't registered your device, you can do it [here](https://developer.apple.com/account/resources/devices/add). To find your device's `UDID`, connect your phone to your Mac, open Xcode, open `Window` → `Devices and Simulators`, select your phone, and use the value from the field `Identifier`.
  - Use the `Default` entitlements (if you have requested CarPlay functionality to Apple, you will have the option here to select CarPlay entitlements)
  - For the `Provisioning Profile Name`, use something that will be easy to identify and click `Generate`. These names are the ones that we'll need to fill the `Debug.xcconfig` file
  - Download and double click the file to install them to Xcode.

We are now ready to fill the configuration values:
- `DEVELOPMENT_TEAM` → Go to [the Apple's developer membership tab](https://developer.apple.com/account/#/membership), copy the value for the `Team ID` field on the website
- `BP_ENTITLEMENTS` → Keep the value already there, but if you have requested CarPlay functionality to Apple, then you can modify it, and leave `BookPlayer` so that CarPlay is enabled
- `BP_BUNDLE_IDENTIFIER` → This is the base bundle id of the first App ID we created
- `BP_PROVISIONING_MAIN` → The provisioning profile that used the first App ID we created
- `BP_PROVISIONING_WIDGET` → The provisioning profile that used the App ID with the suffix `.BookPlayerWidget`
- `BP_PROVISIONING_WATCH` → The provisioning profile that used the App ID with the suffix `.watchkitapp`
- `BP_PROVISIONING_WATCH_WIDGETS` → The provisioning profile that used the App ID with the suffix `.watchkitapp.widgets`
- `BP_PROVISIONING_INTENTS` → The provisioning profile that used the App ID with the wildcard
- `BP_PROVISIONING_WIDGET_UI` → The provisioning profile that used the App ID with the suffix `.BookPlayerWidgetUI`
- `BP_PROVISIONING_SHARE_EXTENSION` → The provisioning profile that used the App ID with the suffix `.BookPlayerShareExtension`

You should be able to run the project now in your device 💪 (if you find any problems, please feel free to open a ticket, or contact us via Discord)

<a name="themes"/>

## Adding more themes

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