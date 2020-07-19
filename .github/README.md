# ans-role-config-shell

Set up commonly-sourced config files for all shells.

[![Release](https://img.shields.io/github/release/digimokan/ans-role-config-shell.svg?label=release)](https://github.com/digimokan/ans-role-config-shell/releases/latest "Latest Release Notes")
[![License](https://img.shields.io/badge/license-MIT-blue.svg?label=license)](LICENSE.md "Project License")

## Table Of Contents

* [Purpose](#purpose)
* [Supported Operating Systems](#supported-operating-systems)
* [Quick Start](#quick-start)
    * [Load Role Via `ansible-galaxy` Command](#load-role-via-ansible-galaxy-command)
* [Role Options](#role-options)
* [Shell Config File Layout](#shell-config-file-layout)
* [Contributing](#contributing)

## Purpose

* Set up shell sourcing layout for single environment vars file
  (`shell-common/env_vars`).
* Set up aliases and console-config layout, customizable per shell type.
* Do the right thing for all combinations of login, non-login, interactive, and
  non-interactive shell invocations.
* Support _bash_, _zsh_, _ksh_, _fish_, and _sh_ shell types.

## Supported Operating Systems

* Arch Linux.

## Quick Start

### Load Role Via `ansible-galaxy` Command

1. Create `requirements.yml` in ansible project root, and add this content:

   ```yaml
   # requirements.yml
   - src: https://github.com/digimokan/ans-role-config-shell
     version: master
     name: config-shell
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
       - name: "Set up commonly-sourced config files for all shells"
         include_role:
           name: config-shell
         vars:
           user_name: "admin"
   ```

## Role Options

See the role `defaults` file, for overridable vars:

  * [defaults/main.yml](../defaults/main.yml)

Define these _required_ vars for the role:

  * `user_name`: user to set up the shell config files for

## Shell Config File Layout

```
├─┬ ~/.shell-config/
│ │
│ ├─┬ shell-common/      # common
│ │ │
│ │ ├── env_vars         # environment vars: APPEND YOURS HERE
│ │ ├── interactive      # aliases and console-config: APPEND YOURS HERE
│ │ ├── logout_actions   # logout actions: APPEND YOURS HERE
│ │ └── std_env          # $ENV config: do not modify
│ │
│ ├─┬ bash/              # bash-only
│ │ │
│ │ └── interactive      # aliases and console-config: APPEND YOURS HERE
│ │
│ ├─┬ zsh/               # zsh-only
│ │ │
│ │ └── interactive      # aliases and console-config: APPEND YOURS HERE
│ │
│ ├─┬ ksh/               # ksh-only
│ │ │
│ │ └── interactive      # aliases and console-config: APPEND YOURS HERE
│ │
│ ├─┬ fish/              # fish-only
│ │ │
│ │ └── interactive      # aliases and console-config: APPEND YOURS HERE
│ │
│ └─┬ sh/                # system-shell-only
│   │
│   └── interactive      # aliases and console-config: APPEND YOURS HERE
│
```

## Contributing

* Feel free to report a bug or propose a feature by opening a new
  [Issue](https://github.com/digimokan/ans-role-config-shell/issues).
* Follow the project's [Contributing](CONTRIBUTING.md) guidelines.
* Respect the project's [Code Of Conduct](CODE_OF_CONDUCT.md).

