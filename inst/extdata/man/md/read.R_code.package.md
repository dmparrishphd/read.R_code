
Example
-------

    PATH <- "~/lib/read.R_code-WORM"
    ENV <- source ( paste0 (
        PATH ,
        "/inst/extdata/R/env.read.R_code/1.R"
    ) ) [[ 1 ]] ( PATH )

    ENV $ read.R_code ( "~/R/R.R" )
