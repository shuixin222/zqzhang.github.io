---
layout: post
type: post
title: Parse Arguments in Python
---

This is first time to use Python in seriously. Just start from code snippets
used in my projects. Good or bad, it is just a start.

## First code snippet

Let's see the first code snippet. Sounds like it is trying to parse arguments
passed into the script.

```python
import sys
from base_utils import get_args

##### initialization #####
globals().update(vars(get_args(sys.argv)))
args = {}
if script_args:
    for entry in script_args:
        key, val = entry.split("=")
        args[key] = val

globals().update(args)
```

## Annotating the code snippet

### `import`

First thing first, the `import` key word, per the Python tutorial
[modules](https://docs.python.org/2/tutorial/modules.html), imports a standard
module *sys* and a function *get_args* from a package (module). There are
2 recommended ways for importing:

* Import a module via `import item` or `import item.subitem.subsubitem`, where
  each item except for the last must be a package; the last item can be a module
  or a package but cannot be a class or function or variable defined in the
  previous item.
* Import a module, function, class or variable via `from package import item`,
  where the `import` statement first tests whether the item is defined in the
  package; if not, it assumes it is a module and attempts to load it. If it
  fails to find it, an ImportError exception is raised.

### `sys.argv`

The
[`sys.argv`](https://docs.python.org/2/library/sys.html?highlight=sys.argv#sys.argv)
variable returns a list of command line arguments passed to a Python script.

`argv[0]` is the script name (it is operating system dependent whether this is
a full pathname or not). If the command was executed using the `-c `command line
option to the interpreter, `argv[0]` is set to the string `'-c'`. If no script
name was passed to the Python interpreter, `argv[0]` is the empty string.

### `get_args()`

This is an utility function for parsing arguments. It is defined in the
`base_utils` module.

```python
import argparse
import sys

def get_args(args):
    '''
    Helper function for parsing arguments
    Usage:
        args = get_args(sys.argv)
    '''
    old_argv = sys.argv
    sys.argv = args

    parser = argparse.ArgumentParser(
                description = 'Process arguments for each script/runner')
    # connection arguments
    # serial
    parser.add_argument('-s', '--serial', dest = 'serial',
                        help = 'Device serial')
    # ADB server port
    parser.add_argument('--adb-server-port', dest = 'adb_server_port',
                        help = 'Port for ADB server')
    # ADB local port for uiautomator
    parser.add_argument('--adb-local-port', dest = 'adb_local_port',
                        help = 'ADB local port for uiautomator')

    # script args
    parser.add_argument('--script-args', dest = 'script_args',
                        help = 'Script arguments', nargs = '+')


    args = parser.parse_args()

    sys.argv = old_argv
    globals().update(vars(args))
    return args
```

This function uses standard library
[argparse](https://docs.python.org/2/library/argparse.html)
to add (`parser.add_argument()`) and parse (`parser.parse_args()`) arguments.

### `vars()`

[`vars()`](https://docs.python.org/2/library/functions.html?highlight=vars#vars)
is a built-in function. It returns the `__dict__` attribute for a module, class,
instance, or any other object with a `__dict__` attribute.

Where,
[`object.__dict__`](https://docs.python.org/2/library/stdtypes.html#object.__dict__)
is a dictionary or other mapping object used to store an object’s (writable)
attributes.

### `globals().update()`

[`globals()`](https://docs.python.org/2/library/functions.html?highlight=globals#globals)
is a built-in function. It returns a dictionary representing the current global
symbol table. This is always the dictionary of the current module (inside a
function or method, this is the module where it is defined, not the module
from which it is called).

[`dict.update([other])`](https://docs.python.org/2/library/stdtypes.html?highlight=update#dict.update)
updates the dictionary with the key/value pairs from other, overwriting existing
keys. It returns `None`.

`update()` accepts either another dictionary object or an iterable of key/value
pairs (as tuples or other iterables of length two). If keyword arguments are
specified, the dictionary is then updated with those key/value pairs:
`d.update(red=1, blue=2)`.

## Trying the code snippet

Copy the code snippet into a file, say `parse_arguments.py`, and put it in the
same sub-directory as `base_utils.py`. Then we can try it.

```bat
.\parse_arguments.py --help
usage: parse_arguments.py [-h] [-s SERIAL] [--adb-server-port ADB_SERVER_PORT]
                          [--adb-local-port ADB_LOCAL_PORT]
                          [--script-args SCRIPT_ARGS [SCRIPT_ARGS ...]]

Process arguments for each script/runner

optional arguments:
  -h, --help            show this help message and exit
  -s SERIAL, --serial SERIAL
                        Device serial
  --adb-server-port ADB_SERVER_PORT
                        Port for ADB server
  --adb-local-port ADB_LOCAL_PORT
                        ADB local port for uiautomator
  --script-args SCRIPT_ARGS [SCRIPT_ARGS ...]
                        Script arguments
```

See the online demo at
[here](https://github.com/zqzhang/demo/tree/gh-pages/python).
