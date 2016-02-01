.. _framework=tools=available=common=manipulate=text:

================
Manipulate files 
================

Paste two files side by side
############################

This tool merges two datasets side by side. If the first (left) dataset contains column assignments such as chromosome, start, end and strand, these will be preserved. However, if you would like to change column assignments, click the pencil icon in the history item.

Example
*******

First dataset::

    a 1
    a 2
    a 3

Second dataset::

    20
    30
    40 

Pasting them together will produce::

    a 1 20
    a 2 30
    a 3 40

Select random lines from a file
###############################

This tool selects N random lines from a file, with no repeats, and preserving ordering.

Example
*******

Input File::

    chr7  56632  56652   D17003_CTCF_R6  310  +
    chr7  56736  56756   D17003_CTCF_R7  354  +
    chr7  56761  56781   D17003_CTCF_R4  220  +
    chr7  56772  56792   D17003_CTCF_R7  372  +
    chr7  56775  56795   D17003_CTCF_R4  207  +

Selecting 2 random lines might return this::

    chr7  56736  56756   D17003_CTCF_R7  354  +
    chr7  56775  56795   D17003_CTCF_R4  207  +

Line/Word/Character count of a dataset
######################################

This tool outputs counts of specified attributes (lines, words, characters) of a dataset.

Filter data on any column using simple expressions
##################################################

The filter tool allows you to restrict the dataset using simple conditional statements.

Columns are referenced with c and a number. For example, c1 refers to the first column of a tab=delimited file
Make sure that multi=character operators contain no white space ( e.g., <# is valid while < # is not valid )
When using 'equal=to' operator double equal sign '##' must be used ( e.g., c1##'chr1' )
Non=numerical values must be included in single or double quotes ( e.g., c6##'+' )
Filtering condition can include logical operators, but make sure operators are all lower case ( e.g., (c1!#'chrX' and c1!#'chrY') or not c6##'+' )

Example
*******

``c1##'chr1'`` selects lines in which the first column is chr1

``c3=c2<100*c4`` selects lines where subtracting column 3 from column 2 is less than the value of column 4 times 100

``len(c2.split(',')) < 4`` will select lines where the second column has less than four comma separated elements

``c2>#1`` selects lines in which the value of column 2 is greater than or equal to 1

Numbers should not contain commas = ``c2<#44,554,350`` will not work, but ``c2<#44554350`` will. Some words in the data can be used, but must be single or double quoted ( e.g., ``c3##'exon'`` )

Sort data in ascending or descending order
##########################################

This tool sorts the dataset on any number of columns in either ascending or descending order.

Numerical sort orders numbers by their magnitude, ignores all characters besides numbers, and evaluates a string of numbers to the value they signify.
General numeric sort orders numbers by their general numerical value. Unlike the numerical sort option, it can handle numbers in scientific notation too.
Alphabetical sort is a phonebook type sort based on the conventional order of letters in an alphabet. Each nth letter is compared with the nth letter of other words in the list, starting at the first letter of each word and advancing to the second, third, fourth, and so on, until the order is established. Therefore, in an alphabetical sort, 2 comes after 100 (1 < 2).

Examples
*******

The list of numbers 4,17,3,5 collates to 3,4,5,17 by numerical sorting, while it collates to 17,3,4,5 by alphabetical sorting.

Sorting the following::

    Q     d    7   II    jhu  45
    A     kk   4   I     h    111
    Pd    p    1   ktY   WS   113
    A     g    10  H     ZZ   856
    A     edf  4   tw    b    234
    BBB   rt   10  H     ZZ   100
    A     rew  10  d     b    1111
    C     sd   19  YH    aa   10
    Hah   c    23  ver   bb   467
    MN    gtr  1   a     X    32
    N     j    9   a     T    205
    BBB   rrf  10  b     Z    134
    odfr  ws   6   Weg   dew  201
    C     f    3   WW    SW   34
    A     jhg  4   I     b    345
    Pd    gf   7   Gthe  de   567
    rS    hty  90  YY    LOp  89
    A     g    10  H     h    43
    A     g    4   I     h    500

on columns 1 (alphabetical), 3 (numerical), and 6 (numerical) in ascending order will yield::

    A     kk   4   I     h    111
    A     edf  4   tw    b    234
    A     jhg  4   I     b    345
    A     g    4   I     h    500
    A     g    10  H     h    43
    A     g    10  H     ZZ   856
    A     rew  10  d     b    1111
    BBB   rt   10  H     ZZ   100
    BBB   rrf  10  b     Z    134
    C     f    3   WW    SW   34
    C     sd   19  YH    aa   10
    Hah   c    23  ver   bb   467
    MN    gtr  1   a     X    32
    N     j    9   a     T    205
    odfr  ws   6   Weg   dew  201
    Pd    p    1   ktY   WS   113
    Pd    gf   7   Gthe  de   567
    Q     d    7   II    jhu  45
    rS    hty  90  YY    LOp  89

Sorting the following::

    chr10  100  200  feature1  100.01   +
    chr20  800  900  feature2  1.1      +
    chr2   500  600  feature3  1000.1   +
    chr1   300  400  feature4  1.1e=05  +
    chr21  300  500  feature5  1.1e2    +
    chr15  700  800  feature6  1.1e4    +

on column 5 (numerical) in ascending order will yield::

    chr1   300  400  feature4  1.1e=05  +
    chr15  700  800  feature6  1.1e4    +
    chr20  800  900  feature2  1.1      +
    chr21  300  500  feature5  1.1e2    +
    chr10  100  200  feature1  100.01   +
    chr2   500  600  feature3  1000.1   +

on column 5 (general numeric) in ascending order will yield::

    chr1   300  400  feature4  1.1e=05  +
    chr20  800  900  feature2  1.1      +
    chr10  100  200  feature1  100.01   +
    chr21  300  500  feature5  1.1e2    +
    chr2   500  600  feature3  1000.1   +
    chr15  700  800  feature6  1.1e4    +

Select lines that match an expression
#####################################

The select tool searches the data for lines containing or not containing a match to the given pattern. Regular Expression is introduced in this tool. A Regular Expression is a pattern describing a certain amount of text.

= ``( ) { } [ ] . * ? + ^ $` are all special characters. \ can be used to "escape" a special character, allowing that special character to be searched for.
= ``\A`` matches the beginning of a string(but not an internal line).
= ``\d`` matches a digit, same as [0=9].
= ``\D`` matches a non=digit.
= ``\s`` matches a whitespace character.
= ``\S`` matches anything BUT a whitespace.
= ``\t`` matches a tab.
= ``\w`` matches an alphanumeric character.
= ``\W`` matches anything but an alphanumeric character.
= ``( .. )`` groups a particular pattern.
= ``\Z`` matches the end of a string(but not a internal line).
= ``{ n or n, or n,m }`` specifies an expected number of repetitions of the preceding pattern.
= ``{n}`` The preceding item is matched exactly n times.
= ``{n,}`` The preceding item is matched n or more times.
= ``{n,m}`` The preceding item is matched at least n times but not more than m times.
= ``[ ... ]`` creates a character class. Within the brackets, single characters can be placed. A dash (=) may be used to indicate a range such as a=z.
= ``.`` Matches any single character except a newline.
= ``*`` The preceding item will be matched zero or more times.
= ``?`` The preceding item is optional and matched at most once.
= ``+`` The preceding item will be matched one or more times.
= ``^`` has two meaning: = matches the beginning of a line or string. = indicates negation in a character class. For example, [^...] matches every character except the ones inside brackets.
= ``$`` matches the end of a line or string.
= ``|`` Separates alternate possibilities.

Example
*******

``^chr([0=9A=Za=z])+`` would match lines that begin with chromosomes, such as lines in a BED format file.

``(ACGT){1,5}`` would match at least 1 "ACGT" and at most 5 "ACGT" consecutively.

``([^,][0=9]{1,3})(,[0=9]{3})*`` would match a large integer that is properly separated with commas such as 23,078,651.

``(abc)|(def)`` would match either "abc" or "def".

``^\W+#`` would match any line that is a comment.

Join two Datasets side by side on a specified field
###################################################

This tool joins lines of two datasets on a common field. An empty string ("") is not a valid identifier. You may choose to include lines of your first input that do not join with your second input.

Columns are referenced with a number. For example, 3 refers to the 3rd column of a tab=delimited file.

Example
*******

Dataset1::

    chr1 10 20 geneA
    chr1 50 80 geneB
    chr5 10 40 geneL

Dataset2::

    geneA tumor=supressor
    geneB Foxp2
    geneC Gnas1
    geneE INK4a

Joining the 4th column of Dataset1 with the 1st column of Dataset2 will yield::

    chr1 10 20 geneA geneA tumor=suppressor
    chr1 50 80 geneB geneB Foxp2

Joining the 4th column of Dataset1 with the 1st column of Dataset2, while keeping all lines from Dataset1, will yield::

    chr1 10 20 geneA geneA tumor=suppressor
    chr1 50 80 geneB geneB Foxp2
    chr5 10 40 geneL

Compare two Datasets to find common or distinct rows
####################################################

This tool finds lines in one dataset that HAVE or DO NOT HAVE a common field with another dataset.

Example
*******

If this is First dataset::

    chr1 10 20 geneA
    chr1 50 80 geneB
    chr5 10 40 geneL

and this is Second dataset::

    geneA tumor=suppressor
    geneB Foxp2
    geneC Gnas1
    geneE INK4a

Finding lines of the First dataset whose 4th column matches the 1st column of the Second dataset yields::

    chr1 10 20 geneA
    chr1 50 80 geneB

Conversely, using option Non Matching rows of First dataset on the same fields will yield::

    chr5 10 40 geneL

Group data by a column and perform aggregate operation on other columns
#######################################################################

This tool allows you to group the input dataset by a particular column and perform aggregate functions: Mean, Median, Mode, Sum, Max, Min, Count, Concatenate, and Randomly pick on any column(s).

The Concatenate function will take, for each group, each item in the specified column and build a comma delimited list. Concatenate Unique will do the same but will build a list of unique items with no repetition.

Count and Count Unique are equivalent to Concatenate and Concatenate Unique, but will only count the number of items and will return an integer.

If multiple modes are present, all are reported.

Example
*******

For the following input::

    chr22  1000  1003  TTT
    chr22  2000  2003  aaa
    chr10  2200  2203  TTT
    chr10  1200  1203  ttt
    chr22  1600  1603  AAA

Grouping on column 4 while ignoring case, and performing operation Count on column 1 will return::

    AAA    2
    TTT    3

Grouping on column 4 while not ignoring case, and performing operation Count on column 1 will return::

    aaa    1
    AAA    1
    ttt    1
    TTT    2

Transform column content with regular expression
################################################

This tool transform content of one column given a regular expression. The regular expression can be tested on `Pythex <http://pythex.org/>`_.

Add column to an existing dataset
#################################

You can enter any value and it will be added as a new column to your dataset

Example
*******

If you original data looks like this::

    chr1 10  100 geneA
    chr2 200 300 geneB
    chr2 400 500 geneC

Typing + in the text box will generate::

    chr1 10  100 geneA +
    chr2 200 300 geneB +
    chr2 400 500 geneC +

You can also add line numbers by selecting Iterate: YES. In this case if you enter 1 in the text box you will get::

    chr1 10  100 geneA 1
    chr2 200 300 geneB 2
    chr2 400 500 geneC 3

Change Case of selected columns
###############################

This tool selects specified columns from a dataset and converts the values of those columns to upper or lower case.

Columns are specified as c1, c2, and so on.
Columns can be specified in any order (e.g., c2,c1,c6)

Example
*******

Changing columns 1 and 3 ( delimited by Comma ) to upper case in::

    apple,is,good
    windows,is,bad

will result in::

    APPLE is GOOD
    WINDOWS is BAD

Column Join
###########

This tool allows you to join several files with the same column structure into one file, removing certain columns if necessary. The user needs to select a 'hinge', which is the number of left=most columns to match on. They also need to select the columns to include in the join, which should include the hinge columns, too.

Note that the files are expected to have the same number of columns. If for some reason the join column is missing (this only applies to the last column(s)), the tool attempts to handle this situation by inserting an empty item (or the appropriate filler) for that column on that row. This could lead to the situation where a row has a hinge but entirely empty or filled columns, if the hinge exists in at least one file but every file that has it is missing the join column. Also, note that the tool does not distinguish between a file missing the hinge altogether and a file having the hinge but missing the column (in both cases the column would be empty or filled). There is an example of this below

General Example
***************

Given the following files:

FILE 1::

    chr2    1    T    6    .C...,     I$$III
    chr2    2    G    6    ..N..,     III@II
    chr2    3    C    7    ..C...,    I$IIIII
    chr2    4    G    7    .G....,    I#IIIII
    chr2    5    G    7    ...N..,    IIII#BI
    chr2    6    A    7    ..T...,    I$IDIII
    chr1    1    C    1    ^:.        I
    chr1    2    G    2    .^:.       $I
    chr1    3    A    2    ..         I%
    chr1    4    C    2    ..         I$
    chr1    5    T    3    ..^:.      I#I
    chr1    6    G    3    ..^:,      I#I

FILE 2::

    chr1    3    T    1    ^:.        I
    chr1    4    G    2    .^:.       $I
    chr1    5    T    2    ..         I%
    chr1    6    C    3    ..^:.      III
    chr1    7    G    3    ..^:.      I#I
    chr1    8    T    4    ...^:,     I#II
    chr2    77   C    6    .G...,     I$$III
    chr2    78   G    6    ..N..,     III@II
    chr2    79   T    7    ..N...,    I$IIIII
    chr2    80   C    7    .G....,    I#IIIII
    chr2    81   G    7    ...A..,    IIII#BI
    chr2    82   A    8    ...G...,   I$IDIIII
    chr2    83   T    8    .A.....N   IIIIIIII
    chr2    84   A    9    ......T.   I$IIIIIII

FILE 3::

    chr1    1    A    1    .          I
    chr1    2    T    2    G.         I$
    chr1    3    C    2    .,         I@
    chr1    4    C    3    ..N        III
    chr1    42   C    5    ...N^:.    III@I
    chr1    43   C    5    .N..^:.    IIIII
    chr1    44   T    5    .A..,      IA@II
    chr1    45   A    6    .N...^:.   IIIII$
    chr1    46   G    6    .GN..^:.   I@IIII
    chr1    47   A    7    ....^:..,  IIIII$I
    chr2    73   T    5    .N..,      II$II
    chr2    74   A    5    ....,      IIIII
    chr2    75   T    5    ....,      IIIII
    chr2    76   T    5    ....,      IIIII
    chr2    77   C    5    ....,      IIIBI
    chr2    78   T    5    ....,      IDIII

To join on columns 3 and 4 combining on columns 1 and 2, columns 1=4 should be selected for the 'Include these columns' option, and column 2 selected for the 'hinge'. With these settings, the following would be output::

    chr1    1    C    1              A    1
    chr1    2    G    2              T    2
    chr1    3    A    2    T    1    C    2
    chr1    4    C    2    G    2    C    3
    chr1    5    T    3    T    2
    chr1    6    G    3    C    3
    chr1    7              G    3
    chr1    8              T    4
    chr1    42                       C    5
    chr1    43                       C    5
    chr1    44                       T    5
    chr1    45                       A    6
    chr1    46                       G    6
    chr1    47                       A    7
    chr2    1    T    6
    chr2    2    G    6
    chr2    3    C    7
    chr2    4    G    7
    chr2    5    G    7
    chr2    6    A    7
    chr2    73                       T    5
    chr2    74                       A    5
    chr2    75                       T    5
    chr2    76                       T    5
    chr2    77             C    6    C    5
    chr2    78             G    6    T    5
    chr2    79             T    7
    chr2    80             C    7
    chr2    81             G    7
    chr2    82             A    8
    chr2    83             T    8
    chr2    84             A    9

Example with missing columns
****************************

Given the following input files:

FILE 1::

    1   A
    2   B   b
    4   C   c
    5   D
    6   E   e

FILE 2::

    1   M   m
    2   N
    3   O   o
    4   P   p
    5   Q
    7   R   r

if we join only column 3 using column 1 as the hinge and with a fill value of '0', this is what will be output::

    1   0   m
    2   b   0
    3   0   o
    4   c   p
    5   0   0
    6   e   0
    7   0   r

Row 5 appears in both files with the missing column, so it's got nothing but fill values in the output file.

Compute an expression on every row
##################################

This tool computes an expression for every row of a dataset and appends the result as a new column (field).

Columns are referenced with c and a number. For example, c1 refers to the first column of a tab=delimited file
c3=c2 will add a length column to the dataset if c2 and c3 are start and end position

Example
*******

If this is your input::

    chr1  151077881  151077918  2  200  =
    chr1  151081985  151082078  3  500  +

computing "c4*c5" will produce::

    chr1  151077881  151077918  2  200  =   400.0
    chr1  151081985  151082078  3  500  +  1500.0

if, at the same time, "Round result?" is set to YES results will look like this::

    chr1  151077881  151077918  2  200  =   400
    chr1  151081985  151082078  3  500  +  1500

You can also use this tool to evaluate expressions. For example, computing "c3>#c2" for Input will result in the following::

    chr1  151077881  151077918  2  200  =  True
    chr1  151081985  151082078  3  500  +  True

or computing "type(c2)##type('') for Input will return::

    chr1  151077881  151077918  2  200  =  False
    chr1  151081985  151082078  3  500  +  False

Concatenate multiple datasets tail=to=head
##########################################

Convert delimiters to TAB
#########################

Converts all delimiters of a specified type into TABs. Consecutive characters are condensed. For example, if columns are separated by 5 spaces they will converted into 1 tab.

Example
*******

Input file::

    chrX||151283558|151283724|NM_000808_exon_8_0_chrX_151283559_r|0|=
    chrX|151370273|151370486|NM_000808_exon_9_0_chrX_151370274_r|0|=
    chrX|151559494|151559583|NM_018558_exon_1_0_chrX_151559495_f|0|+
    chrX|151564643|151564711|NM_018558_exon_2_0_chrX_151564644_f||||0|+

Converting all pipe delimiters of the above file to TABs will get::

    chrX  151283558  151283724  NM_000808_exon_8_0_chrX_151283559_r  0  =
    chrX  151370273  151370486  NM_000808_exon_9_0_chrX_151370274_r  0  =
    chrX  151559494  151559583  NM_018558_exon_1_0_chrX_151559495_f  0  +
    chrX  151564643  151564711  NM_018558_exon_2_0_chrX_151564644_f  0  +

Cut columns from a table
########################

This tool selects (cuts out) specified columns from the dataset.

Columns are specified as c1, c2, and so on. Column count begins with 1. 
Columns can be specified in any order (e.g., c2,c1,c6)
If you specify more columns than actually present = empty spaces will be filled with dots

Example
******* 

Input dataset (six columns: c1, c2, c3, c4, c5, and c6)::

    chr1 10   1000  gene1 0 +
    chr2 100  1500  gene2 0 +

cut on columns "c1,c4,c6" will return::

    chr1 gene1 +
    chr2 gene2 +

cut on columns "c6,c5,c4,c1" will return::

    + 0 gene1 chr1
    + 0 gene2 chr2

cut on columns "c8,c7,c4" will return::

    . . gene1
    . . gene2

Merge Columns together
######################

This tool merges columns together. Any number of valid columns can be merged in any order.

Example
*******

Input dataset (five columns: c1, c2, c3, c4, and c5)::

    1 10   1000  gene1 chr
    2 100  1500  gene2 chr

merging columns "c5,c1" will return::

    1 10   1000  gene1 chr chr1
    2 100  1500  gene2 chr chr2

Note that all original columns are preserved and the result of merge is added as the rightmost column.

Column Regex Find And Replace
#############################

This tool goes line by line through the specified input file and if the text in the selected column matches a specified regular expression pattern replaces the text with the corresponding specified replacement.

Example
*******

To remove the chr part of the reference sequence name in the first column of this GFF file::

    chr1   bed2gff CCDS1000.1_cds_0_0_chr1_148325916_f     148325916       148325975       .       +       .       score "0";
    chr21  bed2gff CCDS13614.1_cds_0_0_chr21_32707033_f    32707033        32707192        .       +       .       score "0";
    chrX   bed2gff CCDS14606.1_cds_0_0_chrX_122745048_f    122745048       122745924       .       +       .       score "0";

Setting::

    using column: c1
    Find Regex: chr([0=9]+|X|Y|M[Tt]?)
    Replacement: \1

produces::

    1    bed2gff CCDS1000.1_cds_0_0_chr1_148325916_f     148325916       148325975       .       +       .       score "0";
    21   bed2gff CCDS13614.1_cds_0_0_chr21_32707033_f    32707033        32707192        .       +       .       score "0";
    X    bed2gff CCDS14606.1_cds_0_0_chrX_122745048_f    122745048       122745924       .       +       .       score "0";

This tool uses Python regular expressions with the re.sub() function. More information about Python regular expressions can be found `here <http://docs.python.org/library/re.html>`_.

The regex ``chr([0=9]+|X|Y|M)`` means start with text chr followed by either: one or more digits, or the letter X, or the letter Y, or the letter M (optionally followed by a single letter T or t). Note that the parentheses ``()`` capture patterns in the text that can be used in the replacement text by using a backslash=number reference: ``\1``

Regex Find And Replace
######################

This tool goes line by line through the specified input file and replaces text which matches the specified regular expression patterns with its corresponding specified replacement.

This tool uses Python regular expressions. More information about Python regular expressions can be found `here <http://docs.python.org/library/re.html>`_

Example
*******

To convert an Ilumina FATSQ sequence id from the CAVASA 8 format::

    @EAS139:136:FC706VJ:2:2104:15343:197393 1:Y:18:ATCACG
    GGGTGATGGCCGCTGCCGATGGCGTCAAATCCCACC
    +EAS139:136:FC706VJ:2:2104:15343:197393 1:Y:18:ATCACG
    IIIIIIIIIIIIIIIIIIIIIIIIIIIIII9IG9IC

To the CASAVA 7 format::

    @EAS139_FC706VJ:2:2104:15343:197393#0/1
    GGGTGATGGCCGCTGCCGATGGCGTCAAATCCCACC
    +EAS139_FC706VJ:2:2104:15343:197393#0/1
    IIIIIIIIIIIIIIIIIIIIIIIIIIIIII9IG9IC

Use Settings::

    Find Regex: ^([@+][A=Z0=9]+):\d+:(\S+)\s(\d).*$
    Replacement: \1_\2#0/\3


Note that the parentheses ``()`` capture patterns in the text that can be used in the replacement text by using a backslash=number reference: ``\1``

The regex ``^([@+][A=Z0=9]+):d+:(S+) (d).*$`` means:

= ``^``  = start the match at the beginning of the line of text
= ``(``  = start a group (1), that is a string of matched text, that can be back=referenced in the replacement as \1
= ``[@+]``  = matches either a @ or + character
= ``[A=Z0=9]+``  = matches an uppercase letter or a digit, the plus sign means to match 1 or more such characters
= ``)``  = end a group (1), that is a string of matched text, that can be back=referenced in the replacement as \1
= ``:\d+:``   = matches a colon followed by one or more digits followed by a colon character
= ``(\S+)``  = matches one or more non=whitespace charcters,  the enclosing parentheses make this a group (2) that can back=referenced in the replacement text as \2
= ``\s``  = matches a whitespace character
= ``(\d)``  = matches a single digit character,  the enclosing parentheses make this a group (3) that can back=referenced in the replacement text as \3
= ``.*`` = dot means match any character, asterisk means zero more more matches
= ``$``  = the regex must match to the end of the line of text

Remove beginning of a file
##########################

This tool removes a specified number of lines from the beginning of a dataset.

Example
*******

Input File::

    chr7  56632  56652   D17003_CTCF_R6  310  +
    chr7  56736  56756   D17003_CTCF_R7  354  +
    chr7  56761  56781   D17003_CTCF_R4  220  +
    chr7  56772  56792   D17003_CTCF_R7  372  +
    chr7  56775  56795   D17003_CTCF_R4  207  +

After removing the first 3 lines the dataset will look like this::

    chr7  56772  56792   D17003_CTCF_R7  372  +
    chr7  56775  56795   D17003_CTCF_R4  207  +

Select first lines from a dataset
#################################

This tool outputs specified number of lines from the beginning of a dataset

Example
*******

Selecting 2 lines from this::

    chr7  56632  56652  D17003_CTCF_R6  310  +
    chr7  56736  56756  D17003_CTCF_R7  354  +
    chr7  56761  56781  D17003_CTCF_R4  220  +
    chr7  56772  56792  D17003_CTCF_R7  372  +
    chr7  56775  56795  D17003_CTCF_R4  207  +

will produce::

    chr7  56632  56652  D17003_CTCF_R6  310  +
    chr7  56736  56756  D17003_CTCF_R7  354  +

Select last lines from a dataset
################################

This tool outputs specified number of lines from the end of a dataset

Example
*******

Input File::

    chr7    57134   57154   D17003_CTCF_R7  356     =
    chr7    57247   57267   D17003_CTCF_R4  207     +
    chr7    57314   57334   D17003_CTCF_R5  269     +
    chr7    57341   57361   D17003_CTCF_R7  375     +
    chr7    57457   57477   D17003_CTCF_R3  188     +

Show last two lines of above file. The result is::

    chr7    57341   57361   D17003_CTCF_R7  375     +
    chr7    57457   57477   D17003_CTCF_R3  188     +

Split file according to the values of a column
##############################################

This tool splits a file into different smaller files using a specific column. It will work like the group tool, but every group is saved to its own file.

Example
*******

Splitting on column 5 from this::

    chr7  56632  56652  cluster 1
    chr7  56736  56756  cluster 1
    chr7  56761  56781  cluster 2
    chr7  56772  56792  cluster 2
    chr7  56775  56795  cluster 2

will produce 2 files with different clusters::

    chr7  56632  56652  cluster 1
    chr7  56736  56756  cluster 1

::

    chr7  56761  56781  cluster 2
    chr7  56772  56792  cluster 2
    chr7  56775  56795  cluster 2

Unique occurrences of each record
#################################

This tool returns all unique lines using the 'sort =u' command. The input file needs to be tab separated. 

Example
*******

Input file::

    chr1   10  100  gene1
    chr1  105  200  gene2
    chr1   10  100  gene1
    chr2   10  100  gene4
    chr2 1000 1900  gene5
    chr3   15 1656  gene6
    chr2   10  100  gene4

Unique lines will result in::

    chr1   10  100  gene1
    chr1  105  200  gene2
    chr2   10  100  gene4
    chr2 1000 1900  gene5
    chr3   15 1656  gene6