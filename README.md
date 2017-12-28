# Jison
Jison, a Tiny All-Powerful Json Parser

Jison is a simple parser for Json manipulation. It parses a Json string into a dictionary with syntax check like what Python's builtin method `json.loads()` does, but beside this it provides many additional features:

(the `object` refers any Json key:value pair)
1. String search under tree structure & hierarchical search
   (requires a 3rd party string match function as parameter to work)
2. Single Json object acquisition
   (get one Json object returned as dict)
3. Multiple Json object acquisition
   (get all Json objects under any depth with same key value and return them as a list of dictionary)
4. Json object deletion
   (delete any single Json object)
5. Json object replacement
   (find and replace any single Json object)
   
 
