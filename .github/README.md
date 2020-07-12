# ans-role-shell-common

Configure a core set of files sourced for _bash_, _zsh_, and _sh_.

[![Release](https://img.shields.io/github/release/digimokan/ans-role-shell-common.svg?label=release)](https://github.com/digimokan/ans-role-shell-common/releases/latest "Latest Release Notes")
[![License](https://img.shields.io/badge/license-MIT-blue.svg?label=license)](LICENSE.md "Project License")

## Table Of Contents

* [Purpose](#purpose)
* [Supported Operating Systems](#supported-operating-systems)
* [Quick Start](#quick-start)
    * [Load Role Via `ansible-galaxy` Command](#load-role-via-ansible-galaxy-command)
* [Role Options](#role-options)
* [Contributing](#contributing)

## Purpose

* Put all _bash_, _zsh_, _sh_ __common__ environment variables into
  `common/en_vars` file.
* Put all _bash_, _zsh_, _sh_ __common__ interactive functions/aliases into
  `common/aliases` file.
* Put all _bash_, _zsh_, _sh_ __common__ logout actions into
  `common/logout_actions` file.
* Put all __non-common__ configuration into `bash/en_vars`, `zsh/en_vars`, etc
  files.
* Make the __non-common__ files source the __common__ files.
* Make the shell-specific files (`.bashrc`, `.bash_profile`, `.zshrc`, etc)
  source the __non-common__ files.
* Configure correct behavior for all combinations of login, non-login,
  interactive, and non-interactive shell invocations.

## Supported Operating Systems

* Arch Linux.

## Quick Start

### Load Role Via `ansible-galaxy` Command

1. Create `requirements.yml` in ansible project root, and add this content:

   ```yaml
   # requirements.yml
   - src: https://github.com/digimokan/ans-role-shell-common
     version: master
     name: shell-common
   ```

2. From the project root directory, install/download the role:

   ```shell
   $ ansible-galaxy install --role-file requirements.yml --roles-path ./roles --force-with-deps
   ```

   * _NOTE:_ `--force-with-deps` _ensures subsequent calls download updates_

3. Include the role like any local role, from the project playbook:

   ```yaml
   # playbook.yml
   - hosts: localhost
     connection: local
     tasks:
       - name: "Configure shell-common source files for env-vars, aliases"
         include_role:
           name: shell-common
         vars:
           user_name: "admin"
   ```

## Role Options

See the role `defaults` file, for overridable vars:

  * [defaults/main.yml](../defaults/main.yml)

Define these _required_ vars for the role:

  * `user_name`: user to configure the shell-common files for

Define these _optional_ vars for the role:

  * `time_zone_tz_name`: set the system time zone
    (see [tz database time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)
    for complete list)

    _NOTE: This var may be set to_ '__auto__' _instead of a time zone. The
           script will then call out to a geo-IP API to determine the time
           zone._

## Contributing

* Feel free to report a bug or propose a feature by opening a new
  [Issue](https://github.com/digimokan/ans-role-shell-common/issues).
* Follow the project's [Contributing](CONTRIBUTING.md) guidelines.
* Respect the project's [Code Of Conduct](CODE_OF_CONDUCT.md).

