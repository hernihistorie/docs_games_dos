# docs_games_dos

Dokumentace (popisky, návody, screenshoty) k hrám na výjezdy
Kategorie: MS-DOS

Seznam se načítá v našem forku [RLOADERu](https://github.com/hernihistorie/RLoader), který se stará o menu v DOSových počítačích

## Specifikace

```
.\RHGAMES\LIST_DIRECTORY
    LIST.TXT  list entries definition
    TITLE\    programs titles screens
    IN_GAME1\ in-game screenshots
    IN_GAME2\ second in-game screenshots
    INFO\     info markdown files
```
    
    
### LIST.TXT
List of entries, one per line, with these columns:

- absolute path with drive letter
- executable filename
- setup program filename (if exists)
- number of cycles
- program title

Lines that starts with # character will be recognized as comments.

Each column must be separated by one or more white-space characters (spaces or tabs).

Executable filename is the executable or batch file to be used to launch the program. Extension is mandatory.

Setup filename is the executable or batch file to be used to setup the program. When setup program not exists a - character must be specified. Extension is mandatory.

The cycles will be used inside DOSBox to automatically set correct emulation speed. If zero is specified 'auto' emulation speed will be set.

The program title will be read until end-of-line character or end-of-file, so it can contains any character.

### Thumbnails generation
rloader thumbnails must be standard 4 bits-per-pixel uncompressed Windows bitmap. Only first 14 colors can be used, 2 colors are reserved by the user interface of this program. Width of the image must be 320 pixels.

You can use any command line tool that supports image manipulation. For example using ImageMagick, which is a free and open source tool, you can write:

```bash
magick.exe input.png -resize 320 -dither Ordered -depth 4 -colors 14 -type palette bmp3:output.bmp
```

where:

`-resize 320` rescales the image to 320 pixels
`-dither` Ordered applies ordered dithering (optional)
`-depth 4` specifies 4 bits per pixel (16 colors)
`-colors 14` remaps using only 14 colors
`-type color` ensures conversion to a palettized image
`bmp3` specifies an uncompressed Windows bitmap
You can avoid bilinear filtering caused by downscaling by adding the `-filter` flag with the values ​​Point or NearestNeighbor.

`TITLE` subdirectory
This directory will contains optional programs titles screen-shots thumbnails.

`IN_GAME1` and `IN_GAME2` subdirectory
This directory will contains optional in-programs screen-shots thumbnails.

`INFO` subdirectory
This directory will contains optional simplified markdown files what will describe specific program usage, options, keyboard shortcuts or notes, with a maximum line length of 38 characters, markdown formatting excluded.

NOTE: titles, in-programs and info filenames must match the inner directory name of the absolute path specified in LIST.TXT file.

