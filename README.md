
# batch-rename

A script to **batch rename/move** files using **regular expressions**
with **sensible defaults** and **nice output**.
Very similar to perl-rename, but uses Python regular expressions and
interactively asks before a rename.
Tested on GNU/Linux, unlikely to work on other platforms.

# Invocation

This is the output of the ```rn --help``` command.
```
usage: rn [-h] [-v] [-q] [-p] [-b] [-c] match replace [file [file ...]]

Batch rename files.

positional arguments:
  match          regexp match
  replace        regexp replace
  file           list of files to rename

optional arguments:
  -h, --help     show this help message and exit
  -v, --verbose  write information about every moved file
  -q, --quiet    do not output anything
  -p, --pretend  just list the mv commands, do not write anything
  -b, --batch    do not ask before renaming
  -c, --copy     copy the files instead of just moving
```

## Usage

**TL;DR:** Python regexp replace is used
([```re.sub```](https://docs.python.org/2/library/re.html#re.sub)).
Single quote everything.

The program asks you before doing anything by default, so feel free to experiment.

### Examples

- Replace underscores with spaces (in all mp3 files):
```bash
rn _ ' ' *.mp3
```

- Drop stuff in brackets (in all files in the current directory):
```bash
rn ' \(.*\)' ''
```

- Print every letter twice (in all files in the current directory):
```bash
rn '(.)' '\1\1'
```
