list-it - Fixed Column Text Table Formatter
===========================================

[![Build Status](https://travis-ci.org/takamin/list-it.svg?branch=master)](https://travis-ci.org/takamin/list-it)

DESCRIPTION
-----------

This module creates a text table string.
And offers a cli command `listit` that print arrays in a json file to console
as a table.

* Each columns are aligned in vertical.
* All number data in column are aligned by its fraction point with `autoAlign` option.
* Longer text can be truncated with `setColumnWidth` option.

CLI Command `listit`
--------------------

### INSTALL

Install with npm.

```bash
$ npm install --global list-it
```

### USAGE

```bash
$ listit --help
Usage: listit [input-filename] [OPTIONS]

Outputs the array included in JSON to the console in tabular format.
Non-array data is displayed as is.

OPTIONS:
  -h, --help    Print this help message
  -v, --version Print the version of this package

----
This command is included in the npm list-it@1.2.0

Repository: https://github.com/takamin/list-it
Homepage: http://takamints.hatenablog.jp/entry/npm-list-it-preformatted-text-table-generator

Copyright (c) 2020 Koji Takami
This software is released under the MIT License
```

### SAMPLE

The `listit` would print all data in the JSON file with its property name.
In following example, `$` means root oject.

```bash
$ listit ./sample/planets.json

[$]:
name    mass      dia    dens grav escV rot
MERCURY    0.33     4879 5427  3.7  4.3  1407.6
VENUS      4.87    12104 5243  8.9 10.4 -5832.5
EARTH      5.97    12756 5514  9.8 11.2    23.9
MOON       0.0073   3475 3340  1.6  2.4   655.7
MARS       0.642    6792 3933  3.7  5.0    24.6
JUPITER 1898.0    142984 1326 23.1 59.5     9.9
SATURN   568.0    120536  687  9.0 35.5    10.7
URANUS    86.8     51118 1271  8.7 21.3   -17.2
NEPTUNE  102.0     49528 1638 11.0 23.5    16.1
PLUTO      0.0146   2370 2095  0.7  1.3  -153.3

```


PROGRAMMING SAMPLE
------------------

__[sample/japanese-food.js](sample/japanese-food.js)__

```
var ListIt = require("list-it");
var buf = new ListIt();
buf.setColumnWidth(1, 5);
buf.setColumnWidth(2, 15);
buf.setColumnWidth(3, 7);
console.log(
    buf
        .d("1").d("Sushi")
            .d("vinegared rice combined raw seafood")
            .d("Healthy").nl()
        .d("2").d("Yakiniku")
            .d("Grilled meat on Japanese")
            .d("Juicy").nl()
        .d("3").d("Ramen")
            .d("Japanese noodle soup dish")
            .d("I like it").nl()
        .d("4").d("Tempura")
            .d("Deep fried seafood or vegetables")
            .d("Delicious").nl()
        .d("5").d("Sashimi")
            .d("Very fresh sliced fish")
            .d("Try it now, It's good").nl()
        .toString());
```

outputs:

```
$ node sample/japanese-food.js
1 Sushi vinegared rice  Healthy
2 Yakin Grilled meat on Juicy
3 Ramen Japanese noodle I like
4 Tempu Deep fried seaf Delicio
5 Sashi Very fresh slic Try it
```

### autoAlign

__[sample/planets.js](sample/planets.js)__

```
var ListIt = require("list-it");
var buf = new ListIt({ "autoAlign" : true });
var PLANETS = [
    ["NAME", "Mass(10^24kg)", "Dia(km)", "Dens(kg/m3)",
                        "Grav(m/s2)", "EscV(km/s)", "Rot(hours)" ],
    ["MERCURY", 0.33,   4879,   5427,   3.7,    4.3,    1407.6  ],
    ["VENUS",   4.87,   12104,  5243,   8.9,    10.4,   -5832.5 ],
    ["EARTH",   5.97,   12756,  5514,   9.8,    11.2,   23.9    ],
    ["MOON",    0.0073, 3475,   3340,   1.6,    2.4,    655.7   ],
    ["MARS",    0.642,  6792,   3933,   3.7,    5.0,    24.6    ],
    ["JUPITER", 1898,   142984, 1326,   23.1,   59.5,   9.9     ],
    ["SATURN",  568,    120536, 687,    9.0,    35.5,   10.7    ],
    ["URANUS",  86.8,   51118,  1271,   8.7,    21.3,   -17.2   ],
    ["NEPTUNE", 102,    49528,  1638,   11.0,   23.5,   16.1    ],
    ["PLUTO",   0.0146, 2370,   2095,   0.7,    1.3,    -153.3  ]
];
console.log( buf.d( PLANETS ).toString() );
```

outputs:

```
$ node sample/planets.js
NAME    Mass(10^24kg) Dia(km) Dens(kg/m3) Grav(m/s2) EscV(km/s) Rot(hours)
MERCURY        0.33      4879        5427        3.7        4.3     1407.6
VENUS          4.87     12104        5243        8.9       10.4    -5832.5
EARTH          5.97     12756        5514        9.8       11.2       23.9
MOON           0.0073    3475        3340        1.6        2.4      655.7
MARS           0.642     6792        3933        3.7        5.0       24.6
JUPITER     1898.0     142984        1326       23.1       59.5        9.9
SATURN       568.0     120536         687        9.0       35.5       10.7
URANUS        86.8      51118        1271        8.7       21.3      -17.2
NEPTUNE      102.0      49528        1638       11.0       23.5       16.1
PLUTO          0.0146    2370        2095        0.7        1.3     -153.3
```

### Object Array

__[sample/planets-obj.js](sample/planets-obj.js)__
```
var ListIt = require("list-it");
var buf = new ListIt({ "autoAlign" : true });
var PLANETS = [
    { name: "MERCURY", mass: 0.33, dia: 4879, dens: 5427,
        grav: 3.7, escV: 4.3, rot: 1407.6 },
    { name: "VENUS", mass: 4.87, dia: 12104, dens: 5243,
        grav: 8.9, escV: 10.4, rot: -5832.5 },
    { name: "EARTH", mass: 5.97, dia: 12756, dens: 5514,
        grav: 9.8, escV: 11.2, rot: 23.9 },
    { name: "MOON", mass: 0.0073, dia: 3475, dens: 3340,
        grav: 1.6, escV: 2.4, rot: 655.7 },
    { name: "MARS", mass: 0.642, dia: 6792, dens: 3933,
        grav: 3.7, escV: 5.0, rot: 24.6 },
    { name: "JUPITER", mass: 1898, dia: 142984, dens: 1326,
        grav: 23.1, escV: 59.5, rot: 9.9 },
    { name: "SATURN", mass: 568, dia: 120536,dens: 687,
        grav: 9.0, escV: 35.5, rot: 10.7 },
    { name: "URANUS", mass: 86.8, dia: 51118, dens: 1271,
        grav: 8.7, escV: 21.3, rot: -17.2 },
    { name: "NEPTUNE", mass: 102, dia: 49528, dens: 1638,
        grav: 11.0, escV: 23.5, rot: 16.1 },
    { name: "PLUTO", mass: 0.0146, dia: 2370, dens: 2095,
        grav: 0.7, escV: 1.3, rot: -153.3 }
];
console.log( buf.d( PLANETS ).toString() );
```

outputs:

```
$ node sample/planets-obj.js
name    mass      dia    dens grav escV rot
MERCURY    0.33     4879 5427  3.7  4.3  1407.6
VENUS      4.87    12104 5243  8.9 10.4 -5832.5
EARTH      5.97    12756 5514  9.8 11.2    23.9
MOON       0.0073   3475 3340  1.6  2.4   655.7
MARS       0.642    6792 3933  3.7  5.0    24.6
JUPITER 1898.0    142984 1326 23.1 59.5     9.9
SATURN   568.0    120536  687  9.0 35.5    10.7
URANUS    86.8     51118 1271  8.7 21.3   -17.2
NEPTUNE  102.0     49528 1638 11.0 23.5    16.1
PLUTO      0.0146   2370 2095  0.7  1.3  -153.3
```

### East asian characters

__[sample/japanese-food-jp.js](sample/japanese-food-jp.js)__

```
var ListIt = require("list-it");
var buf = new ListIt();
console.log(
    buf
        .d("1").d("寿司")
            .d("酢とご飯とシーフード")
            .d("健康的だ").nl()
        .d("2").d("焼肉")
            .d("日本のグリルされたお肉")
            .d("ジューシー").nl()
        .d("3").d("ラーメン")
            .d("日本のスープに入った麺")
            .d("大好き").nl()
        .d("4").d("天ぷら")
            .d("シーフードや野菜に衣をつけて揚げたもの")
            .d("おいしー").nl()
        .d("5").d("刺身")
            .d("大変フレッシュな魚のスライス")
            .d("食べてみて！あご落ちるぜ").nl()
        .toString());
```

outputs:

```
$ node sample/japanese-food-jp.js
1 寿司     酢とご飯とシーフード                   健康的だ
2 焼肉     日本のグリルされたお肉                 ジューシー
3 ラーメン 日本のスープに入った麺                 大好き
4 天ぷら   シーフードや野菜に衣をつけて揚げたもの おいしー
5 刺身     大変フレッシュな魚のスライス           食べてみて！あご落ちるぜ
```



API
---

### class ListIt(opt)

Creates a `ListIt` instance.

The instance has current row that is a position for the columns to be added.

You cannot edit the columns and rows that were already added using `d(...)` method.

See the examples below.

#### opt.autoAlign

When this is set true, the data in cell will be aligned in automatic depending on its type.

The number will be aligned to the right taking account of its decimal point.

* Type : boolean
* Default setting : true

#### opt.columnWidth

Declare text width for columns by character length (or remove).

* Type : Array<number>|number|null
* Default: null

**For Each Columns**

An array of numbers could be specified.
Its each elements are set to the column at that position.
A `null` as the element value means that width will not be specified.

**For All Columns**

If a single number is specified for this option, It will set to all columns.
And also when the value is null, column width is not declared at all.

#### ListIt#setColumnWidth(indexOfColumns:number, width:number)

Set the column width by text length.

The actual width is calculated by traversing all data in a column.
A number data never be affected, because it should not be truncated.
So it may be longer than the specified length when some number data
exist in a column.

PARAMETERS:

1. `indexOfColumns` - a column index to set.
2. `width` - a character length of the column.
    If `null` is specified, the declaration is removed.

RETURN VALUE:

This method returns `this` instance to chain the next method call.

#### ListIt#setColumnWidthAll(widthForAll:Array<number|null>|number|null)

Set the whole column's width. See opt.columnWidth

PARAMETERS:

1. `widthForAll` - An array of widtha.

RETURN VALUE:

This method returns `this` instance to chain the next method call.

### ListIt#d( data [, data ...] )

This method adds one or more columns or rows at a time depending on
the parameter data type.

This method returns `this` object. So you can chain to call a next method.

#### How to add column(s)

If the type of `data` is a primitive type such as string or number,
these are added to the current row as individual columns.

This operation will not add a new line in automatic.
A code of below outputs only one row containing six column from 1 to 6.

```
CODE: buffer.d(1,2,3).d(4,5,6).nl();

OUTPUT: "1 2 3 4 5 6"
```

The above code make same result as below:

```
EQUIVALENT CODE: buffer.d(1,2,3,4,5,6).nl();
```

#### How to add row(s)

If the parameter `data` is an array contains one or more primitive data at least,
it will added as one closed row.

But if the type of all elements of the array is an array,
in other words it is two or more dimensional array,
each elements are added as a row.

NOTE: A new-line will never be added before the addition.
So, If the previous row was not closed, you must call the `nl()` method.

The following sample outputs two rows:

```
CODE: buffer.d( [1,2,3], [4,5,6] );

OUTPUT:"1 2 3\n4 5 6"

EQUIVALENT CODE: buffer.d([ [1,2,3], [4,5,6] ]);
```


### ListIt#nl()

Ends up a process for the current row.

This method also returns `this` object.

### ListIt#toString()

Returns preformatted text table.


LICENSE
-------

MIT
