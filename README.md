[![npm version](https://badge.fury.io/js/ttab.svg)](http://badge.fury.io/js/ttab)

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

**Contents**

- [ttab &mdash; Introduction](#ttab-&mdash-introduction)
- [Installation](#installation)
  - [From the npm registry](#from-the-npm-registry)
  - [Manual installation](#manual-installation)
- [Examples](#examples)
- [Usage](#usage)
- [License](#license)
  - [Acknowledgements](#acknowledgements)
  - [npm dependencies](#npm-dependencies)
- [Changelog](#changelog)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


# ttab &mdash; Introduction

An [OS X](https://www.apple.com/osx/) CLI for programmatically opening a new terminal tab/window in the standard terminal application, `Terminal.app`, optionally with a command to execute and/or a specific title and specific display settings.

# Installation

**Important**: Irrespective of installation method, `ttab` needs to be granted _access for assistive devices_ in order to operate, which is a _one-time operation that requires administrative privileges_.  
If you're not prompted on first run and get an error message instead, go to `System Preferences > Security & Privacy`, tab `Privacy`, select `Accessibility`, unlock, and make sure `Terminal.app` is in the list on the right and has a checkmark.  
For more information, see [Apple's support article on the subject](https://support.apple.com/en-us/HT202802)

## From the npm registry

With [Node.js](http://nodejs.org/) or [io.js](https://iojs.org/) installed, install from the [npm registry](https://www.npmjs.com/package/ttab):

    [sudo] npm install ttab -g

**Note**:

* Whether you need `sudo` depends on how you installed Node.js / io.js and whether you've [changed permissions later](https://docs.npmjs.com/getting-started/fixing-npm-permissions); if you get an `EACCES` error, try again with `sudo`.
* The `-g` ensures [_global_ installation](https://docs.npmjs.com/getting-started/installing-npm-packages-globally) and is needed to put `ttab` in your system's `$PATH`.

## Manual installation

* Download [this `bash` script](https://raw.githubusercontent.com/mklement0/ttab/stable/bin/ttab) as `ttab`.
* Make it executable with `chmod +x ttab`.
* Move it to a folder in your `$PATH`, such as `/usr/local/bin`

# Examples

```shell
# Open a new tab in the current terminal window.
ttab

# Open a new tab in a new terminal window.
ttab -n 

# Open a new tab and execute the specified command.
ttab ls -l "$HOME/Library/Application Support"

# Open a new tab, switch to the specified dir., then execute the specified command.
ttab -d ~/Library/Application\ Support ls -1 

# Open a new tab with title 'How Green Was My Valley' and settings 'Grass'
ttab -t 'How Green Was My Valley' -s Grass

# Open a new tab and execute the specified script.
ttab /path/to/someScript 

# Open a new tab, execute the specified script, then close the tab on termination.
ttab exec /path/to/someScript

# Open a new tab, execute a command, wait for a keypress, then close the tab.
ttab eval "ls \$HOME/Library/Application\ Support; echo Press a key to exit.; read -s -n 1; exit"
```

# Usage

<!-- DO NOT EDIT THE FENCED CODE BLOCK and RETAIN THIS COMMENT: The fenced code block below is updated by `make update-readme/release` with CLI usage information. -->

```
$ ttab --help


SYNOPSIS:
  ttab [-w] [-s settings] [-t title] [-g|-G] [-d dir] [command [param1 ...]]

DESCRIPTION:
  Opens a new Terminal.app tab and optionally executes a
  command and assigns settings,     among other options.

  IMPORTANT: *Terminal.app must be allowed assistive access* in order for this
  utility to work, which requires one-time authorization with administrative
  privileges. If you get error messages instead of being prompted, authorize
  Terminal.app via System Preferences > Security & Privacy > Privacy >
  Accessibility.

  The new tab will run a login shell (i.e., load the user's shell profile)
  and by default inherit the working directory from the parent shell.

  -w
    creates the new tab in a new window rather than in Terminal's front
    window.
  -s
    specifies the settings (profiles) to apply to the new tab, as
    defined in Terminal.app's Preferences > Profiles, such as 'Grass';
    settings determine the appearance and behavior of the new tab; name
    matching is case-insensitive.
  -t 
    specifies a custom title to assign to the new tab; otherwise, if a 
    command is specified, its first token will become the new tab's title.
  -d
    explicitly specifies a working directory for the new tab; by default, the
    invoking shell's working directory is inherited (even if -w is also
    specified).
  -g
    (back*g*round) causes Terminal not to activate, if it isn't the frontmost
    application); within Terminal, however, the new tab will become active
    active tab; useful in scripts that launch other applications and
    don't want Terminal to steal focus later.
  -G
    causes Terminal not to activate *and* the active element within Terminal
    not to change; i.e., the active window and tab stay the same. If Terminal
    happens to be fronmost, the new tab will effectively open in the
    background.

  NOTE: With -g or -G specified, for technical reasons, Terminal / the new
        tab will still activate *briefly, temporarily* in most scenarios.

  Quoted parameters are handled properly and there's no need to quote the
  command as a whole, provided it is a *single* command.
  Prefix such a single command with 'exec' to automatically close the tab
  when the command terminates, assuming the tab's settings are configured to
  close the tab on termination of the shell.

  To specify *multiple* commands, use 'eval' followed by a single,
  *double*-quoted string in which the commands are separated by ';' Do NOT
  use backslash-escaped double quotes *inside this string*; rather, use
  *single-character backslash-escaping* as needed. Use 'exit' as the last
  command to automatically close the tab when the command terminates,
  assuming the tab's settings are configured to close the tab on termination
  of the shell.
  Precede 'exit' with 'read -s -n 1' to wait for a keystroke first.

EXAMPLES:
  # Create new tab with title 'Green' using settings 'Grass'
  ttab -t Green -s Grass  
  ttab ls -l "$HOME/Library/Application Support"
  ttab -d "$HOME/Library/Application Support" ls -1
  ttab /path/to/someScript arg1 arg2
  # Execute a script and close the tab on termination (settings permitting).
  ttab exec /path/to/someScript arg1 arg2
  # Pass a multi-command string via 'eval', wait for keystroke, then exit.
  ttab eval "ls \$HOME/Library/Application\ Support; 
                    echo Press a key to exit.; read -s -n 1; exit"
```

<!-- DO NOT EDIT THE NEXT CHAPTER and RETAIN THIS COMMENT: The next chapter is updated by `make update-readme/release` with the contents of 'LICENSE.md'. ALSO, LEAVE AT LEAST 1 BLANK LINE AFTER THIS COMMENT. -->

# License

Copyright (c) 2015 Michael Klement <mklement0@gmail.com> (http://same2u.net), released under the [MIT license](https://spdx.org/licenses/MIT#licenseText).

## Acknowledgements

This project gratefully depends on the following open-source components, according to the terms of their respective licenses.

[npm](https://www.npmjs.com/) dependencies below have optional suffixes denoting the type of dependency; the *absence* of a suffix denotes a required *run-time* dependency: `(D)` denotes a *development-time-only* dependency, `(O)` an *optional* dependency, and `(P)` a *peer* dependency.

<!-- DO NOT EDIT THE NEXT CHAPTER and RETAIN THIS COMMENT: The next chapter is updated by `make update-readme/release` with the dependencies from 'package.json'. ALSO, LEAVE AT LEAST 1 BLANK LINE AFTER THIS COMMENT. -->

## npm dependencies

* [doctoc (D)](https://github.com/thlorenz/doctoc)
* [json (D)](https://github.com/trentm/json)
* [replace (D)](https://github.com/harthur/replace)
* [semver (D)](https://github.com/npm/node-semver#readme)
* [tap (D)](https://github.com/isaacs/node-tap)
* [urchin (D)](https://github.com/tlevine/urchin)

<!-- DO NOT EDIT THE NEXT CHAPTER and RETAIN THIS COMMENT: The next chapter is updated by `make update-readme/release` with the contents of 'CHANGELOG.md'. ALSO, LEAVE AT LEAST 1 BLANK LINE AFTER THIS COMMENT. -->

# Changelog

Versioning complies with [semantic versioning (semver)](http://semver.org/).

<!-- NOTE: An entry template for a new version is automatically added each time `make version` is called. Fill in changes afterwards. -->

* **v0.1.6** (2015-06-01):
  * [doc] Read-me improvements; typo in CLI usage help fixed.

* **v0.1.5** (2015-06-01):
  * [doc] Improved CLI usage help.

* **v0.1.4** (2015-06-01):
  * [doc] Improved CLI usage help; keywords added to `package.json`.
  * [dev] `make browse` now opens the GitHub repo in the default browser.

* **v0.1.3** (2015-06-01):
  * [fix] The -g and -G options again correctly do not activate Terminal.app when creating the desired tab.
  * [enhancement] Option parsing now accepts option-arguments directly attached to the option.
  * [dev] Tests added.

* **v0.1.2** (2015-06-01):
  * [doc] Manual-installation link and instructions fixed; examples fixed.

* **v0.1.1** (2015-06-01):
  * [doc] README.md improved with respect to manual installation instructions.

* **v0.1.0** (2015-06-01):
  * Initial release.
