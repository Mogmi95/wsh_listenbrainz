## wsh_listenbrainz

Please pay special attention to this: http://listenbrainz.org/contribute

>While the project remains in an alpha stage, we cannot promise that the data
will remain stable and intact. We may decide to wipe our database and
to start over again. Until the project goes into beta, you should not have
ListenBrainz be the only place where you keep your listen history!

Currently, the script will not retry failed submissions but it can log
all plays to file(s) inside your foobar2000 profile folder. If needed,
I may be able to modify the script to bulk submit these cached plays in future.

###Known issues

`foobar2000` cannot read the `UFID` id3v2 frame written by `Picard`.
It can use `MUSICBRAINZ_TRACKID` or `MUSICBRAINZ TRACK ID` if it's
written as `TXXX`.

###Submissions

Along with the timestamp, the following tags will be submitted:

```
ARTIST
TRACK
ALBUM
TRACK NUMBER
MUSICBRAINZ_ARTISTID, MUSICBRAINZ ARTIST ID
MUSICBRAINZ_ALBUMID, MUSICBRAINZ ALBUM ID
MUSICBRAINZ_TRACKID, MUSICBRAINZ TRACK ID
```

`ARTIST` and `TRACK` are required, the rest will only be sent if
present. The script uses the same standard as `Last.fm` for deciding
how much of a track you have to play for it to count.This is either
half the track length or 4 minutes - whichever is lower.

###Instructions

Install `WSH panel mod`
https://code.google.com/p/foo-wsh-panel-mod/downloads/list

Go to `File>Preferences>Tools>WSH panel mod` and make
sure `Safe mode` is disabled. Restart `foobar2000` when prompted.

Add a `WSH panel mod` panel to your layout and paste the contents of 
`listenbrainz.txt` inside it.

There are three variables which you can edit right at the top of the script:

```javascript
//get your token from http://listenbrainz.org/user/import
var token = "";
//if true, outputs submission data to the foobar2000 console
var show_data = false;
//if true, all plays will be logged to file(s) inside your foobar2000 profile
//or main foobar folder if using portable mode
//%appdata%\foobar2000\listenbrainz\MM.YYYY.json
//d:\apps\foobar2000\listenbrainz\MM.YYYY.json
var log_data = true;
```

It's just a blank grey panel with no UI so play some music. You can check
the `Console` found on the `View` menu to see the messages it reports.

In additon to the optional data output, the `Console` should always report
the server response. For me, it is currently returning HTTP status 200/success.
YMMV!
