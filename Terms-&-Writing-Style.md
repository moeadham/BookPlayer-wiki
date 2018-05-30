## Naming things

It's not always easy to name things in a larger project, so this page tries to lay out some base rules.

- The app is called *BookPlayer*.
- The collection of books and playlists is called *Library*.
- A playlist contains *items* not books. 
- An *item* is an entry in a *playlist*. It can be a whole book if the user wants to order an anthology or series, but most likely it's a part of a book that was too long to be contained in one file.  
- A *playlist* is always lowercase because it is the describing noun of a list with a distinctive name chosen by the user
- A book is always a *book*, we don't need to say audiobook.
- You can only import *files* not books, they become *items* (in a playlist) or *books* (in the *Library*) only after import.
- All alerts should provide named actions, never yes or no.

## Style

- Alerts should be concise but friendly.