# NuPIC Developer Tools

There are two tools here. If you want them add the `bin` folder to your `PATH`:

- [NuPIC startup scripts](#startup-scripts)
- [release script](#release-script)

# NuPIC startup scripts

These scripts are used to build NuPIC and NuPIC Core from source code cloned into local repositories. Once added to your `PATH`, they may be executed from anywhere in your filesystem. 

> **NOTE**: The help strings below denote paths that will be different on each system, depending on the checkout locations of `NUPIC` and `NUPIC_CORE`. 

## Requirements

- `export NUPIC=<nupic-repo>`
- `export NUPIC_CORE=<nupic-core-repo>`

## Usage

### Installing NuPIC Core

`> install_nupic_core -h`

```
Installs nupic.core from /Users/mtaylor/nta/nupic.core directory. By default, this
installs into /Users/mtaylor/nta/nupic.core/build/release, but can be overridden with the
-r or -s options (see below).

Usage:
> install_nupic_core [options]

Options:
 -c Clean build, removes old build artifacts.
 -v Verbose console output.
 -s build into system location (if specified, -r is ignored)
 -r <release-dir> outputs release to specified directory instead of
    /Users/mtaylor/nta/nupic.core/build/release (default)

Examples:
An installation to default location at /Users/mtaylor/nta/nupic.core/build/release:
    > install_nupic_core
A clean verbose installation to system location:
    > install_nupic_core -cvs
A clean installation to specified location (/tmp):
    > install_nupic_core -c -r /tmp
```

### Installing NuPIC

`> install_nupic -h`

```
Installs NuPIC from /Users/mtaylor/nta/nupic directory. If nupic.core release directory
is not specified with -u or -r options (see below), the nupic.core
binary package is downloaded.

Usage:
> install_nupic [options]

Options:
 -c Clean build, removes old build artifacts.
 -v Verbose console output.
 -u Builds using nupic.core release at /Users/mtaylor/nta/nupic.core/build/release
 -r <release-dir> Builds using nupic.core release at specified
    directory instead of /Users/mtaylor/nta/nupic.core/build/release.

Examples:
An installation using downloaded nupic.core binary release:
    > install_nupic
A clean verbose installation using nupic.core at
/Users/mtaylor/nta/nupic.core/build/release:
    > install_nupic -cvu
A clean installation using nupic.core at specified location (/tmp):
    > install_nupic -cv -r /tmp
```

### Install All

`> install_nupic_all` 

Calls the previous two scripts with the `-c` options and ensures the `nupic.core` release binaries are used for the `nupic` build. 


# Release script

> **WARNING**: This script is still a work in progress!

Pushes a new git release using git tags and the GitHub API. Users must have push access to the target repository and a GitHub access token.

## Requirements:
- git
- [GitHub access token](https://github.com/blog/1509-personal-api-tokens)
  - `export GH_ACCESS_TOKEN=<token>`
- Push access to target git repository
- `pip install libsaas`

## Usage

> ./bugfix-release <path-to-repo> [options]

The `path-to-repo` may be a relative or absolute path to the repository being released. If the path is omitted, it's assumed you're releasing NuPIC, so the value of the `NUPIC` environment variable will be used for the repository location. 


## Options
```
  -h, --help            show this help message and exit
  -v, --verbose         Print debugging statements.
  -d, --dry_run         Prevents pushing to remote master branch.
  -r REMOTE, --remote=REMOTE
                        Which remote location to push to (default 'upstream').
```