# utl-creating-a-clinical-n-mean-stddev-median-min-max-sas-dataset-from-proc-tabulate
Creating a clinical n mean stddev median min max sas dataset from proc tabulate
    %let pgm=utl-creating-a-clinical-n-mean-stddev-median-min-max-sas-dataset-from-proc-tabulate;

    Creating a clinical n mean stddev median min max sas dataset from proc tabulate

    This creates a table in addition to the tabulate listing

    github
    https://tinyurl.com/2bneptda
    https://github.com/rogerjdeangelis/utl-creating-a-clinical-n-mean-stddev-median-min-max-sas-dataset-from-proc-tabulate

    Macro on end

    You may need to tweak the macro for complex tabulates.
    As soon as the printed tabulate looks like a retangular table, run the macro.
    The number of bars is the primary filter.

    Related repos
    https://github.com/rogerjdeangelis?tab=repositories&q=tabul&type=&language=&sort=

    DO NOT USE VARIABLE NAMES IN THE TITLE THAT BEGIN WITH VAR;

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options formchar='|----|+|---+=|-/\<>*';
    proc tabulate data=sashelp.class;class sex ;
      * do not use variable names that begin with var;
      title "|hdr|stat|f|m|";
    var height weight;table weight*(n mean stddev median min max ) height*(n mean stddev median min max
     ),sex=""/rts=44  ; /* box has to wide enought so thta there is not folding */
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* ----------------------------------------------------------------------                                                 */
    /* |                                          |     F      |     M      |                                                 */
    /* |------------------------------------------+------------+------------|                                                 */
    /* |WEIGHT              |N                    |        9.00|       10.00|                                                 */
    /* |                    |---------------------+------------+------------|                                                 */
    /* |                    |Mean                 |       90.11|      108.95|                                                 */
    /* |                    |---------------------+------------+------------|                                                 */
    /* |                    |StdDev               |       19.38|       22.73|                                                 */
    /* |                    |---------------------+------------+------------|                                                 */
    /* |                    |Median               |       90.00|      107.25|                                                 */
    /* |                    |---------------------+------------+------------|                                                 */
    /* |                    |Min                  |       50.50|       83.00|                                                 */
    /* |                    |---------------------+------------+------------|                                                 */
    /* |                    |Max                  |      112.50|      150.00|                                                 */
    /* |--------------------+---------------------+------------+------------|                                                 */
    /* |HEIGHT              |N                    |        9.00|       10.00|                                                 */
    /* |                    |---------------------+------------+------------|                                                 */
    /* |                    |Mean                 |       60.59|       63.91|                                                 */
    /* |                    |---------------------+------------+------------|                                                 */
    /* |                    |StdDev               |        5.02|        4.94|                                                 */
    /* |                    |---------------------+------------+------------|                                                 */
    /* |                    |Median               |       62.50|       64.15|                                                 */
    /* |                    |---------------------+------------+------------|                                                 */
    /* |                    |Min                  |       51.30|       57.30|                                                 */
    /* |                    |---------------------+------------+------------|                                                 */
    /* |                    |Max                  |       66.50|       72.00|                                                 */
    /* ----------------------------------------------------------------------                                                 */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

     /**************************************************************************************************************************/
     /*                                                                                                                        */
     /* p to 40 obs from WANT_ODSRPT total obs=12 22MAY2022:15:54:33                                                           */
     /*                                                                                                                        */
     /* bs     HDR      STAT         F         M                                                                               */
     /*                                                                                                                        */
     /*  1    WEIGHT    N           9.00     10.00                                                                             */
     /*  2              Mean       90.11    108.95                                                                             */
     /*  3              StdDev     19.38     22.73                                                                             */
     /*  4              Median     90.00    107.25                                                                             */
     /*  5              Min        50.50     83.00                                                                             */
     /*  6              Max       112.50    150.00                                                                             */
     /*  7    HEIGHT    N           9.00     10.00                                                                             */
     /*  8              Mean       60.59     63.91                                                                             */
     /*  9              StdDev      5.02      4.94                                                                             */
     /* 10              Median     62.50     64.15                                                                             */
     /* 11              Min        51.30     57.30                                                                             */
     /* 12              Max        66.50     72.00                                                                             */
     /*                                                                                                                        */
     /*             Variables in Creation Order                                                                                */
     /*                                                                                                                        */
     /* #    Variable    Type    Len                                                                                           */
     /*                                                                                                                        */
     /* 1    HDR         Char      6                                                                                           */
     /* 2    STAT        Char      6                                                                                           */
     /* 3    F           Num       8   Note Numeric                                                                            */
     /* 4    M           Num       8                                                                                           */
     /*                                                                                                                        */
     /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    %utl_odstbu(setup);

    options formchar='|----|+|---+=|-/\<>*';
    proc tabulate data=sashelp.class;class sex ;
      * do not use variable names that begin with var;
      title "|hdr|stat|f|m|";
    var height weight;
    table weight*(n mean stddev median min max )
          height*(n mean stddev median min max ),sex=""
             /rts=44  ; /* box has to wide enought so thta there is not wrapping */
    run;quit;

    %utl_odstbu(outdsn=want_odsrpt,bars=5);



    %macro utl_odstbu(outdsn,bars=5,firstobs=2);

       %if %qupcase(&outdsn)=SETUP %then %do;

            filename _tmp1_ clear;  * just in case;

            %utlfkil(%sysfunc(pathname(work))/_tmp1_.txt);

            filename _tmp1_ "%sysfunc(pathname(work))/_tmp1_.txt";

            %let _ps_= %sysfunc(getoption(ps));
            %let _fc_= %sysfunc(getoption(formchar));

            OPTIONS ls=max ps=32756  FORMCHAR='|'  nodate nocenter;

            title; footnote;

            proc printto print=_tmp1_;
            run;quit;

       %end;
       %else %do;

            /* %let outdsn=tst; %let datarow=3; */

            proc printto;
            run;quit;

            %utlfkil(%sysfunc(pathname(work))/_tmp2_.txt);

            *filename _tmp2_  "%sysfunc(pathname(work))/_tmp2_.txt";

            proc datasets lib=work nolist;  *just in case;
             delete &outdsn;
            run;quit;

            proc printto print="%sysfunc(pathname(work))/_tmp2_.txt";
            run;quit;

            data _null_;
              retain n 0;
              infile _tmp1_ length=l firstobs=&firstobs;
              input lyn $varying32756. l;
              file print titles;
              if countc(lyn,'|')=&bars then do;
                  putlog lyn;
                  put lyn;
              end;
            run;quit;

            proc printto;
            run;quit;

            proc import
               datafile="%sysfunc(pathname(work))/_tmp2_.txt"
               dbms=dlm
               out=&outdsn(drop=var:)
               replace;
               delimiter='|';
               getnames=yes;
            run;quit;

            filename _tmp1_ clear;
            filename _tmp2_ clear;

            * turn off for production;
            %*utlfkil(%sysfunc(pathname(work))/_tmp1_.txt);
            %*utlfkil(%sysfunc(pathname(work))/_tmp2_.txt);

            proc datasets lib = work nodetails nolist;
              modify &outdsn ;
                attrib _all_ label = "" ;
                format _all_;
                informat _all_;
              run ;
            quit ;
       %end;

    %mend utl_odstbu;

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
