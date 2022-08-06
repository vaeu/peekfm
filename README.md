# peekfm

This is a small utility written in POSIX awk that crawls user-defined
artist shoutboxes on lastfm and prints shouts published throughout the
day. There is no way to parse shouts from the past for now, however. I
may or may not add this functionality in the future.

## Dependencies

`peekfm` relies on `curl` to scrape web pages.

## Usage

```
$ peekfm
```

First of, create a directory that would contain an artists file later
on:

```
$ mkdir -p "${XDG_DATA_HOME:-$HOME/.local/share}/peekfm"
```

Secondly, create a list of musicians whose shoutboxes you’d like to
check out:

```
$ cat >> "${XDG_DATA_HOME:-$HOME/.local/share}/peekfm" <<EOF
Boards of Canada
Whitehouse
Current 93
Crystal Castles
Aphex Twin
EOF
```

Proper capitalisation is not required for the program to work correctly,
so the following snippet is perfectly valid, although not encouraged:

```
            CURRENT 93
BOARdS oF CANada
    whITeHOUSE
```

As of 2022-08-06, here is the output `peekfm` produces based on artists
we’ve defined earlier:

```
$ peekfm
peekfm: fetching artist shoutboxes as of 2022-08-06
peekfm: processing 5 web pages...

BOARDS OF CANADA > This band is so boring and trash
BOARDS OF CANADA > Sez u

CRYSTAL CASTLES > MUTUAL PULLING THROUGH 🙌💟

APHEX TWIN > overrated
APHEX TWIN > huh?
```

Since none of the users had posted in shoutboxes of ‘Current 93’ and
‘Whitehouse’ at that particular date, nothing got printed to the
terminal.

> **NOTE**:
>
> Some users are going to be using emojis in their comments, so having a
> font that properly renders Unicode character set can be useful.

On Debian GNU/Linux such a font can be installed by running the
following command:

```
$ sudo apt-get install fonts-symbola
```

On OpenBSD it’s as easy as

```
$ doas pkg_add symbola-ttf
```

You may need to cache the fonts after the installation is complete:

```
$ fc-cache -fv
```
