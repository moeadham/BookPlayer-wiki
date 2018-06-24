## Naming things

It's not always easy to name things in a larger project, so this page tries to lay out some base rules.

- The app is called *BookPlayer*.
- The collection of books and playlists is called *Library*.
- A *playlist* contains *files* not books as playlists because an item inside a playlist is most likely only a partial of a whole book.
- A *playlist* is always lowercase because it is the describing noun of a list with a distinctive name chosen by the user.
- A book is always a *book*, we don't need to say audiobook.
- You can only import *files* not books, they become *items* (in a playlist) or *books* (in the *Library*) only after import.
- All alerts should provide named actions, never yes or no.
- BookPlayer has a `Player` screen and a `Mini Player` floating at the bottom of the Library

## Style

- Alerts should be concise but friendly.
- Follow [iOS Human Interface Guidelines](https://developer.apple.com/ios/human-interface-guidelines/visual-design/terminology/)