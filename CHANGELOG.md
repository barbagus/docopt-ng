# CHANGELOG

## UNRELEASED

### Changed
- Tweak a few things to restore compatibility with docopt (the original repo) 0.6.2
  See PR https://github.com/jazzband/docopt-ng/pull/36 for more info
  
    1. BREAKING: Restore what constitutes an "option":
       Now the important rule to follow is
       `any line starting with - or -- is treated as an option`.
       This means that some things that did NOT used to be treated
       as options, now ARE treated as options:
           
           1. lines before `usage:`
           2. non-indented --options
           3. lines not inside the options: section
       
       However, we also keep one part of the old behavior of this fork where in the line
       `header that ends with the keyword options: --foo`, --foo is still treated as
       an option because the start of a line up to `options:` is ignored.
    
    2. BREAKING: Error messages are tweaked a little bit. Unlikely that you relied
       on them, but just in case.
    
    3. NONBREAKING: Now allow for blank lines between options.
       As described in https://github.com/jazzband/docopt-ng/issues/33

    4. NONBREAKING: Fix an unlikely edge case of how options are parsed:
       Here, --foo was interpreted to take "Enable" as an argument
       ```
       options:
          --foo
        Enable the foo behaviour. (One space before "Enable")
       ```
       Whereas here, Enable was interpreted as part of the description.
       ```
       options:
          --foo
         Enable the foo behaviour. (2 space before "Enable".)
       ```
       Now, both of these examples are treated more intuitively, where Enable
       is treated as the description

## Version 0.8.1:

- Fixup of auto release in Github Actions

## Version 0.8.0:

- Expose `DocoptExit` in `__all__`, let users to raise DocoptExit from their code
  https://github.com/jazzband/docopt-ng/pull/8
- Fix magic with arguments that have a dash https://github.com/jazzband/docopt-ng/pull/6
- Add `py.typed` so now users can actuall use mypy with us!
  https://github.com/jazzband/docopt-ng/commit/de7c861dafb86418da423d4829f389a62c82151a
- Migrate to being maintained by Jazzband!
- Migrate to GitHub actions from TravisCI
- Update and tweak many little things in build, testing, and docs

## Version 0.7.2:

-   Complete MyPy typehints - ZERO errors.
    Required refactoring class implementations, adding typing stubs, but not changing tests. :)
-   100% code coverage. Required the addition of a few tests.
    Removed unused codepaths. Tagged typing stubs `pragma: no cover` as they are definitionally exercised.

## Version 0.7.1:

-   Add `magic()` and `magic_docopt()` aliases for `docopt()` allowing easier use of new features.

## Version 0.7.0:

-   "MORE MAGIC"
-   First argument is now optional - `docopt()` will look for `__doc__` defined in parent scopes.
-   Dot access is supported on resulting `arguments` object,
    ignoring angle brackets and leading dashes.
-   `more_magic` parameter added to `docopt()` defaults False.
-   If `more_magic` enabled, `arguments` variable created and populated
    in calling scope with results.
-   If `more_magic` enabled, fuzzy (levenshtein) autocorrect enabled for long-args.
-   Lots of typehints.
-   README moved to Markdown.

## Version 0.6.3:

-   Catch up on \~two years of pull requests.
-   Fork [docopt](https://github.com/docopt/docopt) to
    [docopt-ng](https://github.com/bazaar-projects/docopt-ng).
-   Add levenshtein based autocorrect from
    [string-dist](https://github.com/obulkin/string-dist).
-   Add better debug / error messages.
-   Linting (via [black](https://github.com/ambv/black) and
    [flake8](https://gitlab.com/pycqa/flake8)).

## Version 0.6.2:

-   Bugfixes

## Version 0.6.1:

-   Fix issue [\#85](https://github.com/docopt/docopt/issues/85) which
    caused improper handling of `[options]` shortcut if it was present
    several times.

## Version 0.6.0:

-   New argument `options_first`, disallows interspersing options and
    arguments. If you supply `options_first=True` to `docopt`, it will
    interpret all arguments as positional arguments after first
    positional argument.
-   If option with argument could be repeated, its default value will
    be interpreted as space-separated list. E.g. with
    `[default: ./here ./there]` will be interpreted as
    `['./here', './there']`.
