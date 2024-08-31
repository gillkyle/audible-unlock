# Audible scripts

Get your Audible books in MP4 for usage with something like [BookPlayer](https://github.com/TortugaPower/BookPlayer).

Audible encrypts files on your device, you own the rights to the content when you purchase the book ([see this ruling](https://www.eff.org/files/2014/12/10/gov.uscourts.nysd_.425052.82.0.pdf)).

To get a book, it requires a few steps:

1. recover your "activation_bytes" hash for your Audible account, which are used as a key to encrypt your files
2. crack your hash using Audible specific rainbow tables, so you can then decrypt your Audible files with it
3. use your the cracked hash to convert files from the Audible `.aax` format into `.mp4`

## 1. Recover your 

You need to recover or retrieve your "activation_bytes" only once. This single
"activation_bytes" value will work for all your .aax files.

## Note

Git clone this repository on your machine. This repository has the required
rainbow tables `(*.rtc files)` and RainbowCrack binaries.

```
git clone https://github.com/inAudible-NG/tables.git
```

## Usage on Linux

FFmpeg 2.8.1+ is required. Use Wine with the included (in `run` folder) Windows
binaries in case these Linux executables do not run on your distribution.

##### Extract SHA1 checksum from the .aax file

```
$ ffprobe test.aax  # extract SHA1 checksum
...
[mov,mp4,m4a,3gp,3g2,mj2 @ 0x1dde580] [aax] file checksum == 999a6ab8...
[mov,mp4,m4a,3gp,3g2,mj2 @ 0x1dde580] [aax] activation_bytes option is missing!
```

##### Recover "activation_bytes"

```
$ ./rcrack . -h 999a6ab8...
```

## Usage on Windows

Download FFmpeg from https://ffmpeg.zeranoe.com/builds/.

##### Extract SHA1 checksum from .aax file

```
C:\>ffprobe.exe sample.aax
ffprobe version N-79460-g21acc4d Copyright (c) 2007-2016 the FFmpeg developers
  built with gcc 5.3.0 (GCC)
...
[mov,mp4,m4a,3gp,3g2,mj2 @ 039aae60] [aax] file checksum == 999a6ab8...
[mov,mp4,m4a,3gp,3g2,mj2 @ 039aae60] [aax] activation_bytes option is missing!
```

##### Recover "activation_bytes"

```
C:\tables>run\rcrack.exe . -h 999a6ab8...
statistics
-------------------------------------------------------
plaintext found:                              1 of 1
total time:                                   13.98 s
...
result
-------------------------------------------------------
999a6ab8...                               xyz   hex:CAFED00D
```

"activation_bytes" is CAFED00D here.

## References

See http://project-rainbowcrack.com/alglib.htm for details.

## Notes

This is a fork of the https://github.com/inAudible-NG/tables repo, synced to my own profile so where I can store some of my own secrets files, and update steps to be MacOS friendly as it doesn't accept contributions.

Please use responsibly, and only on content you have purchased and are legally authorized to access and backup.