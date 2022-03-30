# ans_role_config_shell

Set up commonly-sourced config files for all shells.

[![Release](https://img.shields.io/github/release/digimokan/ans_role_config_shell.svg?label=release)](https://github.com/digimokan/ans_role_config_shell/releases/latest "Latest Release Notes")
[![License](https://img.shields.io/badge/license-MIT-blue.svg?label=license)](LICENSE.md "Project License")

## Table Of Contents

* [Purpose](#purpose)
* [Supported Operating Systems](#supported-operating-systems)
* [Quick Start](#quick-start)
    * [Use From Playbook](#use-from-playbook)
    * [Use From Parent Role As Dependency](#use-from-parent-role-as-dependency)
* [Role Options](#role-options)
* [Shell Config File Layout](#shell-config-file-layout)
* [Contributing](#contributing)

## Purpose

* Set up shell sourcing layout for single environment vars file
  (`shell-common/env_vars`).
* Set up aliases and console-config layout, customizable per shell type.
* Do the right thing for all combinations of login, non-login, interactive, and
  non-interactive shell invocations.
* Provide role "utility tasks" to simplify setting env vars, aliases, etc.
* Support _bash_, _zsh_, _ksh_, _fish_, and _sh_ shell types.

## Supported Operating Systems

* Arch Linux.

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

4. Use a role "utility task" (from the `inc` directory) to add a common alias:

   ```yaml
   - name: "Add common ls long listing alias"
     ansible.builtin.include_role:
       name: ans_role_config_shell
       tasks_from: inc/add_common_interactive_lines.yml
     vars:
       user_name: "admin"
       description: "add long listing ls alias"
       config_lines: "alias ll='ls -la'"
   ```
5. The following utility tasks are available:

    * Written in shell-agnostic syntax, and runs for all shells:
        * `inc/add_common_env_var_lines`
        * `inc/add_common_login_actions_lines`
        * `inc/add_common_interactive_lines`
    * Written in a shell-specific syntax, and only runs for specific shell:
        * `inc/add_bash_interactive_lines`
        * `inc/add_fish_interactive_lines`
        * `inc/add_zsh_interactive_lines`
        * `inc/add_ksh_interactive_lines`

### Use From Parent Role As Dependency

1. List in parent role's `meta/main.yml`, with `never` tag to avoid duplication:

   ```yaml
   dependencies:
     - src: https://github.com/digimokan/ans_role_config_shell
       tags:
         - never
   ```

2. Call role with step 3 or 4 from [Use From Playbook](#use-from-playbook)
   section.

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
  [Issue](https://github.com/digimokan/ans_role_config_shell/issues).
* Follow the project's [Contributing](CONTRIBUTING.md) guidelines.
* Respect the project's [Code Of Conduct](CODE_OF_CONDUCT.md).

