Simple python 3.9+ script to reapply annotations from stub files to existing code. Doesn't preserve comments now, so is not read for production use.

## Installation
This project is not available yet on PyPi. 

Installing directly from git:

1. Clone repo
    $ git clone https://github.com/sterliakov/stubmerge
    $ cd stubmerge
1. Create virtual environment of your choice, install requirements:
    $ python -m virtualenv pyenv
    $ . pyenv/bin/activate
    $ pip install -r requirements.txt
1. Enjoy!

## Usage:

```
usage: retypeme.py [-h] [--ignore-decorators IGNORE_DECORATORS [IGNORE_DECORATORS ...]]
                   [--ignore-errors {method,missing_class,bases,assignment,wrong_kind,decorators,signature,multi_assignment,error,missing_source} [{method,missing_class,bases,assignment,wrong_kind,decorators,signature,multi_assignment,error,missing_source} ...]]
                   [--no-color] [--no-isort] [--black] [--django]
                   source stub target

Apply annotations from stub files to source

positional arguments:
  source                Source files directory
  stub                  Stub files directory
  target                Output files directory (will be overwritten)

options:
  -h, --help            show this help message and exit
  --ignore-decorators IGNORE_DECORATORS [IGNORE_DECORATORS ...]
                        Decorators to exclude from checks (only function name, like `lru_cache`)
  --ignore-errors {method,missing_class,bases,assignment,wrong_kind,decorators,signature,multi_assignment,error,missing_source} [{method,missing_class,bases,assignment,wrong_kind,decorators,signature,multi_assignment,error,missing_source} ...]
                        Error types to ignore
  --no-color            Disable output coloring
  --no-isort            Disable isort
  --black               Format output with black
  --django              Perform django-specific tasks
```

Pass `--django` flag to replace `@cached_property` with `@property` and `@classonlymethod` with `@classmethod` to make mypy a little happier.

## Features:

* Detect incompatible stubs and source base classes, missing/extra methods and variables, decorators etc.
* Does not die on errors (except for syntax errors which are intentionally propagated)
* Work fast ([`django-stubs`](https://pypi.org/project/django-stubs/) are reapplied to Django in 15 s. and in 1 minute with black)

