read.R_code
===========

Read R code from a file.

More specifically, open and read a file in text mode assumed to be in UTF-8 encoding and assumed to contain R code.

Usage
-----

    read.R_code(file)
    
| Argument | Description |
| -------: | :---------- |
|     file | a character string describing the file from which to read |

Value
-----

A data frame of three columns.
There is one row for each line in the file.

The first two columns report the results of basic tests of each line: 1)
whether it is composed only of the characters suggested by
_Writing R Extensions_ (Sect. 1.1.5):

> Only ASCII characters (and the control characters tab,
> formfeed, LF and CR) should be used in code files.

and 2) whether condition 1 is met AND formfeed and tab are absent.

The third column contains the text read.

Example
-------

    PATH <- "~/lib/read.R_code-WORM"
    ENV <- source ( paste0 (
        PATH ,
        "/inst/extdata/R/env.read.R_code/1.R"
    ) ) [[ 1 ]] ( PATH )

    ENV $ read.R_code ( "~/R/R.R" )
