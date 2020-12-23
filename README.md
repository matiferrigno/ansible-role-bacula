[![Ansible-lint rules explanation][ansible-lint]](https://ansible-lint.readthedocs.io/en/latest/default_rules.html)

[ansible-lint]: https://img.shields.io/badge/Ansible--lint-rules%20table-blue.svg


# Ansible Role: Bacula

An Ansible Role that installs Bacula on Linux.

## Requirements

* ansible:2.10
## Role Variables

### Full

defaults/main.yml has enough docs.

### Minimal configuration

*Install Bacula Director, Catalog and Storage.*

```yaml
# install geerlingguy.mysql
bacula_mysql_root_password: "changeme!"

# Catalog
bacula_catalog_dbname: "bacula"
bacula_catalog_dbuser: "baculausr"
bacula_catalog_dbpass: "changeme!"

# Director
bacula_dir_fqdn: "backup-dir.fqdn"
bacula_dir_pass: "changeme!"

# Storage
bacula_sd_fqdn: "backup-sd.fqdn"

# policies template (jinja2) folder
bacula_policies_template_folder: "{{ playbook_dir + '/templates/bacula/policies.d' }}"

# Clients (only configure server, it do not install bacula-fd on client)
bacula_clients:
  - name: "client-01"
    enabled: yes
    host: "10.1.0.10"
    fqdn: "client-01.fqdn"
    pass: "<pass client>"
    policies:
     - name: my-own-policy
       enabled: yes
       files:
       - "/root"
       - "/home/"
       - "/var/lib/docker"
```
* a jinja2 policy template file must exists in directory ```{{ bacula_policies_template_folder directory }}``` whitch name should be *my-own-policy.conf.j2*.

* an example is included on templates/policies.d/example.conf.j2


## Dependencies

```yaml
dependencies:
  - name: geerlingguy.mysql
```

## Example Playbook


```yaml
    - hosts: all
      roles:
         - { role: matiasferrigno.bacula }
```

## Testing

### Requirements

  * molecule 3.2.0 using python 3.9
    * delegated:3.2.0 from molecule
    * podman:0.3.0 from molecule_podman
  * podman 2.1

```
$ molecule check
```

## TODO

Split:

- bacula-director
- bacula-catalog
- bacula-storage

## License


MIT / BSD

## Author Information


This role was created in 2020 by Matías Emanuel Ferrigno.