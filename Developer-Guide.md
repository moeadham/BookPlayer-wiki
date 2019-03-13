This page is intended for developers looking to extend existing functionality (like adding more themes or app icons)

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