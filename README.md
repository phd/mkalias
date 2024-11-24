mkalias
=======

Automatic lazy Bash completion for aliases.

Lazy assignment of completion functions to aliases in `.bashrc` prevents Bash from loading completion functions for all
referenced commands at startup and taking up to several seconds to become interactive.

Importing
---------

Import `mkalias.sh` in `.bashrc` or your interactive shell:

``` bash
source /absolute/or/./relative/path/to/mkalias.sh
```

Usage
-----

```
mkalias NAME [SYNTAX [COMMAND]]
mkalias [-p [NAME]]
mkalias (--help|-h)

    NAME       The Name of the alias, required.
    SYNTAX     New syntax for alias, optional.
               If given, mkalias creates a new alias NAME for that syntax.
               If not given, it gets the current syntax from the existing alias
               or returns an error.
    COMMAND    Command to complete alias like, optional.
               If given, mkalias notifies Bash completion to complete the alias
               like it was this command.
               If not given, mkalias deduces the command to act as from the
               first word of the alias' syntax.
    -p [NAME]  Print the alias, its syntax and associated completion command.
               With no arguments print all completion-enabled aliases.

    Calling mkalias on an existing alias again will simply redefine it and/or
    overwrite its completion settings.
```

Examples
--------

Create a *new* alias `g` for `git` and register it for completion like the *deduced* command `git`:

``` bash
$ mkalias g git
```

Create a *new* alias `g` for `clear && git` and register it for completion like the *explicit* command `git`:

``` bash
$ mkalias g 'clear && git' git
```

Create a standard alias `g` for `git`.
Then register the *existing* alias `g` for completion like the *deduced* command `git`:

``` bash
$ alias g='git'
$ mkalias g
```

Create a standard alias `g` for `clear && git`.
Then register the *existing* alias `g` for completion like the *explicit* command `git`:

``` bash
$ alias g='clear && git'
$ mkalias g '' git
```

Testing
-------

You can test Bash completion for your newly created `git` alias `g` by typing:

``` bash
$ g stat[TAB]
```

which after pressing the `[TAB]` key will be completed to:

``` bash
$ g status
```
