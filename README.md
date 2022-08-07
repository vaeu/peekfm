# peekfm

This is a small utility written in POSIX awk that crawls user-defined
artist shoutboxes on lastfm and prints shouts published throughout the
day.

## Dependencies

`peekfm` relies on `curl` to scrape web pages.

## Usage

```
$ peekfm [YYYY-MM-DD]
```

First of, create a directory that would contain an artists file later
on:

```
$ mkdir -p "${XDG_DATA_HOME:-$HOME/.local/share}/peekfm"
```

Secondly, create a list of musicians whose shoutboxes you’d like to
check out:

```
$ cat >> "${XDG_DATA_HOME:-$HOME/.local/share}/peekfm/artists" <<EOF
Current 93
Whitehouse
Hella
平沢進
Orchid
EOF
```

Proper capitalisation is not required for the program to work correctly,
so the following snippet is perfectly valid, although not encouraged:

```
            CURRENT 93
BOARdS oF CANada
    whITeHOUSE
```

### Parsing recent shouts

Let’s run the program without feeding it any arguments first so it can
fetch the web pages that we can parse locally later on.

```
$ peekfm
peekfm: fetching artist shoutboxes as of 2022-08-07
peekfm: processing 5 web pages...

HELLA > i like death grips and all, but i need way more of this

ORCHID > not gay but listening to orchid is listening to orchid
```

Since none of the users had posted in shoutboxes of ‘Current 93’,
‘平沢進’ and ‘Whitehouse’ at that particular date, nothing got printed
to the terminal.

### Parsing shouts published at a given date

Since we’ve run the program once without any arguments, it fetched web
pages of our artists and stored those in a temporary directory. If we
were to look up shouts published yesterday, two weeks—or even
months—ago, we could easily do this without re-downloading every page by
giving the program a specific date in the format of ‘YYYY-MM-DD’:

> **NOTE**:
>
> The program parses the index page of the comments, so many older
> shouts will not be printed out.

```
$ peekfm 2021-07-29
peekfm: processing 5 web pages...

平沢進 > the new album is a fkn masterpiece

$ peekfm 2022-04-18
peekfm: processing 5 web pages...

CURRENT 93 > That's exactly what I meant brother
CURRENT 93 > cock some

HELLA > makes my toes squirm, i totally reccomend!
```

### Dealing with Unicode

Some users are going to be using emojis in their comments, so having a
font that properly renders Unicode character set can be useful.

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
