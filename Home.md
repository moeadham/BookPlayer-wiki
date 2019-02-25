# Frequently Asked Questions

## Whats coming next to BookPlayer?

See [our Roadmap](https://github.com/TortugaPower/BookPlayer/projects/1).

## Where can I get audiobooks that work with BookPlayer?

[LibriVox](https://librivox.org/) provides many wonderful audiobooks to start. They even have a M4B download option which is the format that works best with BookPlayer. 

You can also easily combine the MP3 files from audiobooks you bought on CD using the tools found below.

## How to combine MP3 files into M4B audio books

While BookPlayer supports playing MP3 just fine, it really shines when used with M4B based audio books.

To create these, there are several tools at your disposal: 

- [Audiobook Binder](http://bluezbox.com/audiobookbinder.html) (Mac, Free) 
- [Audiobook Creator](http://www.audiobookcreator.de/en/index.html) (Windows, Free) 
- [Chapter and Verse](http://lodensoftware.com/chapter-and-verse/) (Windows, Free) 

We do not have any affiliation with any of these tools. If you find something that works better for you, please tell us so we can extend our list.

Combining your files not only makes it easier to handle them, but also makes it easier for BookPlayer to display the right artwork and chapters.

## How to import audiobooks into BookPlayer

BookPlayer supports three ways to import audiobooks:

- [Airdrop](https://support.apple.com/en-us/HT204144). 
This is a bluetooth-enabled feature, which Apple devices support, so if you have a Mac, you can transfer your books directly to your phone by dragging and dropping.

- [Third-party local apps](https://support.apple.com/en-us/HT206481). 
Other apps you may have installed in your phone (like Dropbox, Google Drive), will notify the phone that they are ‘File Providers’, making their files available for any app in the phone. If you have one of these type of apps installed, they will be listed alongside your iCloud ‘Folder’ in the file picker.

- [iTunes File Sharing](https://support.apple.com/en-us/HT201301). This requires iTunes installed and it’s independent of platform (you can do it if you have a Windows or a Mac).

## Problem importing multiple files via Third-party local apps

We have received feedback that after selecting multiple files and pressing 'Done' nothing happens.

What is actually happening, is that the native `Files` app is downloading the files, but it's not presenting the feedback necessary, and BookPlayer doesn’t get any notification about the selection, until all the selected files are downloaded. 

Unfortunately, this means that once the screen to import files is presented, the control and interaction is out of our hands, until a selection has been made and our app is notified by the phone operating system.

The lack of downloading feedback, could be either a bug on Apple’s part, or a bug in the implementation of these file providers (apps like Google Drive, Dropbox, etc). 

We recommend testing first with one file and see if the `Files` app present the proper feedback. Otherwise we'd recommend one of the other two options to import audiobooks that BookPlayer has.