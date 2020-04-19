Our url scheme is the following:

`bookplayer://`

We currently support the following actions:

* `play`
* `download`
* `skipRewind`
* `skipForward`
* `sleep`

## play

Resumes playback of the last book played

### Example

`bookplayer://play`

## download

Downloads file specified from the specified URL

### Example

`bookplayer://download?url="https://link-to/your/file.mp3"`

## skipRewind

Triggers one skip back in time

### Example

`bookplayer://skipRewind`

## skipForward

Triggers one skip forward in time

### Example

`bookplayer://skipForward `

## sleep

Configures the Sleep Timer, with the specified `seconds` parameter

Accepted values for `seconds`:
* `-2`, sets timer until the end of current chapter
* `-1`, cancels the timer

### Example

`bookplayer://sleep?seconds=20`