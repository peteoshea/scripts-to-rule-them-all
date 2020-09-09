# Scripts To Rule Them All

[![Build Status](https://travis-ci.org/github/peteoshea/scripts-to-rule-them-all.svg?branch=master)](https://travis-ci.org/github/peteoshea/scripts-to-rule-them-all)

This is a set of boilerplate scripts based on GitHub's
[scripts-to-rule-them-all](https://github.com/github/scripts-to-rule-them-all).

I don't feel that all of these scripts need to be called directly so I am moving some of them into a
`bin` subfolder to allow reuse without cluttering up the main `script` folder.

## The Scripts

The following is a list of scripts and their primary responsibilities.

### [script/setup][setup]

Used to set up a project in an initial state.
This is typically run after an initial clone, or, to reset the project back to its initial state.

### [script/update][update]

Used to update the project after a fresh pull.
This should include any database migrations or any other things required to get the state of the
app into shape for the current version that is checked out.

### [script/test][test]

Used to run the test suite of the project.
As this script will likely be called from [cibuild][cibuild] it should handle setting things up.
This will usually be done by a call to [update][update].

A good pattern to support is having optional arguments that allow you to run specific tests.

Linting is also be considered a form of testing.
These tend to run faster than tests, so put them towards the beginning so it fails faster if
there's a linting problem.

### [script/cibuild][cibuild]

*TODO - Needs converting to bash when actually required.*

[`script/cibuild`][cibuild] is used for your continuous integration server.
This script is typically only called from your CI server.

You should set up any specific things for your environment here before your tests
are run. Your test are run simply by calling [`script/test`][test].

### script/server

*TODO - Needs converting to bash when actually required.*

[`script/server`][server] is used to start the application.

For a web application, this might start up any extra processes that the
application requires to run in addition to itself.

[`script/update`][update] should be called ahead of any application booting to ensure that
the application is up to date and can run appropriately.

### script/console

*TODO - Needs converting to bash when actually required.*

[`script/console`][console] is used to open a console for your application.

A good pattern to support is having an optional argument that is an environment
name, so you can connect to that environment's console.

You should configure and run anything that needs to happen to open a console for
the requested environment.

## Installing Dependencies

The [bootstrap][bootstrap] script, called from both [setup][setup] and [update][update] scripts,
is used solely for fulfilling dependencies of the project.
This can mean installing packages, updating git submodules, etc.
The goal is to make sure all required dependencies are installed.

This script currently allows for following package managers:

### [APT](https://en.wikipedia.org/wiki/APT_(software))

If you are on a Debian based Linux system, like Ubuntu, then you can create an `apt-pkgs` file with
a list of the required packages.
You must ensure that this file has Linux line-endings (LF) otherwise it may not work as expected.

### [yum](https://en.wikipedia.org/wiki/Yum_(software))

If you are on a RedHat based Linux system, like CentOS or Fedora, then you can create an `yum-pkgs`
file with a list of the required packages.
You must ensure that this file has Linux line-endings (LF) otherwise it may not work as expected.

### [Homebrew](https://brew.sh/)

You can use [Homebrew](https://brew.sh/) by creating a `Brewfile` at the top level of the project
with a list of the packages to be installed.
Simply having the `Brewfile` means Homebrew will be installed and updated.

[bootstrap]: script/bin/bootstrap
[cibuild]: script/cibuild
[console]: script/console
[server]: script/server
[setup]: script/setup
[test]: script/test
[update]: script/update
