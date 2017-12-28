# Jison
Jison, a Tiny All-Powerful Json Parser (Python3.6)

Jison is a simple but powerful parser for Json manipulation. It parses a Json string into a dictionary with syntax check like what Python's builtin method `json.loads()` does, but beside this it provides many additional features:

(the `object` refers any Json `key:value` pair)
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

## Examples
Assume `sample.json` has following content:
```json
{"sample":"Jison","params":[{"key1":"main","key2":"client","key3":"0/0","key4":0,"key5":2}, {"key1":"sub","key2":"parent","c1":null,"c2":true}],"id":1}
```

```python
# initialization can be a Json string or from `.json` file
jison = Jison()
jison.load_json(file_name='sample.json')
```

```python
# get dictionary from Json
print(jison.parse())
""" output
{'id': 1,
 'params': [{'key1': 'main',
             'key2': 'client',
             'key3': '0/0',
             'key4': 0,
             'key5': 2},
            {'c1': None, 'c2': True, 'key1': 'sub', 'key2': 'parent'}],
 'sample': 'Jison'}
"""

# get single Json object
print(jison.get_single_object(obj_name='params'))
""" output
{'params': [{'key1': 'main',
             'key2': 'client',
             'key3': '0/0',
             'key4': 0,
             'key5': 2},
            {'c1': None, 'c2': True, 'key1': 'sub', 'key2': 'parent'}]}
"""

# get multiple Json objects
print(jison.get_multi_object(obj_name='key1'))
""" output
[{'key1': 'main'}, {'key1': 'sub'}]
"""

# delete Json object



```


