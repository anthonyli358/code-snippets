# Python

### Timer

```python
from contextlib import contextmanager
import time

@contextmanager
def timer(name):
    t0 = time.time()
    yield
    print(f'[{name}] done in {time.time() - t0:.0f} s')

# timer example
with timer('process stuff'):
    do_something()
```

### Create a decorator

```python
from functools import wraps

def some_decorator(f):
    @wraps(f)
    def decorated_function(*args, **kwargs):
        print(args, kwargs)
        # do things
        return f(*args, **kwargs)
    return decorated_function

@some_decorator
def do_sth(a, b, c):
    pass
```

### Exceptions

```python
import logging

try:
	pass
except Error as e:
	logging.exception("", exc_info=e)
```

### Unittests

```python
import unittests 

class TestCase(unittests.TestCase):
	def setUp(self):
		self.data = json.load()

	def test_data(self):
		tests = [({}, True), ({}, True)]
		for value, expected in tests:
			self.assertEqual(func(*value), expected)

if __name__=='__main__':
	unittest.main()
```