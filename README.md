# utl-transpose-pairs-of-dates-by-groups-or-transposing-mutiple-variables
Transpose pairs of dates by groups or transposing mutiple variables
    Transpose pairs of dates by groups or transposing mutiple variables

    github
    https://tinyurl.com/y55yhwol
    https://github.com/rogerjdeangelis/utl-transpose-pairs-of-dates-by-groups-or-transposing-mutiple-variables

    SAS Forum
    https://tinyurl.com/y2adw5bx
    https://communities.sas.com/t5/SAS-Enterprise-Guide/Transpose-multiple-variable-columns/m-p/558261

    macros
    https://tinyurl.com/y9nfugth
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories

    utl_transpose by
    AUTHORS: Arthur Tabachneck, Xia Ke Shan, Robert Virgile and Joe Whitehurst

    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    data have ;

      input code name$ type$  num fro to;
      informat fro to date9.;
      format fro to date9.;
      type=cats(type,num);

    cards4;
    10 RAD ANNUAL 1 1JAN2019 01JAN2019
    10 RAD ANNUAL 2 7JAN2019 10JAN2019
    10 RAD ANNUAL 3 12JAN2019 13JAN2019
    15 CAD ANNUAL 1 15JAN2019 18JAN2019
    15 CAD ANNUAL 2 20JAN2019 22JAN2019
    20 SAD ANNUAL 1 25JAN2019 27JAN2019
    20 SAD ANNUAL 2 28JAN2019 30JAN2019
    ;;;;
    run;quit;


    HAVE total obs=7                                                 | RULES
                                                                     |
    Obs    CODE    NAME     TYPE      NUM       FRO          TO      | CODE NAME FROANNUAL1 TOANNUAL1 FROANNUAL2 TOANNUAL2 FROANNUAL3 TOANNUAL3
                                                                     |
     1      10     RAD     ANNUAL1     1     01JAN2019    01JAN2019  |  10  RAD  01JAN2019 01JAN2019 07JAN2019 10JAN2019 12JAN2019  13JAN2019
     2      10     RAD     ANNUAL2     2     07JAN2019    10JAN2019  |
     3      10     RAD     ANNUAL3     3     12JAN2019    13JAN2019  |

     4      15     CAD     ANNUAL1     1     15JAN2019    18JAN2019  |  15  CAD  15JAN2019 18JAN2019 20JAN2019 22JAN2019     .          .
     5      15     CAD     ANNUAL2     2     20JAN2019    22JAN2019  |

     6      20     SAD     ANNUAL1     1     25JAN2019    27JAN2019  |  ..
     7      20     SAD     ANNUAL2     2     28JAN2019    30JAN2019  |

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;
    WANT total obs=3

    Obs    CODE    NAME    FROANNUAL1    TOANNUAL1    FROANNUAL2    TOANNUAL2    FROANNUAL3    TOANNUAL3

     1      10     RAD     01JAN2019     01JAN2019    07JAN2019     10JAN2019    12JAN2019     13JAN2019
     2      15     CAD     15JAN2019     18JAN2019    20JAN2019     22JAN2019            .             .
     3      20     SAD     25JAN2019     27JAN2019    28JAN2019     30JAN2019            .             .


    *
     _ __  _ __ ___   ___ ___  ___ ___
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    ;

    %utl_transpose(data=have, out=want, by=code name , id=type, guessingrows=1000,var=fro to);


