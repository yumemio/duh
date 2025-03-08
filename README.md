# `duh`: `du` with a timeout

`duh` is a simple wrapper around `du` with a per-target timeout.

## Requirements

* `bash`
* `timeout` (part of `coreutils`)

## Installation

Copy duh into a folder in your `$PATH`, e.g.:

```console
# install -m 755 duh /usr/local/bin
```

## Usage

### Example

```console
# # timeout: 2 seconds
# # --exclude, -h, and -s will be passed to du

# duh --exclude=/mnt -hsT2 /* | sort -hr
49G	/var
2.7G	/root
2.1G	/swapfile
2.0G	/opt
180M	/boot
28M	/etc
5.2M	/lost+found
2.1M	/run
152K	/tmp
24K	/media
20K	/export
4.0K	/cdrom
[timeout]	/usr
[timeout]	/srv
[timeout]	/snap
[timeout]	/home
0	/vmlinuz.old
0	/vmlinuz
0	/sys
0	/sbin
...
```

### Description

```
duh [DU_OPTIONS] -T TIMEOUT [FILE]...
```

For each FILE, duh calls:

```
timeout TIMEOUT du [DU_OPTIONS] FILE
```

If timeout occurs (exit status 124), it prints:

```
[timeout]    FILE
```

`TIMEOUT` is given in seconds.

Any occurrence of `-d` or `--max-depth` causes an error.

All options (except `-T`/`--timeout`) are passed to `du`.

## Options

* `--help`: Show the help message and exit.

## Why

I'm tired of staring blankly at the screen while running `du` to find out which directory is gobbling up the disk space, manually hitting <kbd>Ctrl</kbd>-<kbd>C</kbd> when it outgrows my patience.

Duh.

I [asked ChatGPT](https://en.wikipedia.org/wiki/Vibe_coding) to see if it can make my life easier - and this is what I got.
