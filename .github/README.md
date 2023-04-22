# ans_role_config_shell

Set shell-agnostic environment variables, login actions, and logout actions.

[![Release](https://img.shields.io/github/release/digimokan/ans_role_config_shell.svg?label=release)](https://github.com/digimokan/ans_role_config_shell/releases/latest "Latest Release Notes")
[![License](https://img.shields.io/badge/license-MIT-blue.svg?label=license)](LICENSE.md "Project License")

## Table Of Contents

* [Purpose](#purpose)
* [Supported Operating Systems](#supported-operating-systems)
* [Quick Start](#quick-start)
    * [Use From Playbook](#use-from-playbook)
    * [Use From Parent Role As Dependency](#use-from-parent-role-as-dependency)
* [Role Options](#role-options)
* [Contributing](#contributing)

## Purpose

* Specify environment variables that will be set by a user's login shell.
* Define optional commands to be run by the user's login shell.
* Define optional commands to be run on exit of the user's login shell.
* Support _bash_, _bourne_, _ksh_, _csh_, _tcsh_, and _zsh_ user login-shells.

## Supported Operating Systems

* Ubuntu.
* Arch Linux.
* FreeBSD.

## Quick Start

### Use From Playbook

1. Create `requirements.yml` in ansible project root, and add this content:

   ```yaml
   # requirements.yml
   - src: https://github.com/digimokan/ans_role_config_shell
   ```

2. From the project root directory, install/download the role:

   ```shell
   $ ansible-galaxy install --role-file requirements.yml --roles-path ./roles --force-with-deps
   ```

   * _NOTE:_ `--force-with-deps` _ensures subsequent calls download updates_

3. Include the main role, to set up the shell config files:

   ```yaml
   - name: "Set up commonly-sourced config files for all shells"
     ansible.builtin.include_role:
       name: ans_role_config_shell
     vars:
       user_name: "admin"
   ```

## Role Options

See the role `defaults` files for main role vars listings:

  * [defaults](../defaults/main/)

Define these _required_ vars for the role:

  * `user_name`: user to set up the shell config files for

## Contributing

* Feel free to report a bug or propose a feature by opening a new
  [Issue](https://github.com/digimokan/ans_role_config_shell/issues).
* Follow the project's [Contributing](CONTRIBUTING.md) guidelines.
* Respect the project's [Code Of Conduct](CODE_OF_CONDUCT.md).

