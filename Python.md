Python is a high-level language, interpreted programming language known for dynamic typing, versatility 

python code is converted into machine code by compiler //machine code is low-level labguage that interacts with the hardware
when we install python there is no compiler but a interpreter // the interpreter converts it into byte code(low level)
interpreted means it is run line by line (due to t his it is slow as it is parsed line by line and therefore errors in the code are discovered when the interpreter raches the line with error and not beforehand like with compiled languages like c++)

id() is used to find the address at which a variable is stored in RAM

Logging is used to debug the code, to understand what lines the print statemnt is coming from
import logging
logging.basicConfig(level=logging.DEBUG, format='%(asctime)s %(message)s').......
logging.info(f"cost of x is {y}") // info is like print function

OR use loguru (from loguru import logger) and then logger.info(....) // simpler than above

For lists, the values in a list are stored in continuous memory in RAM. For such data structures, indexing is done(mostly zero-based indexing).
Some list methods - append(), extend() OR + (used to add two lists), insert(index_to_insert_at, data), pop(idx)-- by default deletes last element from the list and returns the element, index of the element to be deleted can be given as well, remove(element) -- deletes the first occurrence of the sprecified element

List Comprehension

[output for value in list if condition]
[output if condition else condition for value in list]


Dictionary methods -- keys() -- returns a list, values() -- returns a list, items() -- returns a list of tuples, get(key, default_value), update({key:value}), pop(key)
Another way to update a dict - 
a= {}
new = {}
final = {**a, **b} // updated dict

Dictionary Comprehension

{key:dict[key]+100 for key in dict} // increase all values by 100
{dict[key]+100 if key!='xyz' else dict[key] for key in dict}



Tuples

- tuple is ordered and immutable(cannot be changed)
- x = (1, 2, "abc", True)
- Some functions - count(val)-- return num of occurrence of that value, index(val) -- returns index of the first occurrence of value, + to add two or more tuples


Set

- unordered, immutable, cannot contain duplicate values, {} used to define a set but holds singular values instead of pairs in dict
- To create an empty set, set() 
- Use od sets in Maths - AUB, AnB, A-B/B-A, A symmetric difference B(removes common elements)
- Methods - a.union(b), a.intersection(b), a.isdisjoint(b), a.difference(b), add(val), remove(val), discard(val) -- remove gives error if val not present, discard doesnt give error


String

- ord(char) -- gives ASCII value for the character, count(char) -- return num of occurrences of character, 97-122(a-z), 65-90(A-Z), chr(ascii_val) -- returns the character with that ASCII, replace(old, new), 
