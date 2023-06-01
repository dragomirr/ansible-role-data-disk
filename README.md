# Ansible role data disk

Ansible role for formatting and mounting block devices. Tested with ansible 2.15, but probably will work with anything greater than or equal to 2.10.

Currently it is not possible to partition block device, you can only use whole block device.

By default it will use `uuid` if `label` is not specified.


[Changelog](./CHANGELOG.md)

## Requirements

Collections:

  * ansible.posix
  * community.general

## Role variables

Check `defaults/main.yml` for example and `vars/main.yml` for default values. Defauls in `vars/main.yml` are meant for `ext4`.

  * `data_disk_devices` -- list of devices to format and mount.
  * `data_disk_mount_by_device_name` -- set to `true` if mounting by device name is required. For this to work `label` should not be set.

## Dependencies

None.

## Example playbook

```yaml
---
- hosts: servers
  become: true

  roles:
    - role: dragomirr.data_disk
      data_disk_devices:
        - device: /dev/nvme2n1
          mountpoint: /var/lib/pgsql
          label: DATABASE
          mode: "0700"
          mount_opts: discard,rw,nobarrier,noquota,noatime,nofail,data=writeback,commit=60
        - device: /dev/sdb
          mountpoint: /mnt/sdb
```

## Licence

GPL3