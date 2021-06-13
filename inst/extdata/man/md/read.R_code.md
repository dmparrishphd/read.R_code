read.R_code
===========

as stated in Writing R Extensions (Sect. 1.1.5):

> Only ASCII characters (and the control characters tab,
> formfeed, LF and CR) should be used in code files.

Example
-------

    PATH <- "~/lib/read.R_code-WORM"
    ENV <- source ( paste0 (
        PATH ,
        "/inst/extdata/R/env.read.R_code/1.R"
    ) ) [[ 1 ]] ( PATH )

    ENV $ read.R_code ( "~/R/R.R" )
