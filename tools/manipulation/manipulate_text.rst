.. _framework-tools-manipulation-manipulate-file:

================
Manipulate files
================

.. _framework-tools-manipulation-manipulate-file-paste:

Paste two files side by side
############################

This tool merges two datasets side by side. If the first (left) dataset contains column assignments such as chromosome, start, end and strand, these will be preserved. However, if you would like to change column assignments, click the pencil icon in the history item.

.. _framework-tools-manipulation-manipulate-file-select-random:

Select random lines from a file
###############################

This tool selects N random lines from a file, with no repeats, and preserving ordering.

.. _framework-tools-manipulation-manipulate-file-wc:

Line/Word/Character count of a dataset
######################################

This tool outputs counts of specified attributes (lines, words, characters) of a dataset.

.. _framework-tools-manipulation-manipulate-filter:

Filter data on any column using simple expressions
##################################################

The filter tool allows you to restrict the dataset using simple conditional statements.


.. _framework-tools-manipulation-manipulate-file-sort:

Sort data in ascending or descending order
##########################################

This tool sorts the dataset on any number of columns in either ascending or descending order.

Numerical sort orders numbers by their magnitude, ignores all characters besides numbers, and evaluates a string of numbers to the value they signify.
General numeric sort orders numbers by their general numerical value. Unlike the numerical sort option, it can handle numbers in scientific notation too.
Alphabetical sort is a phonebook type sort based on the conventional order of letters in an alphabet. Each nth letter is compared with the nth letter of other words in the list, starting at the first letter of each word and advancing to the second, third, fourth, and so on, until the order is established. Therefore, in an alphabetical sort, 2 comes after 100 (1 < 2).

.. _framework-tools-manipulation-manipulate-file-select-lines:

Select lines that match an expression
#####################################

The select tool searches the data for lines containing or not containing a match to the given pattern. Regular Expression is introduced in this tool. A Regular Expression is a pattern describing a certain amount of text.

- ``( ) { } [ ] . * ? + ^ $`` are all special characters. ``\`` can be used to "escape" a special character, allowing that special character to be searched for.
- ``\A`` matches the beginning of a string(but not an internal line).
- ``\d`` matches a digit, same as [0=9].
- ``\D`` matches a non=digit.
- ``\s`` matches a whitespace character.
- ``\S`` matches anything BUT a whitespace.
- ``\t`` matches a tab.
- ``\w`` matches an alphanumeric character.
- ``\W`` matches anything but an alphanumeric character.
- ``( .. )`` groups a particular pattern.
- ``\Z`` matches the end of a string(but not a internal line).
- ``{ n or n, or n,m }`` specifies an expected number of repetitions of the preceding pattern.
- ``{n}`` The preceding item is matched exactly n times.
- ``{n,}`` The preceding item is matched n or more times.
- ``{n,m}`` The preceding item is matched at least n times but not more than m times.
- ``[ ... ]`` creates a character class. Within the brackets, single characters can be placed. A dash (=) may be used to indicate a range such as a=z.
- ``.`` Matches any single character except a newline.
- ``*`` The preceding item will be matched zero or more times.
- ``?`` The preceding item is optional and matched at most once.
- ``+`` The preceding item will be matched one or more times.
- ``^`` has two meaning: = matches the beginning of a line or string. = indicates negation in a character class. For example, [^...] matches every character except the ones inside brackets.
- ``$`` matches the end of a line or string.
- ``|`` Separates alternate possibilities.

.. _framework-tools-manipulation-manipulate-file-join:

Join two Datasets side by side on a specified field
###################################################

This tool joins lines of two datasets on a common field. An empty string ("") is not a valid identifier. You may choose to include lines of your first input that do not join with your second input.

Columns are referenced with a number. For example, 3 refers to the 3rd column of a tab=delimited file.

.. _framework-tools-manipulation-manipulate-file-compare:

Compare two Datasets to find common or distinct rows
####################################################

This tool finds lines in one dataset that HAVE or DO NOT HAVE a common field with another dataset.

.. _framework-tools-manipulation-manipulate-file-group:

Group data by a column and perform aggregate operation on other columns
#######################################################################

This tool allows you to group the input dataset by a particular column and perform aggregate functions: Mean, Median, Mode, Sum, Max, Min, Count, Concatenate, and Randomly pick on any column(s).

The Concatenate function will take, for each group, each item in the specified column and build a comma delimited list. Concatenate Unique will do the same but will build a list of unique items with no repetition.

Count and Count Unique are equivalent to Concatenate and Concatenate Unique, but will only count the number of items and will return an integer.

If multiple modes are present, all are reported.

.. _framework-tools-manipulation-manipulate-file-add-column:

Add column to an existing dataset
#################################

You can enter any value and it will be added as a new column to your dataset

.. _framework-tools-manipulation-manipulate-file-change-case:

Change Case of selected columns
###############################

This tool selects specified columns from a dataset and converts the values of those columns to upper or lower case.

Columns are specified as c1, c2, and so on.
Columns can be specified in any order (e.g., c2,c1,c6)

.. _framework-tools-manipulation-manipulate-file-column-join:

Column Join
###########

This tool allows you to join several files with the same column structure into one file, removing certain columns if necessary. The user needs to select a 'hinge', which is the number of left=most columns to match on. They also need to select the columns to include in the join, which should include the hinge columns, too.

Note that the files are expected to have the same number of columns. If for some reason the join column is missing (this only applies to the last column(s)), the tool attempts to handle this situation by inserting an empty item (or the appropriate filler) for that column on that row. This could lead to the situation where a row has a hinge but entirely empty or filled columns, if the hinge exists in at least one file but every file that has it is missing the join column. Also, note that the tool does not distinguish between a file missing the hinge altogether and a file having the hinge but missing the column (in both cases the column would be empty or filled). There is an example of this below

.. _framework-tools-manipulation-manipulate-file-compute:

Compute an expression on every row
##################################

This tool computes an expression for every row of a dataset and appends the result as a new column (field).

Columns are referenced with c and a number. For example, c1 refers to the first column of a tab=delimited file
c3=c2 will add a length column to the dataset if c2 and c3 are start and end position

.. _framework-tools-manipulation-manipulate-file-convert:

Convert delimiters to TAB
#########################

Converts all delimiters of a specified type into TABs. Consecutive characters are condensed. For example, if columns are separated by 5 spaces they will converted into 1 tab.

.. _framework-tools-manipulation-manipulate-file-cut:

Cut columns from a table
########################

This tool selects (cuts out) specified columns from the dataset.

Columns are specified as c1, c2, and so on. Column count begins with 1.
Columns can be specified in any order (e.g., c2,c1,c6)
If you specify more columns than actually present = empty spaces will be filled with dots

.. _framework-tools-manipulation-manipulate-file-merge:

Merge Columns together
######################

This tool merges columns together. Any number of valid columns can be merged in any order.

.. _framework-tools-manipulation-manipulate-file-column-regex:

Column Regex Find And Replace
#############################

This tool goes line by line through the specified input file and if the text in the selected column matches a specified regular expression pattern replaces the text with the corresponding specified replacement.

.. _framework-tools-manipulation-manipulate-file-regex:

Regex Find And Replace
######################

This tool goes line by line through the specified input file and replaces text which matches the specified regular expression patterns with its corresponding specified replacement.

This tool uses Python regular expressions. More information about Python regular expressions can be found `here <http://docs.python.org/library/re.html>`_

.. _framework-tools-manipulation-manipulate-file-remove-beginning:

Remove beginning of a file
##########################

This tool removes a specified number of lines from the beginning of a dataset.

.. _framework-tools-manipulation-manipulate-file-select-beginning:

Select first lines from a dataset
#################################

This tool outputs specified number of lines from the beginning of a dataset

.. _framework-tools-manipulation-manipulate-file-select-tail:

Select last lines from a dataset
################################

This tool outputs specified number of lines from the end of a dataset

.. _framework-tools-manipulation-manipulate-file-split:

Split file according to the values of a column
##############################################

This tool splits a file into different smaller files using a specific column. It will work like the group tool, but every group is saved to its own file.

.. _framework-tools-manipulation-manipulate-file-unique:

Unique occurrences of each record
#################################

This tool returns all unique lines using the 'sort -u' command. The input file needs to be tab separated.

.. _framework-tools-manipulation-manipulate-file-normalize:

Normalize a dataset by row or column sum to obtain proportion or percentage
###########################################################################

This tool normalizes each row or column of a dataset by the row or column sum. The results can be in proportion or percentage.

The input file must be in tabular format with tab-separated columns. Only data will be used for normalization.

.. _framework-tools-manipulation-manipulate-file-extract:

Extract lines corresponding to minimum and maximum values of a column
#####################################################################

This tool extract a variable number of lines corresponding to minimum or maximum values of a chosen column.

The file must be in tabular format with tabular separated columns. To chosen column to extract minimum or maximum values must be data columns.
