list-it - Fixed Column Text Table Formatter
===========================================

DESCRIPTION
-----------

This module is used to create a preformatted text table.

Each columns in all rows are aligned in vertical.

You can put it to the console or a preformated text-file.

When a autoAlign option is set, the numbers are aligned by its fraction point.

SAMPLE
------

__japanese-foods.js__

```
var listit = require("list-it");
var buf = listit.buffer();
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
1 Sushi    vinegared rice combined raw seafood Healthy
2 Yakiniku Grilled meat on Japanese            Juicy
3 Ramen    Japanese noodle soup dish           I like it
4 Tempura  Deep fried seafood or vegetables    Delicious
5 Sashimi  Very fresh sliced fish              Try it now, It's good
```

### autoAlign

__planets.js__

```
var listit = require("list-it");
var buf = listit.buffer({ "autoAlign" : true });
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


METHODS
-------

### buffer(opt)

Creates a `ListItBuffer` instance and returns it.

The instance has current row that is a position for the columns to be added.

You cannot edit the columns and rows that were already added.

See the examples below.

#### opt.autoAlign

When this is set true, the data in cell will be aligned in automatic depending on its type.

The number will be aligned to the right taking account of its decimal point.

* Type : boolean
* Default setting : false

### ListItBuffer.d( data [, data ...] )

This method adds one or more columns or rows at a time depending on
the parameter data type.

This method returns `this` object. So you can chain a method call.

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


### ListItBuffer.nl()

Ends up a process for the current row.

This method also returns `this` object.

### ListItBuffer.toString()

Returns preformatted text table.


LICENCE
-------

MIT
