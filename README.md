## Jison
Jison is a tiny all-Powerful Fluent Json parser (Python3.6)

Jison is a simple but powerful parser for Json manipulation. It parses a Json string into a dictionary with syntax check like what Python's builtin method `json.loads()` does, or write to file like `json.dump()`, but beside these it provides many additional features:

(the `object` refers any Json `key:value` pair)
1. Fluent dictionary of Json operation with dots `.`, for example: `json.key1.key2.key3[0].key4`
2. String search under tree structure & hierarchical search
   (requires a 3rd party string match function which returns int/float in [0, 1] as parameter to work)
3. Single Json object acquisition
   (get one Json object returned as dict)
4. Multiple Json object acquisition
   (get all Json objects under any depth with same key value and return them as a list of dictionary)
5. Json object deletion
   (delete any single Json object)
6. Json object replacement
   (find and replace any single Json object)

## Examples
Assuming `sample.json` has following content:
```json
{"id": 1,
 "params": [{"key1": "main",
             "key2": "client",
             "key3": "0/0",
             "key4": 0,
             "key5": 2},
            {"c1": null, "c2": true, "key1": "sub", "key2": "parent"}],
 "sample": "Jison"}
```

```python
# the initialization can be a Json string, a Python dict or from a `sample` + `.json` file
>>> jison = Jison(fp=open('sample.json', 'r'))
```

```python
# parse the Json and get dictionary
>>> json = jison.parse()
>>> json
""" result
{'id': 1,
 'params': [{'key1': 'main',
             'key2': 'client',
             'key3': '0/0',
             'key4': 0,
             'key5': 2},
            {'c1': None, 'c2': True, 'key1': 'sub', 'key2': 'parent'}],
 'sample': 'Jison'}
"""
```
---
```python
# fluent json operation
>>> json.params[0].key1
""" result
'main'
"""
```
---
```
# get single Json object in dictionary
>>> obj = jison.get_object(obj_name='params')
""" result
{'params': [{'key1': 'main',
             'key2': 'client',
             'key3': '0/0',
             'key4': 0,
             'key5': 2},
            {'c1': None, 'c2': True, 'key1': 'sub', 'key2': 'parent'}]}
"""
```
---
```
# get multiple Json objects
>>> objs = jison.get_multi_object(obj_name='key1')
""" result
[{'key1': 'main'}, {'key1': 'sub'}]
"""
```
---
```
# get a list of multiple Json objects, or None if no key is matched
>>> key1, key99, key2 = jison.get_multi_object(obj_name=['key1', 'key99, 'key2'])
""" result
key1:  [{'key1': 'main'}, {'key1': 'sub'}]
key99: None
key2:  [{'key2': 'client'}, {'key2': 'parent'}]
"""
```
---
```
# delete Json object and return a Jison instance, this operation will be written to file which the Json is loaded from
>>> new_json = jison.remove_object(obj_name='params').json
""" result
{'id': 1, 'sample': 'Jison'}
"""
```
---
```
# replace a Json object with another and return a Jison instance, this operation will be written to file which the Json is loaded from
>>> replaced_json = jison.replace_object(obj_name='params', new_chunk={"replaced": "new_data"}).json
""" result
{'id': 1, 'replaced': 'new_data', 'sample': 'Jison'}
"""
```
