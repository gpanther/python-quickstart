# Python Quickstart

Premise: you know programming but know no (or only a little of) Python.

**Note**: This is for Python 3, *NOT* legacy Python (2.7)

## Introduction

- Python: a slow, statically typed (but checked at runtime) scripting language.
- Sorry for choosing it, here are some steps to make it less painful
- YMHH (You Might Have Heard):
  - whitespace sensitive
  - slow because of the GIL

## Virtual environments, packages

```bash
mkdir python-quickstart
cd python-quickstart
pyvenv env # Not relocable !!!
source env/bin/activate
# our just
./env/bin/python
./env/bin/pip
```

`print("Hello world!")`

Packages are pulled from [PyPi](https://pypi.python.org/pypi/pudb) (not to be confused with [PyPy](http://pypy.org/) an alternative to CPython)

```
pip install pudb
pip install pudb==2016.2
pip install pudb>=2016.0
```

```
# requirements.txt
requests==2.13.0
# requirements_dev.txt
-r requirements.txt
pudb==2016.2
# can also contain URLs
# command line:
pip install -r requirements_dev.txt
```

```
pip freeze > requirements_frozen.txt
pip list --outdated --format=columns
```

- [Default `.gitignore` for Python](https://github.com/github/gitignore/blob/master/Python.gitignore):

```
__pycache__/
*.py[cod]
...
env/
...
htmlcov/
.tox/
.coverage
.coverage.*
...
```

* Let's talk about native packages. Some strategies:
  * Hope that the packager included wheels
  * Install from package manager and _afterwards_ do `pyvenv --system-site-packages env`
  * Have a complete build-chain ready (`build-essential`, `python3-dev`, `libpq-dev`, ...)

## Booleans, numbers, strings, lists, tuples, dicts, sets, range

```python
None
```

```python
True
False
```

```python
1234
0o777
0b101
10**123
10/3
10//3
```

```python
type(1234)
str(1234)
repr(1234)
hash(1234)
id(1234)
```

```python
'foo\tbar'
"foo\x09bar"
"""foo"""
'''foo'''
r'foo\tbar'
'foo%d: %.2f (%r)' % (1, 2, 3)
'foo{0}'.format(1)
b'foo'.decode('utf-8')
```

```python
[]
[1, "abc", 2]
[1, "abc", 2] + [3]
list((1, 2, 3))
l = [1, "abc", 2]
l[0]
len(l)
l[-1]
l[::2]
l[::-1]
del l[1]
(1, 2)
(1,)
(1, 2)[::-1]
```

```python
{1: 2, "foo": "bar"}
dict(fiz=2, foo="bar")
d = {1: 2, "foo": "bar"}
d[1]
d[2]
d.keys()
d.values()
d.items()
1 in d
2 not in d
d.update({1: 2, 3: 5})
d.get(2)
d.pop(2)
d.pop(2, None)
d.pop(1)
d.pop(1)
del d['foo']
{1, 2, 3.1415}
set((1, 2, 3.1415))
1 in {1, 2}
{}
```

```python
range(0, 10)
list(range(0, 10))
list(range(0, 10, 3))
```

More: https://docs.python.org/3.5/library/stdtypes.html

## Comments

```python
# this is a comment
'''
This is a multi-line comment - almost
'''
```

## Ordered dicts, frozensets, named touple, counter

`import collections`

```python
counter = collections.Counter()
counter.update((1, 1, 1, 1))
counter.update({1: 4})
counter[1] = 0
counter[42]
```

```python
collections.OrderedDict
```

```python
dd = collections.defaultdict(list)
dd[1].append(5)
```

```python
# from https://docs.python.org/3.5/library/collections.html#collections.namedtuple
Point = collections.namedtuple('Point', ['x', 'y'])
```

## Control structures

```python
if a:
  pass
elif b:
  pass
else:
  pass
```

```python
for i in {1: 2, 3: 4}: print(i)
for i in {1: 2, 3: 4}.items(): print(i)
for k, v in {1: 2, 3: 4}.items(): print(k + v)
for k, v in {1: 2, 3: 4}.items(): print('%s -> %s' % (k, v))
for k, _ in {1: 2, 3: 4}.items(): print(k)
for _, _ in {1: 2, 3: 4}.items(): print("Hello")
```

```python
while True:
  break / continue
```

```python
for i in (1, 2, 3):
  if i == 2:
    print("Found!")
    break;
else:
  print("Not found!")
```

```python
for i in enumerate((1, 2, 3)):
  print(i)
```

https://docs.python.org/3.5/library/functions.html

## Modules

```python
dir/__init__.py
import dir
import dir.foo
from dir import foo
```

## Testing, TDD

```python
import unittest


class TestTest(unittest.TestCase):
    def testMe(self):
        self.assertEqual(1, 2)


if __name__ == '__main__':
    unittest.main()
```

```bash
python -m unittest discover tests
python -m unittest test
python -m unittest -f test
```

```bash
pip install pytest
```

```python
def testMe():
    assert 1 == 2
```

```python
def testMe():
    assert 1 == 2
```

```python
def inc(x):
    return x + 1

def testAnswer():
    assert inc(3) == 5
```

## Function, decorators

* Named parameters

```python
def sum(a, b):
    return a + b


print(sum(b=1, a=2))
```

* "varargs"

```python
def dump(*args, **kwargs):
    print(args)
    print(kwargs)


dump(1, 2, 3, 4, foo='bar')
```

* Closures

```python
def incrementFactory(w):
    def inc(x):
        return x + w
    return inc


inc = incrementFactory(5)
print(inc(1))
```

* Lambdas / anonymous functions

```python
def incrementFactory(w):
    return lambda x: x + w


inc = incrementFactory(5)
print(inc(1))
```

```python
import functools


def sum(a, b):
    return a + b


def incrementFactory(w):
    return functools.partial(sum, w)

inc = incrementFactory(5)
print(inc(1))
```
* decorators

```python
def decorate(f):
    def decorated(*args, **kwargs):
        print('Before!')
        f(*args, **kwargs)
        print('After!')
    return decorated


@decorate
def test(*args):
    return sum(args)


print(test(1, 2, 3))
```

```python
import functools


def decorate(f):
    @functools.wraps(f)
    def decorated(*args, **kwargs):
        print('Before!')
        try:
            return f(*args, **kwargs)
        finally:
            print('After!')
    return decorated


@decorate
def test(*args):
    return sum(args)


print(test(1, 2, 3))
```

## Mocking

## Exceptions

## Classes

* Inheritance
* Magic methods

## List/Dict/Set comprehensions

## Generators

* [Generator Tricks](http://www.dabeaz.com/generators/index.html)
* [A Curious Course on Coroutines and Concurrency](http://dabeaz.com/coroutines/)

## Itertools and more itertools

## Context managers

## Serialization

* JuJ: Just Use Json
* Pickle and YAML are both security risks!

## Static analyzers, coverage

## Debugging

## Logging

## WSGI, Flask

- WSGI: web standard gateway interface
- "WSGI servers": uWSGI, mod_wsgi, etc
- [Flask](http://flask.pocoo.org/): very basic web framework.
- Uses thread-local variables like `flask.request`
- Has an integrated debugger
- Watch out for security! Doesn't even provide CSRF protection by default: http://flask.pocoo.org/snippets/3/
- Probably should be checked for https://www.owasp.org/index.php/Top_10_2013-Top_10
- For Jinja2: make sure that autoescape is enabled

```python
import flask
app = flask.Flask(__name__)


@app.route("/")
def hello():
    return 1 + "Hello World!"


if __name__ == "__main__":
    app.run(debug=True)
```

## Some well-known modules:

* [requests](http://docs.python-requests.org/en/master/)
* [numpy](http://www.numpy.org/) - also [Intel Distribution for Python](https://software.intel.com/en-us/intel-distribution-for-python)
* [youtube-dl](https://pypi.python.org/pypi/youtube_dl)
* cProfile
* [objgraph](https://pypi.python.org/pypi/objgraph)
* ...

## Podcasts

* [Talk Python to Me](https://talkpython.fm/)
* [Podcast.\_\_init\_\_](https://pythonpodcast.com/)
* [Python Bytes](https://pythonbytes.fm/)

## Other tidbits:

* [PyVideo.org](http://pyvideo.org/)
* Python 3.5 type hints
* Good editors: PyCharm, PyDev
* [/r/Python](https://www.reddit.com/r/Python/) and [/r/PythonTips](https://www.reddit.com/r/pythontips/)
* Code formatting guidelines (style guides):
  * PEP8: https://www.python.org/dev/peps/pep-0008/
  * Google Style Guide: https://google.github.io/styleguide/pyguide.html
* `from __future__ import ...` - see the [\__future\__ module](https://docs.python.org/3.6/library/__future__.html)
* `# -*- coding: <encoding-name> -*-`
* Other alternative Python runtimes: Jypton, IronPython

# Good luck!
