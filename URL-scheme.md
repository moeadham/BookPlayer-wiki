Our url scheme is the following:

`bookplayer://`

We currently support the following actions:

- [play](#play)
- [download](#download)
- [skipRewind](#skipRewind)
- [skipForward](#skipForward)
- [sleep](#sleep)

<a name="play"/>

## play

Resumes playback of the last book played

### Example

`bookplayer://play`

<a name="download"/>

## download

Downloads file specified from the specified URL

### Example

`bookplayer://download?url="https://link-to/your/file.mp3"`

<a name="skipRewind"/>

## skipRewind

Triggers one skip back in time

### Example

`bookplayer://skipRewind`

<a name="skipForward"/>

## skipForward

Triggers one skip forward in time

### Example

`bookplayer://skipForward `

<a name="sleep"/>

## sleep

Configures the Sleep Timer, with the specified `seconds` parameter

Accepted values for `seconds`:
- `-2`, sets timer until the end of current chapter
- `-1`, cancels the timer
- Any value greater than `0`, sets timer with that time

### Example

`bookplayer://sleep?seconds=20`