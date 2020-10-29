# Violet Parser Generator

Simple LALR parser generator written in C#

## Test

### Json Parser

Check https://github.com/xxx1720 repositories.

### Parser Generation

```
==================================================

                 PRODUCTION RULES

==================================================
   1:         S' -> script
   2:     script -> block
   3:       line -> stmt
   4:       stmt -> function
   5:       stmt -> index = index
   6:       stmt -> runnable
   7:      block -> [ block ]
   8:      block -> line block
   9:      block ->
  10:     consts -> number
  11:     consts -> string
  12:      index -> variable
  13:      index -> variable [ variable ]
  14:   variable -> name
  15:   variable -> function
  16:   variable -> consts
  17:   argument -> index
  18:   argument -> index , argument
  19:   function -> name ( )
  20:   function -> name ( argument )
  21:   runnable -> loop ( name = index to index ) block
  22:   runnable -> foreach ( name : index ) block
  23:   runnable -> if ( index ) block
  24:   runnable -> if ( index ) block else block

==================================================

                FISRT, FOLLOW SETS

==================================================
FIRST(S')={[,name,loop,foreach,if,number,string}
FIRST(script)={[,name,loop,foreach,if,number,string}
FIRST(line)={name,loop,foreach,if,number,string}
FIRST(stmt)={name,loop,foreach,if,number,string}
FIRST(block)={[,name,loop,foreach,if,number,string}
FIRST(consts)={number,string}
FIRST(index)={name,number,string}
FIRST(variable)={name,number,string}
FIRST(argument)={name,number,string}
FIRST(function)={name}
FIRST(runnable)={loop,foreach,if}
FIRST(=)={=}
FIRST([)={[}
FIRST(])={]}
FIRST(number)={number}
FIRST(string)={string}
FIRST(name)={name}
FIRST(,)={,}
FIRST(()={(}
FIRST())={)}
FIRST(loop)={loop}
FIRST(to)={to}
FIRST(foreach)={foreach}
FIRST(:)={:}
FIRST(if)={if}
FIRST(else)={else}
FOLLOW(S')={$}
FOLLOW(script)={$}
FOLLOW(line)={[,name,loop,foreach,if,number,string}
FOLLOW(stmt)={[,name,loop,foreach,if,number,string}
FOLLOW(block)={],else,$,[,name,loop,foreach,if,number,string}
FOLLOW(consts)={[,],=,,,to,),name,loop,foreach,if,number,string}
FOLLOW(index)={=,,,to,),[,name,loop,foreach,if,number,string}
FOLLOW(variable)={[,],=,,,to,),name,loop,foreach,if,number,string}
FOLLOW(argument)={)}
FOLLOW(function)={[,name,loop,foreach,if,number,string,],=,,,to,)}
FOLLOW(runnable)={[,name,loop,foreach,if,number,string}
FOLLOW(name)={(,=,:}
FOLLOW(()={),name}
FOLLOW(loop)={(}
FOLLOW(foreach)={(}
FOLLOW(if)={(}

==================================================

                   LALR STATES

==================================================
-----I0-----
        S' -> ·script                       $
    script -> ·block                        $
     block -> ·[ block ]                    $
     block -> ·line block                   $
     block ->                               $
      line -> ·stmt                         $/[/name/loop/foreach/if/number/string
      stmt -> ·function                     $/[/name/loop/foreach/if/number/string
      stmt -> ·index = index                $/[/name/loop/foreach/if/number/string
      stmt -> ·runnable                     $/[/name/loop/foreach/if/number/string
  function -> ·name ( )                     $/[/name/loop/foreach/if/number/string/=
  function -> ·name ( argument )            $/[/name/loop/foreach/if/number/string/=
     index -> ·variable                     $/[/name/loop/foreach/if/number/string/=
     index -> ·variable [ variable ]        $/[/name/loop/foreach/if/number/string/=
  runnable -> ·loop ( name = index to index ) block $/[/name/loop/foreach/if/number/string
  runnable -> ·foreach ( name : index ) block $/[/name/loop/foreach/if/number/string
  runnable -> ·if ( index ) block           $/[/name/loop/foreach/if/number/string
  runnable -> ·if ( index ) block else block $/[/name/loop/foreach/if/number/string
  variable -> ·name                         $/[/name/loop/foreach/if/number/string/=
  variable -> ·function                     $/[/name/loop/foreach/if/number/string/=
  variable -> ·consts                       $/[/name/loop/foreach/if/number/string/=
    consts -> ·number                       $/[/name/loop/foreach/if/number/string/=
    consts -> ·string                       $/[/name/loop/foreach/if/number/string/=
-----I1-----
        S' -> script ·                      $
-----I2-----
    script -> block ·                       $
-----I3-----
     block -> [ ·block ]                    ]/$/[/name/loop/foreach/if/number/string/else
     block -> ·[ block ]                    ]
     block -> ·line block                   ]
     block ->                               ]
      line -> ·stmt                         [/name/loop/foreach/if/number/string/]
      stmt -> ·function                     [/name/loop/foreach/if/number/string/]
      stmt -> ·index = index                [/name/loop/foreach/if/number/string/]
      stmt -> ·runnable                     [/name/loop/foreach/if/number/string/]
  function -> ·name ( )                     [/name/loop/foreach/if/number/string/]/=
  function -> ·name ( argument )            [/name/loop/foreach/if/number/string/]/=
     index -> ·variable                     [/name/loop/foreach/if/number/string/]/=
     index -> ·variable [ variable ]        [/name/loop/foreach/if/number/string/]/=
  runnable -> ·loop ( name = index to index ) block [/name/loop/foreach/if/number/string/]
  runnable -> ·foreach ( name : index ) block [/name/loop/foreach/if/number/string/]
  runnable -> ·if ( index ) block           [/name/loop/foreach/if/number/string/]
  runnable -> ·if ( index ) block else block [/name/loop/foreach/if/number/string/]
  variable -> ·name                         [/name/loop/foreach/if/number/string/]/=
  variable -> ·function                     [/name/loop/foreach/if/number/string/]/=
  variable -> ·consts                       [/name/loop/foreach/if/number/string/]/=
    consts -> ·number                       [/name/loop/foreach/if/number/string/]/=
    consts -> ·string                       [/name/loop/foreach/if/number/string/]/=
-----I4-----
     block -> line ·block                   $/]/[/name/loop/foreach/if/number/string/else
     block -> ·[ block ]                    $/]/[/name/loop/foreach/if/number/string/else
     block -> ·line block                   $/]/[/name/loop/foreach/if/number/string/else
     block ->                               $/]/[/name/loop/foreach/if/number/string/else
      line -> ·stmt                         [/name/loop/foreach/if/number/string/$/]/else
      stmt -> ·function                     [/name/loop/foreach/if/number/string/$/]/else
      stmt -> ·index = index                [/name/loop/foreach/if/number/string/$/]/else
      stmt -> ·runnable                     [/name/loop/foreach/if/number/string/$/]/else
  function -> ·name ( )                     [/name/loop/foreach/if/number/string/=/$/]/else
  function -> ·name ( argument )            [/name/loop/foreach/if/number/string/=/$/]/else
     index -> ·variable                     [/name/loop/foreach/if/number/string/=/$/]/else
     index -> ·variable [ variable ]        [/name/loop/foreach/if/number/string/=/$/]/else
  runnable -> ·loop ( name = index to index ) block [/name/loop/foreach/if/number/string/$/]/else
  runnable -> ·foreach ( name : index ) block [/name/loop/foreach/if/number/string/$/]/else
  runnable -> ·if ( index ) block           [/name/loop/foreach/if/number/string/$/]/else
  runnable -> ·if ( index ) block else block [/name/loop/foreach/if/number/string/$/]/else
  variable -> ·name                         [/name/loop/foreach/if/number/string/=/$/]/else
  variable -> ·function                     [/name/loop/foreach/if/number/string/=/$/]/else
  variable -> ·consts                       [/name/loop/foreach/if/number/string/=/$/]/else
    consts -> ·number                       [/name/loop/foreach/if/number/string/=/$/]/else
    consts -> ·string                       [/name/loop/foreach/if/number/string/=/$/]/else
-----I5-----
      line -> stmt ·                        [/name/loop/foreach/if/number/string/$/]/else
-----I6-----
      stmt -> function ·                    $/[/name/loop/foreach/if/number/string/]/else
  variable -> function ·                    $/[/name/loop/foreach/if/number/string/]/=/else
-----I7-----
      stmt -> index ·= index                $/[/name/loop/foreach/if/number/string/]/else
-----I8-----
      stmt -> runnable ·                    $/[/name/loop/foreach/if/number/string/]/else
-----I9-----
  function -> name ·( )                     $/[/name/loop/foreach/if/number/string/=/]/else/,/)/to
  function -> name ·( argument )            $/[/name/loop/foreach/if/number/string/=/]/else/,/)/to
  variable -> name ·                        $/[/name/loop/foreach/if/number/string/]/=/else/,/)/to
-----I10-----
     index -> variable ·                    =/,/)/to/$/[/name/loop/foreach/if/number/string/]/else
     index -> variable ·[ variable ]        =/$/[/name/loop/foreach/if/number/string/]/else/,/)/to
-----I11-----
  runnable -> loop ·( name = index to index ) block $/[/name/loop/foreach/if/number/string/]/else
-----I12-----
  runnable -> foreach ·( name : index ) block $/[/name/loop/foreach/if/number/string/]/else
-----I13-----
  runnable -> if ·( index ) block           $/[/name/loop/foreach/if/number/string/]/else
  runnable -> if ·( index ) block else block $/[/name/loop/foreach/if/number/string/]/else
-----I14-----
  variable -> consts ·                      $/[/name/loop/foreach/if/number/string/=/]/,/)/to/else
-----I15-----
    consts -> number ·                      $/[/name/loop/foreach/if/number/string/=/]/,/)/to/else
-----I16-----
    consts -> string ·                      $/[/name/loop/foreach/if/number/string/=/]/,/)/to/else
-----I17-----
     block -> [ block ·]                    $/]/[/name/loop/foreach/if/number/string/else
-----I18-----
     block -> line block ·                  $/]/[/name/loop/foreach/if/number/string/else
-----I19-----
      stmt -> index = ·index                $/[/name/loop/foreach/if/number/string/]/else
     index -> ·variable                     $/[/name/loop/foreach/if/number/string/]/else
     index -> ·variable [ variable ]        $/[/name/loop/foreach/if/number/string/]/else
  variable -> ·name                         [/$/name/loop/foreach/if/number/string/]/else
  variable -> ·function                     [/$/name/loop/foreach/if/number/string/]/else
  variable -> ·consts                       [/$/name/loop/foreach/if/number/string/]/else
  function -> ·name ( )                     [/$/name/loop/foreach/if/number/string/]/else
  function -> ·name ( argument )            [/$/name/loop/foreach/if/number/string/]/else
    consts -> ·number                       [/$/name/loop/foreach/if/number/string/]/else
    consts -> ·string                       [/$/name/loop/foreach/if/number/string/]/else
-----I20-----
  function -> name ( ·)                     ,/[/$/name/loop/foreach/if/number/string/=/]/else/)/to
  function -> name ( ·argument )            ,/[/)/$/name/loop/foreach/if/number/string/=/]/else/to
  argument -> ·index                        ,/[/)
  argument -> ·index , argument             ,/[/)
     index -> ·variable                     ,/[/)
     index -> ·variable [ variable ]        ,/[/)
  variable -> ·name                         ,/[/)
  variable -> ·function                     ,/[/)
  variable -> ·consts                       ,/[/)
  function -> ·name ( )                     ,/[/)
  function -> ·name ( argument )            ,/[/)
    consts -> ·number                       ,/[/)
    consts -> ·string                       ,/[/)
-----I21-----
     index -> variable [ ·variable ]        =/$/[/name/loop/foreach/if/number/string/]/else/,/)/to
  variable -> ·name                         ]
  variable -> ·function                     ]
  variable -> ·consts                       ]
  function -> ·name ( )                     ]
  function -> ·name ( argument )            ]
    consts -> ·number                       ]
    consts -> ·string                       ]
-----I22-----
  runnable -> loop ( ·name = index to index ) block $/[/name/loop/foreach/if/number/string/]/else
-----I23-----
  runnable -> foreach ( ·name : index ) block $/[/name/loop/foreach/if/number/string/]/else
-----I24-----
  runnable -> if ( ·index ) block           $/[/name/loop/foreach/if/number/string/]/else
  runnable -> if ( ·index ) block else block $/[/name/loop/foreach/if/number/string/]/else
     index -> ·variable                     )
     index -> ·variable [ variable ]        )
  variable -> ·name                         )/[
  variable -> ·function                     )/[
  variable -> ·consts                       )/[
  function -> ·name ( )                     )/[
  function -> ·name ( argument )            )/[
    consts -> ·number                       )/[
    consts -> ·string                       )/[
-----I25-----
     block -> [ block ] ·                   $/]/[/name/loop/foreach/if/number/string/else
-----I26-----
      stmt -> index = index ·               $/[/name/loop/foreach/if/number/string/]/else
-----I27-----
  variable -> function ·                    $/[/name/loop/foreach/if/number/string/]/else/,/)/to
-----I28-----
  function -> name ( ) ·                    $/[/name/loop/foreach/if/number/string/=/]/else/,/)/to
-----I29-----
  function -> name ( argument ·)            $/[/name/loop/foreach/if/number/string/=/]/else/,/)/to
-----I30-----
  argument -> index ·                       )
  argument -> index ·, argument             )
-----I31-----
     index -> variable [ variable ·]        =/$/[/name/loop/foreach/if/number/string/]/else/,/)/to
-----I32-----
  runnable -> loop ( name ·= index to index ) block $/[/name/loop/foreach/if/number/string/]/else
-----I33-----
  runnable -> foreach ( name ·: index ) block $/[/name/loop/foreach/if/number/string/]/else
-----I34-----
  runnable -> if ( index ·) block           $/[/name/loop/foreach/if/number/string/]/else
  runnable -> if ( index ·) block else block $/[/name/loop/foreach/if/number/string/]/else
-----I35-----
  function -> name ( argument ) ·           $/[/name/loop/foreach/if/number/string/=/]/else/,/)/to
-----I36-----
  argument -> index , ·argument             )
  argument -> ·index                        )
  argument -> ·index , argument             )
     index -> ·variable                     ,/)
     index -> ·variable [ variable ]        ,/)
  variable -> ·name                         ,/[/)
  variable -> ·function                     ,/[/)
  variable -> ·consts                       ,/[/)
  function -> ·name ( )                     ,/[/)
  function -> ·name ( argument )            ,/[/)
    consts -> ·number                       ,/[/)
    consts -> ·string                       ,/[/)
-----I37-----
     index -> variable [ variable ] ·       =/$/[/name/loop/foreach/if/number/string/]/else/,/)/to
-----I38-----
  runnable -> loop ( name = ·index to index ) block $/[/name/loop/foreach/if/number/string/]/else
     index -> ·variable                     to
     index -> ·variable [ variable ]        to
  variable -> ·name                         to/[
  variable -> ·function                     to/[
  variable -> ·consts                       to/[
  function -> ·name ( )                     to/[
  function -> ·name ( argument )            to/[
    consts -> ·number                       to/[
    consts -> ·string                       to/[
-----I39-----
  runnable -> foreach ( name : ·index ) block $/[/name/loop/foreach/if/number/string/]/else
     index -> ·variable                     )
     index -> ·variable [ variable ]        )
  variable -> ·name                         )/[
  variable -> ·function                     )/[
  variable -> ·consts                       )/[
  function -> ·name ( )                     )/[
  function -> ·name ( argument )            )/[
    consts -> ·number                       )/[
    consts -> ·string                       )/[
-----I40-----
  runnable -> if ( index ) ·block           [/name/loop/foreach/if/number/string/else/$/]
  runnable -> if ( index ) ·block else block [/name/loop/foreach/if/number/string/else/$/]
     block -> ·[ block ]                    [/name/loop/foreach/if/number/string/else/$/]
     block -> ·line block                   [/name/loop/foreach/if/number/string/else/$/]
     block ->                               [/name/loop/foreach/if/number/string/else/$/]
      line -> ·stmt                         [/name/loop/foreach/if/number/string/else/$/]
      stmt -> ·function                     [/name/loop/foreach/if/number/string/else/$/]
      stmt -> ·index = index                [/name/loop/foreach/if/number/string/else/$/]
      stmt -> ·runnable                     [/name/loop/foreach/if/number/string/else/$/]
  function -> ·name ( )                     [/name/loop/foreach/if/number/string/=/else/$/]
  function -> ·name ( argument )            [/name/loop/foreach/if/number/string/=/else/$/]
     index -> ·variable                     [/name/loop/foreach/if/number/string/=/else/$/]
     index -> ·variable [ variable ]        [/name/loop/foreach/if/number/string/=/else/$/]
  runnable -> ·loop ( name = index to index ) block [/name/loop/foreach/if/number/string/else/$/]
  runnable -> ·foreach ( name : index ) block [/name/loop/foreach/if/number/string/else/$/]
  runnable -> ·if ( index ) block           [/name/loop/foreach/if/number/string/else/$/]
  runnable -> ·if ( index ) block else block [/name/loop/foreach/if/number/string/else/$/]
  variable -> ·name                         [/name/loop/foreach/if/number/string/=/else/$/]
  variable -> ·function                     [/name/loop/foreach/if/number/string/=/else/$/]
  variable -> ·consts                       [/name/loop/foreach/if/number/string/=/else/$/]
    consts -> ·number                       [/name/loop/foreach/if/number/string/=/else/$/]
    consts -> ·string                       [/name/loop/foreach/if/number/string/=/else/$/]
-----I41-----
  argument -> index , argument ·            )
-----I42-----
  runnable -> loop ( name = index ·to index ) block $/[/name/loop/foreach/if/number/string/]/else
-----I43-----
  runnable -> foreach ( name : index ·) block $/[/name/loop/foreach/if/number/string/]/else
-----I44-----
  runnable -> if ( index ) block ·          $/[/name/loop/foreach/if/number/string/]/else
  runnable -> if ( index ) block ·else block $/[/name/loop/foreach/if/number/string/]/else
-----I45-----
  runnable -> loop ( name = index to ·index ) block $/[/name/loop/foreach/if/number/string/]/else
     index -> ·variable                     )
     index -> ·variable [ variable ]        )
  variable -> ·name                         )/[
  variable -> ·function                     )/[
  variable -> ·consts                       )/[
  function -> ·name ( )                     )/[
  function -> ·name ( argument )            )/[
    consts -> ·number                       )/[
    consts -> ·string                       )/[
-----I46-----
  runnable -> foreach ( name : index ) ·block [/name/loop/foreach/if/number/string/$/]/else
     block -> ·[ block ]                    [/name/loop/foreach/if/number/string/$/]/else
     block -> ·line block                   [/name/loop/foreach/if/number/string/$/]/else
     block ->                               [/name/loop/foreach/if/number/string/$/]/else
      line -> ·stmt                         [/name/loop/foreach/if/number/string/$/]/else
      stmt -> ·function                     [/name/loop/foreach/if/number/string/$/]/else
      stmt -> ·index = index                [/name/loop/foreach/if/number/string/$/]/else
      stmt -> ·runnable                     [/name/loop/foreach/if/number/string/$/]/else
  function -> ·name ( )                     [/name/loop/foreach/if/number/string/=/$/]/else
  function -> ·name ( argument )            [/name/loop/foreach/if/number/string/=/$/]/else
     index -> ·variable                     [/name/loop/foreach/if/number/string/=/$/]/else
     index -> ·variable [ variable ]        [/name/loop/foreach/if/number/string/=/$/]/else
  runnable -> ·loop ( name = index to index ) block [/name/loop/foreach/if/number/string/$/]/else
  runnable -> ·foreach ( name : index ) block [/name/loop/foreach/if/number/string/$/]/else
  runnable -> ·if ( index ) block           [/name/loop/foreach/if/number/string/$/]/else
  runnable -> ·if ( index ) block else block [/name/loop/foreach/if/number/string/$/]/else
  variable -> ·name                         [/name/loop/foreach/if/number/string/=/$/]/else
  variable -> ·function                     [/name/loop/foreach/if/number/string/=/$/]/else
  variable -> ·consts                       [/name/loop/foreach/if/number/string/=/$/]/else
    consts -> ·number                       [/name/loop/foreach/if/number/string/=/$/]/else
    consts -> ·string                       [/name/loop/foreach/if/number/string/=/$/]/else
-----I47-----
  runnable -> if ( index ) block else ·block [/name/loop/foreach/if/number/string/$/]/else
     block -> ·[ block ]                    [/name/loop/foreach/if/number/string/$/]/else
     block -> ·line block                   [/name/loop/foreach/if/number/string/$/]/else
     block ->                               [/name/loop/foreach/if/number/string/$/]/else
      line -> ·stmt                         [/name/loop/foreach/if/number/string/$/]/else
      stmt -> ·function                     [/name/loop/foreach/if/number/string/$/]/else
      stmt -> ·index = index                [/name/loop/foreach/if/number/string/$/]/else
      stmt -> ·runnable                     [/name/loop/foreach/if/number/string/$/]/else
  function -> ·name ( )                     [/name/loop/foreach/if/number/string/=/$/]/else
  function -> ·name ( argument )            [/name/loop/foreach/if/number/string/=/$/]/else
     index -> ·variable                     [/name/loop/foreach/if/number/string/=/$/]/else
     index -> ·variable [ variable ]        [/name/loop/foreach/if/number/string/=/$/]/else
  runnable -> ·loop ( name = index to index ) block [/name/loop/foreach/if/number/string/$/]/else
  runnable -> ·foreach ( name : index ) block [/name/loop/foreach/if/number/string/$/]/else
  runnable -> ·if ( index ) block           [/name/loop/foreach/if/number/string/$/]/else
  runnable -> ·if ( index ) block else block [/name/loop/foreach/if/number/string/$/]/else
  variable -> ·name                         [/name/loop/foreach/if/number/string/=/$/]/else
  variable -> ·function                     [/name/loop/foreach/if/number/string/=/$/]/else
  variable -> ·consts                       [/name/loop/foreach/if/number/string/=/$/]/else
    consts -> ·number                       [/name/loop/foreach/if/number/string/=/$/]/else
    consts -> ·string                       [/name/loop/foreach/if/number/string/=/$/]/else
-----I48-----
  runnable -> loop ( name = index to index ·) block $/[/name/loop/foreach/if/number/string/]/else
-----I49-----
  runnable -> foreach ( name : index ) block ·$/[/name/loop/foreach/if/number/string/]/else
-----I50-----
  runnable -> if ( index ) block else block ·$/[/name/loop/foreach/if/number/string/]/else
-----I51-----
  runnable -> loop ( name = index to index ) ·block [/name/loop/foreach/if/number/string/$/]/else
     block -> ·[ block ]                    [/name/loop/foreach/if/number/string/$/]/else
     block -> ·line block                   [/name/loop/foreach/if/number/string/$/]/else
     block ->                               [/name/loop/foreach/if/number/string/$/]/else
      line -> ·stmt                         [/name/loop/foreach/if/number/string/$/]/else
      stmt -> ·function                     [/name/loop/foreach/if/number/string/$/]/else
      stmt -> ·index = index                [/name/loop/foreach/if/number/string/$/]/else
      stmt -> ·runnable                     [/name/loop/foreach/if/number/string/$/]/else
  function -> ·name ( )                     [/name/loop/foreach/if/number/string/=/$/]/else
  function -> ·name ( argument )            [/name/loop/foreach/if/number/string/=/$/]/else
     index -> ·variable                     [/name/loop/foreach/if/number/string/=/$/]/else
     index -> ·variable [ variable ]        [/name/loop/foreach/if/number/string/=/$/]/else
  runnable -> ·loop ( name = index to index ) block [/name/loop/foreach/if/number/string/$/]/else
  runnable -> ·foreach ( name : index ) block [/name/loop/foreach/if/number/string/$/]/else
  runnable -> ·if ( index ) block           [/name/loop/foreach/if/number/string/$/]/else
  runnable -> ·if ( index ) block else block [/name/loop/foreach/if/number/string/$/]/else
  variable -> ·name                         [/name/loop/foreach/if/number/string/=/$/]/else
  variable -> ·function                     [/name/loop/foreach/if/number/string/=/$/]/else
  variable -> ·consts                       [/name/loop/foreach/if/number/string/=/$/]/else
    consts -> ·number                       [/name/loop/foreach/if/number/string/=/$/]/else
    consts -> ·string                       [/name/loop/foreach/if/number/string/=/$/]/else
-----I52-----
  runnable -> loop ( name = index to index ) block ·$/[/name/loop/foreach/if/number/string/]/else

==================================================

                  PARSING TABLE

==================================================
+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+
|          |        = |        [ |        ] |   number |   string |     name |        , |        ( |        ) |     loop |       to |  foreach |        : |       if |     else |        $ |   script |     line |     stmt |    block |   consts |    index | variable | argument | function | runnable |
+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+
|       0  |          |       s3 |          |      s15 |      s16 |       s9 |          |          |          |      s11 |          |      s12 |          |      s13 |          |       r8 |        1 |        4 |        5 |        2 |       14 |        7 |       10 |          |        6 |        8 |
|       1  |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |      acc |          |          |          |          |          |          |          |          |          |          |
|       2  |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |       r1 |          |          |          |          |          |          |          |          |          |          |
|       3  |          |       s3 |       r8 |      s15 |      s16 |       s9 |          |          |          |      s11 |          |      s12 |          |      s13 |          |          |          |        4 |        5 |       17 |       14 |        7 |       10 |          |        6 |        8 |
|       4  |          |       s3 |       r8 |      s15 |      s16 |       s9 |          |          |          |      s11 |          |      s12 |          |      s13 |       r8 |       r8 |          |        4 |        5 |       18 |       14 |        7 |       10 |          |        6 |        8 |
|       5  |          |       r2 |       r2 |       r2 |       r2 |       r2 |          |          |          |       r2 |          |       r2 |          |       r2 |       r2 |       r2 |          |          |          |          |          |          |          |          |          |          |
|       6  |      r14 |       r3 |       r3 |       r3 |       r3 |       r3 |          |          |          |       r3 |          |       r3 |          |       r3 |       r3 |       r3 |          |          |          |          |          |          |          |          |          |          |
|       7  |      s19 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|       8  |          |       r5 |       r5 |       r5 |       r5 |       r5 |          |          |          |       r5 |          |       r5 |          |       r5 |       r5 |       r5 |          |          |          |          |          |          |          |          |          |          |
|       9  |      r13 |      r13 |      r13 |      r13 |      r13 |      r13 |      r13 |      s20 |      r13 |      r13 |      r13 |      r13 |          |      r13 |      r13 |      r13 |          |          |          |          |          |          |          |          |          |          |
|      10  |      r11 |      s21 |      r11 |      r11 |      r11 |      r11 |      r11 |          |      r11 |      r11 |      r11 |      r11 |          |      r11 |      r11 |      r11 |          |          |          |          |          |          |          |          |          |          |
|      11  |          |          |          |          |          |          |          |      s22 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      12  |          |          |          |          |          |          |          |      s23 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      13  |          |          |          |          |          |          |          |      s24 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      14  |      r15 |      r15 |      r15 |      r15 |      r15 |      r15 |      r15 |          |      r15 |      r15 |      r15 |      r15 |          |      r15 |      r15 |      r15 |          |          |          |          |          |          |          |          |          |          |
|      15  |       r9 |       r9 |       r9 |       r9 |       r9 |       r9 |       r9 |          |       r9 |       r9 |       r9 |       r9 |          |       r9 |       r9 |       r9 |          |          |          |          |          |          |          |          |          |          |
|      16  |      r10 |      r10 |      r10 |      r10 |      r10 |      r10 |      r10 |          |      r10 |      r10 |      r10 |      r10 |          |      r10 |      r10 |      r10 |          |          |          |          |          |          |          |          |          |          |
|      17  |          |          |      s25 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      18  |          |       r7 |       r7 |       r7 |       r7 |       r7 |          |          |          |       r7 |          |       r7 |          |       r7 |       r7 |       r7 |          |          |          |          |          |          |          |          |          |          |
|      19  |          |          |          |      s15 |      s16 |       s9 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |       14 |       26 |       10 |          |       27 |          |
|      20  |          |          |          |      s15 |      s16 |       s9 |          |          |      s28 |          |          |          |          |          |          |          |          |          |          |          |       14 |       30 |       10 |       29 |       27 |          |
|      21  |          |          |          |      s15 |      s16 |       s9 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |       14 |          |       31 |          |       27 |          |
|      22  |          |          |          |          |          |      s32 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      23  |          |          |          |          |          |      s33 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      24  |          |          |          |      s15 |      s16 |       s9 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |       14 |       34 |       10 |          |       27 |          |
|      25  |          |       r6 |       r6 |       r6 |       r6 |       r6 |          |          |          |       r6 |          |       r6 |          |       r6 |       r6 |       r6 |          |          |          |          |          |          |          |          |          |          |
|      26  |          |       r4 |       r4 |       r4 |       r4 |       r4 |          |          |          |       r4 |          |       r4 |          |       r4 |       r4 |       r4 |          |          |          |          |          |          |          |          |          |          |
|      27  |          |      r14 |      r14 |      r14 |      r14 |      r14 |      r14 |          |      r14 |      r14 |      r14 |      r14 |          |      r14 |      r14 |      r14 |          |          |          |          |          |          |          |          |          |          |
|      28  |      r18 |      r18 |      r18 |      r18 |      r18 |      r18 |      r18 |          |      r18 |      r18 |      r18 |      r18 |          |      r18 |      r18 |      r18 |          |          |          |          |          |          |          |          |          |          |
|      29  |          |          |          |          |          |          |          |          |      s35 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      30  |          |          |          |          |          |          |      s36 |          |      r16 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      31  |          |          |      s37 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      32  |      s38 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      33  |          |          |          |          |          |          |          |          |          |          |          |          |      s39 |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      34  |          |          |          |          |          |          |          |          |      s40 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      35  |      r19 |      r19 |      r19 |      r19 |      r19 |      r19 |      r19 |          |      r19 |      r19 |      r19 |      r19 |          |      r19 |      r19 |      r19 |          |          |          |          |          |          |          |          |          |          |
|      36  |          |          |          |      s15 |      s16 |       s9 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |       14 |       30 |       10 |       41 |       27 |          |
|      37  |      r12 |      r12 |      r12 |      r12 |      r12 |      r12 |      r12 |          |      r12 |      r12 |      r12 |      r12 |          |      r12 |      r12 |      r12 |          |          |          |          |          |          |          |          |          |          |
|      38  |          |          |          |      s15 |      s16 |       s9 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |       14 |       42 |       10 |          |       27 |          |
|      39  |          |          |          |      s15 |      s16 |       s9 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |       14 |       43 |       10 |          |       27 |          |
|      40  |          |       s3 |       r8 |      s15 |      s16 |       s9 |          |          |          |      s11 |          |      s12 |          |      s13 |       r8 |       r8 |          |        4 |        5 |       44 |       14 |        7 |       10 |          |        6 |        8 |
|      41  |          |          |          |          |          |          |          |          |      r17 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      42  |          |          |          |          |          |          |          |          |          |          |      s45 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      43  |          |          |          |          |          |          |          |          |      s46 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      44  |          |      r22 |      r22 |      r22 |      r22 |      r22 |          |          |          |      r22 |          |      r22 |          |      r22 |      s47 |      r22 |          |          |          |          |          |          |          |          |          |          |
|      45  |          |          |          |      s15 |      s16 |       s9 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |       14 |       48 |       10 |          |       27 |          |
|      46  |          |       s3 |       r8 |      s15 |      s16 |       s9 |          |          |          |      s11 |          |      s12 |          |      s13 |       r8 |       r8 |          |        4 |        5 |       49 |       14 |        7 |       10 |          |        6 |        8 |
|      47  |          |       s3 |       r8 |      s15 |      s16 |       s9 |          |          |          |      s11 |          |      s12 |          |      s13 |       r8 |       r8 |          |        4 |        5 |       50 |       14 |        7 |       10 |          |        6 |        8 |
|      48  |          |          |          |          |          |          |          |          |      s51 |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |          |
|      49  |          |      r21 |      r21 |      r21 |      r21 |      r21 |          |          |          |      r21 |          |      r21 |          |      r21 |      r21 |      r21 |          |          |          |          |          |          |          |          |          |          |
|      50  |          |      r23 |      r23 |      r23 |      r23 |      r23 |          |          |          |      r23 |          |      r23 |          |      r23 |      r23 |      r23 |          |          |          |          |          |          |          |          |          |          |
|      51  |          |       s3 |       r8 |      s15 |      s16 |       s9 |          |          |          |      s11 |          |      s12 |          |      s13 |       r8 |       r8 |          |        4 |        5 |       52 |       14 |        7 |       10 |          |        6 |        8 |
|      52  |          |      r20 |      r20 |      r20 |      r20 |      r20 |          |          |          |      r20 |          |      r20 |          |      r20 |      r20 |      r20 |          |          |          |          |          |          |          |          |          |          |
+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+----------+
```
