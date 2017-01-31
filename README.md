# Python Quickstart

Premise: you know programming but know no (or only a little of) Python.

**Note**: This is for Python 3, *NOT* legacy Python (2.7)

## Introduction

- Python: a slow, statically typed (but checked at runtime) scripting language.
- Sorry for choosing it, here are some steps to make it less painful

## Virtual environments, packages

```bash
mkdir python-quickstart
cd python-quickstart
pyvenv env
source env/bin/activate
```

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
# command line:
pip install -r requirements_dev.txt
```

```
pip freeze > requirements_frozen.txt
pip list --outdated --format=columns
```

## Numbers, strings, lists, tuples, dicts, sets

## Ordered dicts, frozensets, named touple, counter

## Testing, TDD, mocking

## Function, decorators

* Closures

## Exceptions

## Classes

* Inheritance
* Magic methods

## List/Dict/Set comprehensions

## Generators

## Itertools and more itertools

## Context managers

## Serialization

* JuJ: Just Use Json
* Pickle and YAML are both security risks!

## Static analyzers, coverage

## Debugging

## Logging

## WSGI, Flask

## Podcasts

* [Talk Python to Me](https://talkpython.fm/)
* [Podcast.\_\_init\_\_](https://pythonpodcast.com/)
* [Python Bytes](https://pythonbytes.fm/)
