# Ansible Role: Velociraptor Server Deployment

An Ansible Role that installs [Velociraptor](https://docs.velociraptor.app/) as a Server on Linux.

## Requirements

The VM having the role `ludus_velociraptor_server` must be before all other VMs with the role `ludus_velociraptor_client`!

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
velociraptor_version: "v0.72"                   # Velociraptor Major Version
velociraptor_version_patch: "v0.72.0"           # Velociraptor Minor Version

velociraptor_admin_user: "admin"
velociraptor_admin_password: "pleasechangeme"
```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: velociraptor_server
  roles:
    - ludus_velociraptor_server
  role_vars:
    velociraptor_admin_user: "admin"
    velociraptor_admin_password: "password"
```

## Example Ludus Range Config

```yaml
ludus:
  - vm_name: "{{ range_id }}-ad-dc-win2022-server-x64-1"
    hostname: "{{ range_id }}-DC01-2022"
    template: win2022-server-x64-template
    vlan: 10
    ip_last_octet: 11
    ram_gb: 6
    cpus: 4
    windows:
      sysprep: true
    domain:
      fqdn: ludus.domain
      role: primary-dc
    roles:
      - ludus_velociraptor_server
    vars:
      velociraptor_admin_user: "admin"
      velociraptor_admin_password: "password"
```

## License

GPLv3

## Author Information

This role was created by [fmurer](https://github.com/fmurer), for [Ludus](https://ludus.cloud/).
