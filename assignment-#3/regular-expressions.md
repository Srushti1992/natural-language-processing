# Python RegEx
Python has a module named <pre>re</pre> to work with regular expressions. To use it, we need to import the module.

import re
The module defines several functions and constants to work with RegEx.
<hr/>

## re.findall()
The re.findall() method returns a list of strings containing all matches.
<hr/>
Example 1: re.findall()

<pre>

# Program to extract numbers from a string

import re

string = 'hello 12 hi 89. Howdy 34'
pattern = '\d+'

result = re.findall(pattern, string) 
print(result)

# Output: ['12', '89', '34']
</pre>

If the pattern is not found, re.findall() returns an empty list.
<hr/>

re.split()
The re.split method splits the string where there is a match and returns a list of strings where the splits have occurred.

<hr/>

Example 2: re.split()

<pre>
import re

string = 'Twelve:12 Eighty nine:89.'
pattern = '\d+'

result = re.split(pattern, string) 
print(result)

# Output: ['Twelve:', ' Eighty nine:', '.']
</pre>
If the pattern is not found, re.split() returns a list containing the original string.

<hr/>
You can pass maxsplit argument to the re.split() method. It's the maximum number of splits that will occur.

<pre>
import re

string = 'Twelve:12 Eighty nine:89 Nine:9.'
pattern = '\d+'

# maxsplit = 1
# split only at the first occurrence
result = re.split(pattern, string, 1) 
print(result)

# Output: ['Twelve:', ' Eighty nine:89 Nine:9.']
</pre>
By the way, the default value of maxsplit is 0; meaning all possible splits.
<hr/>

re.sub()
The syntax of re.sub() is:
<pre>
re.sub(pattern, replace, string)
</pre>
The method returns a string where matched occurrences are <kbd>replaced</kbd> with the content of replace variable.
<hr/>

## Example 3: re.sub()

<pre>
# Program to remove all whitespaces
import re

# multiline string
string = 'abc 12\
de 23 \n f45 6'

# matches all whitespace characters
pattern = '\s+'

# empty string
replace = ''

new_string = re.sub(pattern, replace, string) 
print(new_string)

# Output: abc12de23f456
</pre>
If the pattern is not found, re.sub() returns the original string.
<hr/>

You can pass <kbd>count</kbd> as a fourth parameter to the <kbd>re.sub()</kbd> method. If omited, it results to 0. This will replace all occurrences.

<pre>
import re

# multiline string
string = 'abc 12\
de 23 \n f45 6'

# matches all whitespace characters
pattern = '\s+'
replace = ''

new_string = re.sub(r'\s+', replace, string, 1) 
print(new_string)

# Output:
# abc12de 23
# f45 6
</pre>
<hr/>

## re.subn()
The <kbd>re.subn()</kbd> is similar to <kbd>re.sub()</kbd> except it returns a tuple of 2 items containing the new string and the number of substitutions made.
<hr/>

## Example 4: re.subn()
<pre>
# Program to remove all whitespaces
import re

# multiline string
string = 'abc 12\
de 23 \n f45 6'

# matches all whitespace characters
pattern = '\s+'

# empty string
replace = ''

new_string = re.subn(pattern, replace, string) 
print(new_string)

# Output: ('abc12de23f456', 4)
</pre>
<hr/>

## re.search()
The re.search() method takes two arguments: a pattern and a string. The method looks for the first location where the RegEx pattern produces a match with the string.

If the search is successful, re.search() returns a match object; if not, it returns None.
<pre>
match = re.search(pattern, str)
</pre>
<hr/>

## Example 5: re.search()

</pre>
import re

string = "Python is fun"

# check if 'Python' is at the beginning
match = re.search('\APython', string)

if match:
  print("pattern found inside the string")
else:
  print("pattern not found")  

# Output: pattern found inside the string
Here, match contains a match object.
</pre>
<hr/>

## Match object
You can get methods and attributes of a match object using dir() function.

Some of the commonly used methods and attributes of match objects are:
<hr/>

### match.group()
The group() method returns the part of the string where there is a match.

## Example 6: Match object
<pre>
import re

string = '39801 356, 2102 1111'

# Three digit number followed by space followed by two digit number
pattern = '(\d{3}) (\d{2})'

# match variable contains a Match object.
match = re.search(pattern, string) 

if match:
  print(match.group())
else:
  print("pattern not found")

# Output: 801 35
</pre>
Here, match variable contains a match object.

Our pattern (\d{3}) (\d{2}) has two subgroups (\d{3}) and (\d{2}). You can get the part of the string of these parenthesized subgroups. Here's how:
<pre>
>>> match.group(1)
'801'

>>> match.group(2)
'35'
>>> match.group(1, 2)
('801', '35')

>>> match.groups()
('801', '35')
</pre>

<hr/>

### match.start(), match.end() and match.span()
The start() function returns the index of the start of the matched substring. Similarly, end() returns the end index of the matched substring.
<pre>
>>> match.start()
2
>>> match.end()
8
</pre>
The span() function returns a tuple containing start and end index of the matched part.

<pre>
>>> match.span()
(2, 8)
</pre>

### match.re and match.string
The re attribute of a matched object returns a regular expression object. Similarly, string attribute returns the passed string.

<pre>
>>> match.re
re.compile('(\\d{3}) (\\d{2})')

>>> match.string
'39801 356, 2102 1111'
</pre>
<hr/>

## Using r prefix before RegEx
When r or R prefix is used before a regular expression, it means raw string. For example, '\n' is a new line whereas r'\n' means two characters: a backslash \ followed by n.

Backlash \ is used to escape various characters including all metacharacters. However, using r prefix makes \ treat as a normal character.

<hr/>

## Example 7: Raw string using r prefix

<pre>
import re

string = '\n and \r are escape sequences.'

result = re.findall(r'[\n\r]', string) 
print(result)

# Output: ['\n', '\r']
</pre>
<hr/>
