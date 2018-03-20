# utl_transpose_long_to_wide_with_sequential_matching_pairs
Transpose long to wide with sequential matching pairs.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Transpose long to wide with sequential matching pairs

    github
    https://tinyurl.com/yc9j8x25
    https://github.com/rogerjdeangelis/utl_transpose_long_to_wide_with_sequential_matching_pairs

    I could not get the R code to work. Mostly due to my lack of R knowledge?

    see
    https://tinyurl.com/y8ucsj9d
    https://stackoverflow.com/questions/49390494/r-long-to-wide-with-sequential-matching-pairs

    INPUT
    =====

      SD1.HAVE total obs=32

        Obs    GRP    STR    OUT

          1     1     axy     45
          2     1     dat     76
          3     1     axy     35   * the first two axy are a pairing and need to transposed

          4     1     axy     66
          5     1     dat     55
          6     1     axy     75   * the next two axy are a second pair

      WANT

        Obs    GRP    STR    OUT1    OUT2

          1     1     axy     45      35
          2     1     axy     66      75

    PROCESS  (all the code)
    =======================

        * group the pairs;
        proc sort data=have out=havSrt noequals;
           by grp str;
        run;quit;

        * lag and potput the pair;
        data want;
          set havSrt;
          outLag=lag(out);
          if mod(_n_,2)=0 then do;
            out1=outLag;
            out2=out;
            output;
          end;
            keep grp str out1 out2;
        run;quit;

    OUTPUT
    ======

     WORK.WANT total obs=16

      GRP    STR    OUT1    OUT2

       1     axy     78      59
       1     axy     38      76

       1     bte     52      61
       1     bte     34      17

       1     cny     41      50
       1     cny     67      12

       1     dat     55      51
       1     dat     45      32

       2     axy     38      59
       2     axy     76      78
       2     bte     17      52
       2     bte     34      62
       2     cny     50      12
       2     cny     67      49
       2     dat     54      32
       2     dat     55      45

    *                _               _       _
     _ __ ___   __ _| | _____     __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|

    ;


    data have;
      input Grp  str$ out;
    cards4;
    1 dat 45
    1 axy 76
    1 dat 55
    1 bte 61
    1 cny 41
    1 bte 34
    1 cny 67
    1 dat 32
    1 axy 59
    1 cny 12
    1 dat 51
    1 cny 50
    1 bte 52
    1 axy 38
    1 bte 17
    1 axy 78
    2 dat 45
    2 axy 76
    2 dat 55
    2 bte 62
    2 cny 49
    2 bte 34
    2 cny 67
    2 dat 32
    2 axy 59
    2 cny 12
    2 dat 54
    2 cny 50
    2 bte 52
    2 axy 38
    2 bte 17
    2 axy 78
    ;;;;
    run;quit;


