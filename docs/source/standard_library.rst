Standard library
================

**This section is still a work in progress**

The Aya standard library consists of type definitions, mathematical
functions, string and list operations, plotting tools and even a small
turtle graphics library. It also defines functions and objects for
working with colors, dates, files, GUI elements, and basic data
structures such as queues, stacks, and sets. The standard library also
contains a file which defines extended ASCII operators for use when code
golfing.

``matrix``
^^^^^^^^^^

The ``matrix`` type provides a basic interface and operator overloads
for working with matrices.

::

   aya> 3 3 10 matrix.randint :mat
   |  7  8  2 |
   |  8  7  3 |
   |  8  4  4 |

   aya> mat [[0 1] 0] I
   |  7 |
   |  8 |

   aya> mat [[0 1] 0] I .t
   |  7  8 |

   aya> mat 2 ^ 100 -
   |   29   20  -54 |
   |   36   25  -51 |
   |   20    8  -56 |

``dataframe``
^^^^^^^^^^^^^

The ``dataframe`` type is an interface for working with tables. CSV
files can be directly imported and modified or the data can be generated
by the program itself.

::

   aya> {, "data/simple.csv":filename } dataframe! :df
            A    B    C
     0 |    1    2    3
     1 |    4    5    6
     2 |    7    8    9

   aya> df [[0 1] ["A" "C"]] I
            A    C
     0 |    1    3
     1 |    4    6

   aya> {, [[1 7 3][8 3 6]]:data } dataframe!
            a    b
     0 |    1    8
     1 |    7    3
     2 |    3    6

   aya> {, [[1 7 3][8 3 6]]:data ["x" "y" "z"]:index} dataframe!
            a    b
     x |    1    8
     y |    7    3
     z |    3    6

``golf``
^^^^^^^^

``golf`` defines many short variables that are useful when golfing. It
also uses the ``Mk`` operator to add additional single character
operators. In the following code, all variables ``ì``, ``¶``, ``¦``,
``¥`` and ``r`` are defined in the golf script.

::

   aya> .# Generate and print an addition table
   aya> 6r_ì¶¦¥
      0   1   2   3   4   5
      1   2   3   4   5   6
      2   3   4   5   6   7
      3   4   5   6   7   8
      4   5   6   7   8   9
      5   6   7   8   9  10

A few more examples

::

   aya> [ a b c d k l p w z ì í]
   [ 2 3 10 1000 [ ] 3.14159265 -1 0 {+} {-} ]

``date``
^^^^^^^^

The date script provides a basic interface for the date parsing
operators ``Mh`` and ``MH``. It also provides basic date unit addition
and subtraction.

::

   aya> date.now
   May 01, 2017 12:53:25 PM

   aya> date.now.year
   2017

   aya> date.now 2 dates.month +
   Jul 01, 2017 8:53:42 AM

   aya> date.now 2 dates.month + .mmddyy
   "07/01/17"

``set``
^^^^^^^

The ``set`` script defines a ``set`` type and many operator overloads.
It defines ``s`` as a prefix operator for the set constructor allowing
the syntax ``s[ ... ]`` to create sets.

::

   aya> s[1 2 3 2 2 1]  .# == ([1 2 3 2 2 1] set!)
   s[ 1 2 3 ]

   aya> s[1 2 3] s[2 3 4] |
   s[ 1 2 3 4 ]

   aya> s[1 2 3] s[2 3 4] &
   s[ 2 3 ]

   aya> s[1 2 3] s[2 5] /
   s[ 1 3 ]

``enum``
^^^^^^^^

The ``enum`` script defines the ``enum`` keyword which uses dictionaries
and metatables to create enums.

::

   aya> enum ::shape [::circle ::triangle ::square]

   aya> shape
   shape

   aya> shape :T
   ::enum

   aya> shape.circle
   shape.circle

   aya> shape.circle :T
   ::shape

   aya> shape.circle shape.circle =
   1

``color``
^^^^^^^^^

The ``color`` script defines basic color constructors and conversions.

::

   aya> 14 57 100 color!
   (14, 57, 100)

   aya> "0e3964" color.newhex
   (14, 57, 100)

   aya> colors.cobalt
   (61, 89, 171)

   aya> colors.cobalt.hsv
   [ 224.72727273 .64327485 .67058824 ]

   aya> 5 colors.red colors.blue.grad matstr:P
     255    0    0
     191    0   63
     127    0  127
      63    0  191
       0    0  255

``file``
^^^^^^^^

The ``file`` script defines variables for moving around and exploring
the directory tree. It also defines the ``file`` type which is used for
opening and editing files.

::

   aya> cd "data"
   /home/nick/Documents/aya-lang/data/

   aya> ls
     /rdatasets
     catalog.csv
     colors.csv
     cor.csv
     p022_names.txt
     realvals.csv
     satwords.txt
     simple.csv
     simplemat.txt
     words.txt

   aya> more "simple.csv"
   A, B, C
   1, 2, 3
   4, 5, 6
   7, 8, 9

   aya> pwd
   /home/nick/Documents/aya-lang/data/
