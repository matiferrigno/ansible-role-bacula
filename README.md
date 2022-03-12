# Ansible Role: Bacula

An Ansible Role that installs Bacula on Linux.

## Example playbook

```yaml
---

- hosts: all
  tasks:
  - name: Gathering info
    setup: {}

- hosts: bacula-client
  tasks:
    - include_role:
        name: bacula
        tasks_from: fd

- hosts: bacula-storage
  tasks:
    - include_role:
        name: bacula
        tasks_from: sd

- hosts: bacula-director
  tasks:
    - include_role:
        name: bacula
        tasks_from: dir
```

Check test/inventory/

## License

MIT / BSD

## Author Information


This role was created in 2020 by Matías Emanuel Ferrigno.