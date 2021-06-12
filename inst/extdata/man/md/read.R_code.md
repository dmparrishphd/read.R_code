read.R_code
===========

_As of 2021-06-21, the following is simply a dump of code in development._

----

    is.character.string <- function ( X )
		is.character ( X ) &&
		length ( X ) == 1

    read.utf8.lines.all <- function ( file ) {
	stopifnot (
		is.character.string ( file ) )
	scan (
		blank.lines.skip = FALSE ,
		file = file ,
		fileEncoding = "UTF-8" ,
		na.strings = character () ,
		sep = "\n" ,
		skipNul = FALSE ,
		quiet = TRUE ,
		what = "" ) }

    UTF32.CTRL.RCODE <- utf8ToInt ( "\t\f\n\r" )

    #"Only ASCII characters (and the control characters tab, formfeed, LF and CR) should be used
    #in code files." (Writing R Extensions, Sect. 1.1.5)

    in.R_code.charSet.str <- function ( string ) {
	    u <- utf8ToInt ( string )
	all ( 32L <= u & u <= 126L | u %in% UTF32.CTRL.RCODE ) }

    in.R_code.charSet.h <- function ( .character ) vapply (
	X = .character ,
	FUN.VALUE = NA ,
	USE.NAMES = FALSE ,
	FUN = in.R_code.charSet.str )

    .harmless <- function ( string , replacement ) {
	UTF32 <- utf8ToInt ( string )
	intToUtf8 ( replace (
		UTF32 ,
		which ( 126 < UTF32 | UTF32 < 32 ) ,
		utf8ToInt ( replacement ) ) ) }

    harmless <- function ( .character , replacement = "?" )
		vapply (
			X = .character ,
			FUN.VALUE = "" ,
			FUN = .harmless ,
			USE.NAMES = FALSE ,
			replacement = replacement )

    read.R_code <- function ( file ) {
	LINES <- read.utf8.lines.all ( file )
	data.frame (
		stringsAsFactors = FALSE ,
		row.names = as.character ( seq_along ( LINES ) ) ,
		OK = in.R_code.charSet.h ( LINES ) ,
		LINE = LINES ) }

    # "All R platforms support... "UTF-8"" (help(iconv)).

    # If file is a character string and fileEncoding is non-default...
    # the text is converted to UTF-8 and declared as such
    # (and the encoding argument to scan is ignored)" (help(scan)).

    con=file("T:/trash",open="wb")
    writeBin(con=con,as.raw(c(1:9,11:12,14:25,27:127,13,10,1:9,13,10)))
    #writeBin(con=con,as.raw(utf8ToInt("foo<-42")))
    close(con)
    read.R_code("T:/trash")
