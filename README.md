# Scripts To Rule Them All

[![CI](https://github.com/peteoshea/scripts-to-rule-them-all/workflows/CI/badge.svg)](https://github.com/peteoshea/scripts-to-rule-them-all/actions)
[![Build Status](https://travis-ci.org/peteoshea/scripts-to-rule-them-all.svg?branch=master)](https://travis-ci.org/peteoshea/scripts-to-rule-them-all)

This is a set of boilerplate bash scripts based on GitHub's [scripts-to-rule-them-all](https://github.com/github/scripts-to-rule-them-all).

I did not have a reason to call the [bootstrap][bootstrap] script directly so I have moved it into a `bin` subfolder to allow reuse without cluttering up the main `script` folder.

The `cibuild` script didn't really make sense to me as different CI systems have different requirements so I have removed it.
As an example the [test][test] script is called directly from the [ci.yml][ci.yml] GitHub action.

As for the `server` and `console` scripts then I haven't had a need for them yet so I've just removed them for now.
I will recreate them as bash scripts if and when I have a need for them.

I have also created a set of [PowerShell Scripts To Rule Them All](https://github.com/peteoshea/powershell-scripts-to-rule-them-all) for developing also happens on Windows machines.

## The Scripts

The following is a list of scripts and their primary responsibilities.

### [script/setup][setup]

Used to set up a project in an initial state.
This is typically run after an initial clone, or, to reset the project back to its initial state.

### [script/update][update]

Used to update the project after a fresh pull.
This should include any database migrations or any other things required to get the state of the app into shape for the current version that is checked out.

### [script/test][test]

Used to run the test suite of the project.
To allow this script to be run from CI setup should be done outside of this script.
A manual call to [update][update] before running the tests is usually a good idea.

A good pattern to support is having optional arguments that allow you to run specific tests.

Linting is also be considered a form of testing.
These tend to run faster than tests, so put them towards the beginning so it fails faster if there's a linting problem.

## Installing Dependencies

The [bootstrap][bootstrap] script, called from both [setup][setup] and [update][update] scripts, is used solely for fulfilling dependencies of the project.
This can mean installing packages, updating git submodules, etc.
The goal is to make sure all required dependencies are installed.

This script currently allows for following package managers:

### [APT](https://en.wikipedia.org/wiki/APT_(software))

If you are on a Debian based Linux system, like Ubuntu, then you can create an `apt-pkgs` file with a list of the required packages.
You must ensure that this file has Linux line-endings (LF) otherwise it may not work as expected.

### [yum](https://en.wikipedia.org/wiki/Yum_(software))

If you are on a RedHat based Linux system, like CentOS or Fedora, then you can create an `yum-pkgs` file with a list of the required packages.
You must ensure that this file has Linux line-endings (LF) otherwise it may not work as expected.

### [Homebrew](https://brew.sh/)

You can use [Homebrew](https://brew.sh/) by creating a `Brewfile` at the top level of the project with a list of the packages to be installed.
Simply having the `Brewfile` means Homebrew will be installed and updated.

[bootstrap]: script/bin/bootstrap
[ci.yml]: .github/wokflows/ci.yml
[setup]: script/setup
[test]: script/test
[update]: script/update
