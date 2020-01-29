README

OVERVIEW:
For this assignment, we put most of our functionality within the main function. We thought
it would work because the functionality was relatively simple and relied mostly on command
line arguments.

We began by getting the name of the file from the -f flag. We only put functionality inside of an if case where we do have "-f" in our argument list because without -f (and a file
name following -f), there would be no file to even open, which means we would have no file
from which to read. Therefore, we only do tasks in the code if this flag exists and we
can get a file from the command line.

Once we have the file, we have to read to the first 500 lines or the entire file if the
file is less than 500 lines long (as specified by the instructions) to get the schema. Our
strategy was to read these lines and then find the line with the most columns. We had created two dictionary objects, total_type, which is used to keep track of the values of each
column within those first <500 lines, and col_types, which we used to enforce our schema.
We also had an int, max_col, which we updated as we read each line to represent the maximum
number of columns (ie: the number of columns the longest row has). From there, we used the
max_col to keep track of the columns, where the key was the column index, and the value
of each entry was an array that contained the row value at the column corresponding to the key (ie: row 0, column 0, appended while reading through each line). We then checked each
array value, and if we found any string in the array, we set col_types at that index to "STRING," for instance. We then continued to loop through each value at the next indices
until col_types was filled out and gave us the correct column schema.

After we found the schema, we read the entire file (or the subsection of the file given to
us starting at -from and ending -len bytes later) and checked whether it fit. If it did not suit the schema at any point, or if the value was invalid (say, for example, we had a
float value of '+ 2. 4' or a string value like 'hello world' without quotes around it, we
replaced that value in the row with the empty string and continued reading through the file.

We checked the arguments from the command line and tailored our responses to each case,
conferring with the schema to print out the column type, as well as check if a value was
missing at a given column at a given offset (row), and for printing out the value at a
given index and offset (it's possible the value is missing due to not having a value to
begin with, being an invalid value, not matching the schema, or the index/offset being out
of bounds).

In an effort to clean up our code and avoid repetition, we wrote functions for isString,
isBool, isInt, and isFloat to check the types of values we read. We then used these functions to write matchesSchema, which takes in a value and an index (A column number) in order
to match the value type with the correct column type. The function isValid checks whether
a value is invalid or not, whether it has whitespace in the center of the value when the
value itself is not a string value or wrapped in double quotes already. We then used these
functions to check validity of values and figure out whether we should return an empty
string or if we should return actual non-empty values.

TESTING:
For testing, we used the example given to us on the assignment page. We then added columns
and rows of our own and tested different value types. We also created our own file, initially 10,000 lines long, and then 15,000 lines to see if we could continue to read and return
the correct values (albeit repetitive files with the same 2-3 lines).

NEXT STEPS:
For our next steps, we would like to abstract more. Our philosophy was to simply get the
code working, but we had made mistakes with timing. While we have checks for types, we
would like to increase modularity, for instance, having separate functions to find the
schema and to read the file and use helper functions for the schema, too, instead of
putting so much into the main function.  
