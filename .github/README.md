# ans_role_config_bitwarden_cli

Install and configure the Bitwarden CLI password manager utility.

[![Release](https://img.shields.io/github/release/digimokan/ans_role_config_bitwarden_cli.svg?label=release)](https://github.com/digimokan/ans_role_config_bitwarden_cli/releases/latest "Latest Release Notes")
[![License](https://img.shields.io/badge/license-MIT-blue.svg?label=license)](LICENSE.md "Project License")

## Table Of Contents

* [Purpose](#purpose)
* [Supported Operating Systems](#supported-operating-systems)
* [Dependencies](#dependencies)
* [Quick Start](#quick-start)
    * [Use From Playbook](#use-from-playbook)
* [Role Options](#role-options)
* [Contributing](#contributing)

## Purpose

* Install the [Bitwarden CLI](https://bitwarden.com/help/cli/) password
  manager utility.
* Simplify Bitwarden CLI usage by providing a
  [utility script](../templates/do_bitwarden_cli.j2).

## Supported Operating Systems

* Arch Linux
* FreeBSD

## Dependencies

* FreeBSD Linux Binary-Compatibility Layer service is running (required for
  FreeBSD Bitwarden CLI app, checked via [var](../defaults/main/os/freebsd.yml)).

## Quick Start

### Use From Playbook

1. Create `requirements.yml` in ansible project root, and add this content:

   ```yaml
   # requirements.yml
   - src: https://github.com/digimokan/ans_role_config_bitwarden_cli
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
       - name: "Install and configure the Bitwarden CLI password manager utility"
         ansible.builtin.include_role:
           name: ans_role_config_bitwarden_cli
         vars:
           bitwarden_user_name: "user2"
           bitwarden_cli_api_key_client_id: "some-api-key-client-id"
           bitwarden_cli_api_key_client_secret: "some-api-key-client-secret"
           bitwarden_cli_exec_jq_cmd: "jq"
           bitwarden_cli_exec_xsel_cmd: "xsel"
           bitwarden_cli_exec_fzf_cmd: "fzf"
   ```

## Role Options

See the role `defaults` files for main role vars listings:

  * [defaults](../defaults/main/)

Define these _required_ vars for the role:

  * `bitwarden_user_name`: user name of main Bitwarden user
  * `bitwarden_check_freebsd_linux_compat_cmd`: check linux compat (for FreeBSD)

Define these _conditionally-required_ vars, as needed:

  * `bitwarden_master_password`: required when not logged in, vault not unlocked

## Contributing

* Feel free to report a bug or propose a feature by opening a new
  [Issue](https://github.com/digimokan/ans_role_config_bitwarden_cli/issues).
* Follow the project's [Contributing](CONTRIBUTING.md) guidelines.
* Respect the project's [Code Of Conduct](CODE_OF_CONDUCT.md).

