read.R_code package
===================

Read R source code files.

Example
-------

    # TERSE EXAMPLE---MODIFIES SEARCH PATH
    attach (
        name = "protopkg:read.R_code" ,
        what = source ( paste0 (
            "~/read.R_code-WORM" ,
            "/inst/extdata/R/env.read.R_code/1.R" )
            ) [[ 1 ]] ( "~/read.R_code-WORM" ) )
    read.R_code ( "~/R/R.R" )

    # VERBOSE EXAMPLE
    #
    # DEFINE PATH TO THE PACKAGE
    PATH <- "~/lib/read.R_code-WORM"
    # DEFINE PATH TO CODE FOR DEFINING THE "read.R_code" ENVIRONMENT
    SOURCE <- paste0 ( PATH ,
        "/inst/extdata/R/env.read.R_code/1.R" )
    # SOURCE THE CODE FOR DEFINING THE "read.R_code" ENVIRONMENT
    env.read.R_code <- source ( SOURCE ) [[ 1 ]]
    # CALL THE CODE FOR DEFINING THE "read.R_code" ENVIRONMENT,
    # THUS DEFINING read.R_codeEnv
    read.R_codeEnv <- env.read.R_code ( PATH )
    # CALL THE read.R_code FUNCTION TO READ AN R CODE FILE
    read.R_codeEnv $ read.R_code ( "~/R/R.R" )
