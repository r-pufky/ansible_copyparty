# copyparty
copyparty Application Proxy Server.

## Requirements
[supported platforms](https://github.com/r-pufky/ansible_copyparty/blob/main/meta/main.yml)

## Role Variables
[defaults](https://github.com/r-pufky/ansible_copyparty/tree/main/defaults/main)

### Ports
All ports and protocols have been defined for the role.

[defaults/ports.yml](https://github.com/r-pufky/ansible_copyparty/blob/main/defaults/main/ports.yml)

## Dependencies
**galaxy-ng** roles cannot be used independently. Part of
[r_pufky.media](https://github.com/r-pufky/ansible_collection_media)
collection.

## Example Playbook
Read defaults documentation.

Deploy copyparty with a minimal startup configuration.

host_vars/cpp.example.com/data/copyparty.conf
``` yaml
[global]
  i: 0.0.0.0

[accounts]
  user: {{ vault_copyparty_user_password }}

[/]
  /var/lib/copyparty-jail
  accs:
    r: *
    rwdma: user
  flags:
    grid
```

``` yaml
- name: 'copyparty server'
  hosts: 'cpp.example.com'
  become: true
  roles:
     - 'r_pufky.media.copyparty'
  vars:
    copyparty_srv_cfg: 'host_vars/copyparty.example.com/data/copyparty.conf'
```

## Development
Configure [environment](https://r-pufky.github.io/ansible_collection_docs/ansible/environment)

Run all unit tests:
``` bash
molecule test --all
```

### Releases
Release format: **{OS}-{SERVICE}-{ROLE}**

Each type inherits the versioning system used; defaulting to schematic
versioning.

`12.0.0-2.0.3-1.0.0`

* 12.0.0 - Debian 12 (bookworm).
* 2.0.3 - Service/app version.
* 1.0.0 - Role version.

Releases are branched on Debian releases:

* **[13.x.x](https://github.com/r-pufky/ansible_copyparty)**: 13 Trixie.
* **[12.x.x](https://github.com/r-pufky/ansible_copyparty/tree/12.x)**: 12 Bookworm.

## Issues
Create a bug and provide as much information as possible.

Associate pull requests with a submitted bug.

## License
[AGPL-3.0 License](https://www.tldrlegal.com/license/gnu-affero-general-public-license-v3-agpl-3-0)
 [(direct link)](https://github.com/r-pufky/ansible_copyparty/blob/main/LICENSE)

## Author Information
PGP Fingerprint: [466EEC2B67516C7117C85CE3A0BC35D16698BAB9](https://keys.openpgp.org/vks/v1/by-fingerprint/466EEC2B67516C7117C85CE3A0BC35D16698BAB9)
| [github gist](https://gist.github.com/r-pufky/a8df36977c55b5bb20829267c4c49d22)
