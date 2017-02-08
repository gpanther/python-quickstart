# Python Quickstart

Premise: you know programming but know no (or only a little of) Python.

**Note**: This is for Python 3, *NOT* legacy Python (2.7)

## Introduction

- Python: a slow, statically typed (but checked at runtime) scripting language.
- Sorry for choosing it, here are some steps to make it less painful
- YMHH (You Might Have Heard):
  - whitespace sensitive
  - slow because of the GIL
- Our friend <del>Google</del> [DuckDuckGo](https://duckduckgo.com/)

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

`import this`

`print("Hello World")`

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

def noReturn():
  pass

print(noReturn())
```

```python
True
False
```

```python
0o777
0b101
1234
0xABC
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
a, *b = [1, 2, 3]
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

```
(1, 2) < (1, 2, 3)
sorted((dict(a=1, b=2), dict(a=2, b=3)), key=lambda e: (e['a'], e['b']))
```

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


if 1 < 3 <= 3:
  pass

if all/any(...):
  ...

if a is (not) b:
  ...

if a in (not) b: # including strings
  ...

a = 0 if True else False
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

```python
import sys
sys.path
```

```python
import foo
foo.__file__
```

## Testing, TDD

```python
import unittest


class TestTest(unittest.TestCase):
    def testMe(self):
        self.assertEqual(1, 2)

# assertRaises
# assertRaisesRegex
# assertLogs
# assertIs
# assertIsNot
# assertIsNone
# assertIsNotNone
# assertIn
# assertNotIn
# assertIsInstance
# assertNotIsInstance

# self.maxDiff = None

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

* default parameters

```python
def foo(a=1, b=2):
    return a+b

print(foo(2))
print(foo(b=4))
```

**Don't use mutable default parameters - they are evaluated only once per module loading**

```python
# !!! WRONG !!!
def appendTo(a=[], b=[]):
    a += b
    return a

print(appendTo(b=[1]))
print(appendTo(b=[2]))
```

```python
# BETTER
def appendTo(a=[], b=[]):
    return a + b

print(appendTo(b=[1]))
print(appendTo(b=[2]))
```

```python
# BESTEST
def appendTo(a=None, b=None):
    a = a or []
    b = b or []
    return a + b

print(appendTo(b=[1]))
print(appendTo(b=[2]))
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

* side-effecting closures

1. Don't do it
2. See rule 1

```python
# !!! WON'T WORK !!!
def foo():
    called = False
    def do():
        called = True
    do()
    assert called

foo()
```

```python
def foo():
    called = [False]
    def do():
        called[0] = True
    do()
    assert called[0]

foo()
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

## Exceptions

```python
try:
    ...
except:
    ...


try:
    ...
except ValueError:
    ...


try:
    ...
except (ValueError, TypeError) as e:
    ...


try:
    ...
except ...:
    ...
finally:
    ...
    

raise ExceptionClass()
```

## Classes

* Don't overuse them

```python
class Foo(object):
    def foo(self):
        print(1)


def Fizz(object):
    def foo(self):
        print(2)

    def bar(self):
        print(3)


class Bar(Foo, Fizz):
    def foo(self, param):
        super().foo()
        print(4)

bar = Bar()
bar.foo(1)
bar.bar()
print(Bar.__mro__)
```

See: https://en.wikipedia.org/wiki/C3_linearization

```python
class Foo(object):
    def __init__(self, a, b):
        self._a = a
        self.__b = b


class Bar(Foo):
    def __init__(self, a):
        self.__b = a
        super().__init__(a, a)


b = Bar(2)
print(b.__dict__)
```

```python
class Foo(object):
    def do(self):
        print(self.PARAM)


class Bar(Foo):
    PARAM = 5


Bar().do()
```

```python
class Foo(object):
    def __init__(self, a):
        self.dodo()
        self.a = a


class Bar(Foo):
    def dodo(self):
        print(self.a)


Bar(1)
```

```python
def getValue():
    print('Getting value')
    return []


class Foo(object):
    a1 = getValue()

    def __init__(self):
        self.a2 = getValue()


f1 = Foo()
f2 = Foo()

assert f1.a1 is f2.a1
assert f1.a2 is not f2.a2
```

```python
class Foo(object):
    def iMethod(self):
        print(1)

    @staticmethod
    def sMethod():
        print(2)

    @classmethod
    def cMethod(cls):
        print(cls)


class Bar(Foo):
    def iMethod(self):
        super().iMethod()

    @staticmethod
    def sMethod():
        Foo.sMethod()

    @classmethod
    def cMethod(cls):
        super().cMethod()


b = Bar()
# b.iMethod()
# b.sMethod()
# b.cMethod()

# Bar.sMethod()
# Foo.sMethod()
# Bar.cMethod()
# Foo.cMethod()

# Foo.iMethod(None)
```

```python
class AttrDict(object):
    def __init__(self, **kwargs):
        for k, v in kwargs.items():
            setattr(self, k, v)


d = AttrDict(a=1, b=2)
print(d.a)
```

```python
class AttrDict(dict):
    __getattribute__ = dict.__getitem__


d = AttrDict(a=1, b=2)
print(d.a)
```

```python
class Klazz(object):
    def __call__(self, *args):
        return args


def fun(*args):
    return args


bubu = Klazz()
print(bubu(1, 2, 3))

bubu = fun
print(bubu(1, 2, 3))
```

* Magic methods: https://docs.python.org/3.5/reference/datamodel.html
* Meta classes
* From [Episode 12 of PythonBytes](https://pythonbytes.fm/episodes/show/12/expanding-your-python-mental-model-and-serving-millions-of-requests-per-second-with-python):
  * http://powerfulpython.com/blog/python-functions-arent-what-you-think/
  * http://nbviewer.jupyter.org/github/akittas/presentations/blob/master/pythess/tao_mro/tao_of_python.ipynb

## Scoping

1. Only functions introduce new scope
2. \*Weird exception for classes
3. after the outermost scope the builtins are searched

```python
u = 1

class Foo(object):
    u = 2

    class Bar(object):
        u = 3

        def do(self):
            u = 4
            print(u)

Foo.Bar().do()
```

\* Using nested classes to hide abstract superclass from unittest
\* The "Meta" class for Django

## Mocking

```python
import random


def randomPlusOne():
    return random.randint(0, 1000000) + 1
```

```python
from unittest import mock

import src


@mock.patch('src.random')
def testRandomPlusOne(random_mock):
    random_mock.randint.return_value = 1
    assert 2 == src.randomPlusOne()
```

`mock.Mock` / `mock.MagicMock`

## List/Dict/Set comprehensions

```python
[i**2 for i in range(0, 10) if i % 2 == 0]

{i**2 for i in range(0, 10) if i % 2 == 0}

{i: i**2 for i in range(0, 10) if i % 2 == 0}
```

## Generators

```python
def gen():
    for i in range(0, 100):
        yield i


print(sum(gen()))
```

* [Generator Tricks](http://www.dabeaz.com/generators/index.html)
* [A Curious Course on Coroutines and Concurrency](http://dabeaz.com/coroutines/)

## Itertools and more itertools

* [itertools](https://docs.python.org/3.5/library/itertools.html)
* [more-itertools](https://pypi.python.org/pypi/more-itertools)

## Context managers

```python
with open(__file__, 'r') as f:
    for l in f:
        print(l)
```

```python
import contextlib


@contextlib.contextmanager
def greet(name):
    print('Hello %s' % name)
    yield
    print('Goodbye %s' % name)


with greet('world'):
    print(42)
```

```python
with foo() as f_in, \
      bar() as f_out:
    ...
```

## Serialization

* JuJ: Just Use Json
* Pickle and YAML are both security risks!

## Static analyzers, coverage

```python
import random


def randomPlusOne():
    return random.randint(0, 1000000) + 1
```

```python
import unittest
from unittest import mock

import src


class TestTest(unittest.TestCase):
    @mock.patch('src.random')
    def testRandomPlusOne(self, random_mock):
        random_mock.randint.return_value = 1
        self.assertEqual(2, src.randomPlusOne())
```

```bash
pip install flake8
pip install pylint
flake8 src.py
pylint src.py
```

```bash
coverage run --branch --module unittest test
coverage report
```

## Debugging

* pdb / [pudb](https://pypi.python.org/pypi/pudb/)
* set_trace()
* no cross-thread BPs
* `python -m p[u]db`

## Logging

```python
import logging

logging.error('Huston...')

try:
    raise ValueError()
except ValueError:
    logging.exception('Error!')
```

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

* `getattr` / `hasattr` / `setattr`
* `min` / `max`
* `sort` / `sorted` / `reverse`
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
