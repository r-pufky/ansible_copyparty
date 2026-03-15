# Copyparty
Copyparty portable file server with accelerated resumable uploads, dedup,
WebDAV, SFTP, FTP, TFTP, zeroconf, media indexer, thumbnails++ all in one file.

## [Requirements][i]
Requires [r_pufky.media][g] galaxy-ng collection.

Install size: ~11MB

## Role Variables
Detailed variable use documented in defaults. See usage for role operation.

* [defaults][j] - User configurable options.

* [ports][k] - Ports are **not** managed (defined for external use).

## Usage

### Feature Flags
Tasks are gated by feature flags and executed in the following order.

  Step | Flag                      | Notes
 ------|---------------------------|-------
  1    | copyparty_flg_maintenance | Preform role maintenance tasks.
  2    | copyparty_flg_install     | Install required packages, users, etc.
  3    | copyparty_flg_config      | Install user-defined config.

### Example Playbooks

#### New Deployments
A minimal config will be deployed if no configuration is specified. This will
deploy a working Copyparty install using **/d** as the default root directory,
**/etc/opt/copyparty** for configuration, with **user**/**user** as the default
user.

``` yaml
- name: 'Copyparty'
  ansible.builtin.include_role:
    name: 'r_pufky.media.copyparty'
```

See [Existing Deployments](#existing-deployments) for reproducible deployments.

#### Existing Deployments
Manage additional files and directories (data storage locations, etc.) outside
of role if used **within** the config. Must be accessible to
**copyparty_srv_user** account.

host_vars/cp.example.com/copyparty.conf
``` ini
# Create a basic customized config.
#
# https://github.com/9001/copyparty/blob/hovudstraum/docs/example.conf

[global]
  i: 0.0.0.0

[accounts]
  user: {{ vault_copyparty_user_password }}

[/]
  /home/user/shared
  accs:
    r: *
    rwdma: user
  flags:
    grid
```

``` yaml
- name: 'New Copyparty Deployment'
  ansible.builtin.include_role:
    name: 'r_pufky.media.copyparty'
  vars:
    copyparty_cfg_file: 'host_vars/cp.example.com/copyparty.conf'
```

## Development
Configure [environment][a].

``` bash
# Run all tests.
molecule test --all
```

Testing variables:

  Variable          | type | Description
 -------------------|------|-------------
  url_inject_enable | bool | Disable **get_url** to inject files locally.

### [Releases][b]
Focused on service deployment with templated configuration to minimize role
churn due to inconsistent and rapid rolling release cycle.

 Release | Debian | Ansible | copyparty | Notes
---------|--------|---------|-----------|-------
 3.x.x   | 13     | 2.20    | v1.20.12  | Update to Ansible 2.20 collection dependencies.
 2.x.x   | 13     | 2.20    | v1.20.10  | Ansible 2.20, feature flags, and semantic versioning.
 1.x.x   | 13     | 2.16    | v1.15.1   | Initial release.

## Issues
Create a bug and provide as much information as possible.

Associate pull requests with a submitted bug.

## License
[AGPL-3.0 License][c] | [direct link][f]

## Author Information
PGP: [466EEC2B67516C7117C85CE3A0BC35D16698BAB9][d] | [github gist][e]


[a]: https://r-pufky.github.io/ansible_docs
[b]: https://semver.org/spec/v2.0.0
[c]: https://www.tldrlegal.com/license/gnu-affero-general-public-license-v3-agpl-3-0
[d]: https://keys.openpgp.org/vks/v1/by-fingerprint/466EEC2B67516C7117C85CE3A0BC35D16698BAB9
[e]: https://gist.github.com/r-pufky/a8df36977c55b5bb20829267c4c49d22

[f]: https://github.com/r-pufky/ansible_copyparty/blob/main/LICENSE
[g]: https://github.com/r-pufky/ansible_collection_media
[i]: https://github.com/r-pufky/ansible_copyparty/blob/main/meta/main.yml
[j]: https://github.com/r-pufky/ansible_copyparty/tree/main/defaults/main/main.yml
[k]: https://github.com/r-pufky/ansible_copyparty/blob/main/defaults/main/ports.yml