read.R_code
===========

Read R code from a file.

More specifically, open and read a file in text mode assumed to be in UTF-8 encoding and assumed to contain R code.

Usage
-----

    read.R_code(file)
    
| Argument | Description                                               |
| -------: | :-------------------------------------------------------- |
|     file | a character string describing the file from which to read |

Value
-----

A data frame of three columns.
There is one row for each line in the file.

The _third_ column contains the text read.

The _first two_ columns report the results of basic tests of each line: 1)
whether it is composed only of the characters suggested by
_Writing R Extensions_ (Sect. 1.1.5)
and 2) whether condition 1 is met AND formfeed and tab are absent.
Such a line of text might be called "nice" text, since all characters are human-readable.

_Writing R Extensions_ (Sect. 1.1.5) reads, in part:
"Only ASCII characters (and the control characters tab,
formfeed, LF and CR) should be used in code files."
This is taken to mean ASCII codes 32 through 126
(the _printing_ characters), plus the four control characters explicitly named.
