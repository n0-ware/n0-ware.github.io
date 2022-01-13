# Oledump
A python program used to analyze `OLE` (Compound File Binary Format) files. 

## OLE Files
Historically called "compound documents." Think of them as a "mini file system" similar to a Zip archive. These `OLE` documents seamlessly integrate various types of data (components) into one file, such as sound clips, spreadsheets, bitmpas, etc. Files such as `.doc`, `.xls`, and `.ppt` are all well known types. 

These files contain **storages** which are essentially folders that contain **streams** of data, or more **storages**. 

## Analysis
The command `oledump.py <Filename>` will output information on a particular `OLE` file related to its structure.

An `M` next to a stream indicates that it contains a VBA Macro. 

### Arguments
- `-A` &mdash; does an *ASCII* dump similar to `-a` but duplicate lines are removed
- `-S` &mdash; dumps strings
- `-d` &mdash; A raw dump of the stream content
- `-s` STREAM NUMBER or `-select`=STREAM NUMBER allows you to select the stream number to analyze (`-s a` to select all streams)
- `-d` or `--dump` &mdash; Raw dump
- `-x` or `--hexump` &mdash; Hedump
- `-a` or `--asciidump` &mdash; ASCII dump
- `-S` or `--strings` &mdash; strings dump
- `-v` or `--vbadecompress` &mdash; VBA decompression