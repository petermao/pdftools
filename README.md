pdftools
========

* **Copyright (c)** 2015 Stefan Lehmann
* **License:** MIT
* **Description:** Python-based command line tool for manipulating PDFs. It is based on the pypdf package.

[![Build Status](https://travis-ci.org/stlehmann/pdftools.svg?branch=master)](https://travis-ci.org/stlehmann/pdftools)
[![PyPI version](https://badge.fury.io/py/pdftools.svg)](https://badge.fury.io/py/pdftools)
[![Downloads](https://pepy.tech/badge/pdftools)](https://pepy.tech/project/pdftools)
[![Downloads](https://pepy.tech/badge/pdftools/week)](https://pepy.tech/project/pdftools/week)

## Installation notes

Ideally, you should be able to clone this repo and run `pip install -e .` to install the package locally.

On OSX, I had to go into `~/Library/Python/<python-version>/lib/python/site-packages/easy-install.pth` and add the local repo directory.

## Features

* add, insert, remove and rotate pages
* split PDF files in multiple documents
* copy specific pages in a new document
* merge or zip PDF files into one document

## Usage

*pdftools* adds some scripts to your existing Python installation that can be called via the command line.
The description for each script is listed below.

In cases where a bare arguent, like `dest` or `src`, follows a switch with an
indefinite number of arguments, like `--pages` or `--sequence`, use `--` to
separate the bare argument from the switch arguments.

### pdftools

```
usage: pdftools [-h] [-V] <command> ...

Python-based command line tool for manipulating PDFs. It is based on the
pypdf package.

optional arguments:
  -h, --help     show this help message and exit
  -V, --version  Print version number and exit (default: False)

Sub-commands:
  <command>
    add          Add pages from a source file to an output PDF file
    copy         Copy specific pages of a PDF file in a new file
    insert       Insert pages of one file into another
    merge        Merge the pages of multiple input files into one output file
    remove       Remove pages from a PDF file
    rotate       Rotate the pages of a PDF files by 90 degrees
    split        Split a PDF file into multiple documents
    zip          Python-like zipping (interleaving) the pages of two documents
                 in one output file
```

### Add

```
usage: pdftools add [-h] [-p PAGES [PAGES ...]] [-o OUTPUT] dest src

Add pages from a source file to an output PDF file

positional arguments:
  dest                  Destination PDF file
  src                   PDF source file

optional arguments:
  -h, --help            show this help message and exit
  -p PAGES [PAGES ...], --pages PAGES [PAGES ...]
                        list of pages to add to the output. Examples: 5; 1-9;
                        1-; -9 (default: None)
  -o OUTPUT, --output OUTPUT
                        Name of the output file. If None, the `dest` file will
                        be overwritten (default: None)
```

### Copy

```
usage: pdftools copy [-h] [-f] [-p PAGES [PAGES ...]] [-o OUTPUT] src

Copy specific pages of a PDF file in a new file

positional arguments:
  src                   Source PDF containing pages to copy

options:
  -h, --help            show this help message and exit
  -f, --force           Caution!! Answers "Yes" to all overwrite queries.
                        (default: False)
  -p PAGES [PAGES ...], --pages PAGES [PAGES ...]
                        list of pages to copy in the new file. Examples: "5 8
                        10": Pages 5, 8, 10; "1-9": Pages 1 to 9; "5-": Pages
                        from 5 to last page; "-9": Pages from beginning to 9
                        (default: 1)
  -o OUTPUT, --output OUTPUT
                        Name of the output file. If None, the `dest` file will
                        be overwritten (default: None)
```

### Insert

```
usage: pdftools insert [-h] [-p PAGES [PAGES ...]] [-i INDEX] [-o OUTPUT]
                       dest src

Insert pages of one file into another

positional arguments:
  dest                  Destination PDF file
  src                   Source PDF file

options:
  -h, --help            show this help message and exit
  -p PAGES [PAGES ...], --pages PAGES [PAGES ...]
                        List of page numbers (start with 1) which will be
                        inserted. If None, all pages will be inserted
                        (default). Examples: 5; 1-9; 1-; -9 (default: None)
  -i INDEX, --index INDEX
                        Page number (1-indexed) of destination file where the
                        pages will be inserted. If None they will be added at
                        the end of the file (default: None)
  -o OUTPUT, --output OUTPUT
                        Name of the output file. If None, the `dest` file will
                        be overwritten (default: None)
```

### Remove

```
usage: pdftools remove [-h] [-f] [-o OUTPUT] src pages [pages ...]

Remove pages from a PDF file

positional arguments:
  src                   PDF source file
  pages                 List of pages to remove from file. Examples: 5; 1-9;
                        1-; -9

options:
  -h, --help            show this help message and exit
  -f, --force           Caution!! Answers "Yes" to all overwrite queries.
                        (default: False)
  -o OUTPUT, --output OUTPUT
                        Name of the output file. If None, the `src` file will
                        be overwritten (default: None)
```

### Rotate

```
usage: pdftools rotate [-h] [-d {90,180,270}] [-c] [-p PAGES [PAGES ...]]
                       [-o OUTPUT]
                       src

Rotate the pages of a PDF file by a set number of degrees

positional arguments:
  src                   Source file

optional arguments:
  -h, --help            show this help message and exit
  -d {90,180,270}, --degrees {90,180,270}
                        Specify degrees value to rotate page(s) (default: 90)
  -c, --counter-clockwise
                        Rotate pages counter-clockwise instead of clockwise,
                        by default (default: False)
  -p PAGES [PAGES ...], --pages PAGES [PAGES ...]
                        List of page numbers which will be rotated. If None,
                        all pages will be rotated. Examples: 5; 1-9; 1-; -9
                        (default: None)
  -o OUTPUT, --output OUTPUT
                        Output filename. If None, the source file will be
                        overwritten (default: None)
```

### Split

```
usage: pdftools split [-h] [-s STEPSIZE] [-q SEQUENCE [SEQUENCE ...]]
                      [-o OUTPUT]
                      src

Split a PDF file into multiple documents

positional arguments:
  src                   Source file to be split

options:
  -h, --help            show this help message and exit
  -s STEPSIZE, --stepsize STEPSIZE
                        How many pages are packed in each output file
                        (default: 1)
  -q SEQUENCE [SEQUENCE ...], --sequence SEQUENCE [SEQUENCE ...]
                        Sequence of numbers describing how many pages to put
                        in each outputfile (default: None)
  -o OUTPUT, --output OUTPUT
                        Output filenames. If None, will append page numbers to
                        the input file name. (default: None)
```

### Merge

```
usage: pdftools merge [-h] [-d] [-o OUTPUT] src [src ...]

Merge the pages of multiple input files into one output file

positional arguments:
  src                   List of input source files

options:
  -h, --help            show this help message and exit
  -d, --delete          Delete source files after merge (default: False)
  -o OUTPUT, --output OUTPUT
                        Output filename (default: merged.pdf)
```

### Zip

```
usage: pdftools zip [-h] [-d] [-r] src1 src2 output

Python-like zipping (interleaving) the pages of two documents in one output
file

positional arguments:
  src1          First source file
  src2          Second source file
  output        Name of the output file

optional arguments:
  -h, --help    show this help message and exit
  -d, --delete  Delete source files after merge (default: False)
  -r, --revert  Revert the pages of second input file (default: False)
```
