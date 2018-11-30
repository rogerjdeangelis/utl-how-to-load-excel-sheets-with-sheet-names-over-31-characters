# utl-how-to-load-excel-sheets-with-sheet-names-over-31-characters
How to load excel sheets with sheet names over 31 characters
    How to load excel sheets with sheet names over 31 characters

    I think you need R or Python for this.

    I copied the ops excel file to d:/xls and github

    github
    https://tinyurl.com/y9lhw237
    https://github.com/rogerjdeangelis/utl-how-to-load-excel-sheets-with-sheet-names-over-31-characters

    SAS Forum
    https://tinyurl.com/ycclym3k
    https://communities.sas.com/t5/New-SAS-User/How-to-get-pcfiles-libname-engine-to-recognize-long-Excel-sheet/m-p/516148


    INPUT
    =====

       github
       https://tinyurl.com/y949wux7

       d:/xls/utl-how-to-get-pcfiles-libname-engine-to-recognize-long-excel-sheet-namesx.xls


       +---------------------+
       |     A               |
       +---------------------+
    1  |   TEST              |
       +---------------------+
    2  |  SIX TESTS     H    |
       +---------------------+

     [test test test test test test]  ==> note sheet name longer than 31 characters


    EXAMPLE OUTPUT
    --------------

    Macro variable shhets with sheet names

     Sheets =  "test test test test test test"   "test test test test test test t"


    WORK.WANT total obs=1

    Obs      TEST

     1     six tests


    PROCESS
    =======

    %symdel sheets / nowarn;
    %utl_submit_r64('
       library("XLConnect");
       library("SASxport");
       wb <- loadWorkbook("d:/xls/utl-how-to-get-pcfiles-libname-engine-to-recognize-long-excel-sheet-namesx.xls");
       sheets<-getSheets(wb);
       sheets;
       want <- readWorksheet(wb, sheet = "test test test test test test");
       writeClipboard(as.character(paste(sheets, collapse = " ")));
       write.xport(want,file="d:/xpt/want.xpt");
    ',returnVar=sheets)

     %put &=sheets;


    OUTPUT
    ======

    see above

    LOG
    ---

    > library("XLConnect");
    > library("SASxport");
    > wb <- loadWorkbook("d:/xls/utl-how-to-get-pcfiles-libname-engine-to-recognize-long-excel-sheet-namesx.xls");
    > sheets<-getSheets(wb);
    > sheets;
    > want <- readWorksheet(wb, sheet = "test test test test test test");
    > writeClipboard(as.character(paste(sheets, collapse = " ")));
    > write.xport(want,file="d:/xpt/want.xpt");

    [1] "test test test test test test"   "test test test test test test t"
    >

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

      github
      https://tinyurl.com/y949wux7




