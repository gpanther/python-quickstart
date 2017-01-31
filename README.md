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

## Numbers, strings, lists, tuples, dicts, sets

## Comments

## Ordered dicts, frozensets, named touple, counter

## Testing, TDD

## Function, decorators

* Named parameters
* "varargs"
* Closures
* Lambdas / anonymous functions

## Mocking

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

- WSGI: web standard gateway interface
- "WSGI servers": uWSGI, mod_wsgi, etc
- [Flask](http://flask.pocoo.org/): very basic web framework.
- Uses thread-local variables like `flask.request`
- Has an integrated debugger
- Watch out for security! Doesn't even provide CSRF protection by default: http://flask.pocoo.org/snippets/3/
- Probably should be checked for https://www.owasp.org/index.php/Top_10_2013-Top_10

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

* Python 3.5 type hints
* Good editors: PyCharm, PyDev
* [/r/Python](https://www.reddit.com/r/Python/) and [/r/PythonTips](https://www.reddit.com/r/pythontips/)
* Code formatting guidelines (style guides):
  * PEP8: https://www.python.org/dev/peps/pep-0008/
  * Google Style Guide: https://google.github.io/styleguide/pyguide.html
* `from __future__ import ...` - see the [\__future\__ module](https://docs.python.org/3.6/library/__future__.html)
* `# -*- coding: <encoding-name> -*-`

# Good luck!
