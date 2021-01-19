# Python File Operations

### Current directory

```python
import os
os.getcwd()
```

### YAML read/write

```python
import yaml

data = {
    'fruit': {
        'apples': '',
        'oranges': '',
    }
    'instruments': {
        'piano': '',
        'guitar': '',
    }
}

with open('db_details.yml', 'w') as outfile:
    yaml.dump(data, outfile, default_flow_style=False)

with open("/Users/anthony/Documents/Projects/Databases/db_details.yml", 'r') as stream:
    db_details = yaml.safe_load(stream)
```

### JSON read/write

```python
import json

data = {
    'fruit': {
        'apples': '',
        'oranges': '',
    }
    'instruments': {
        'piano': '',
        'guitar': '',
    }
}

with open('read.json', 'w') as outfile:
    json.dump(data, outfile, sort_keys=True, indent=4)  # sort_keys, indent used to prettify 

with open('read.json') as data_file:    
    data = json.load(data_file)
```