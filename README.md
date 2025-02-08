james_on_rpi
============
[![Ansible Lint](https://github.com/oxivanisher/role-james_on_rpi/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/oxivanisher/role-james_on_rpi/actions/workflows/ansible-lint.yml)

This role installs and configures [JamesII](https://github.com/oxivanisher/JamesII) nodes on Raspberry Pis.

Notes
-----

* Please be aware, that the `ebindkeys` functionality "conflicts" with the `infrared` stuff for james. It does not really conflict as such, but the current configuration in `files/ebindkeysrc` also triggers for events over infrared and so triggers both/twice.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

| Name          | Comment                              | Default value |
|---------------|--------------------------------------|---------------|
| james_on_rpi_install_dir  | Where will JamesII be installed  | `/opt/JamesII`          |
| james_on_rpi_cli_user  | The Linux cli user to run the interactive james command (sudo config) | `pi`          |
| james_on_rpi_git_branch  | Git branch to checkout from Github | `master`          |
| james_on_rpi_rabbitmq_server  | Rabbit MQ server name    | `james.example.lan`          |
| james_on_rpi_rabbitmq_vhost  | The Rabbit MQ vhost to use  | `james2`          |
| james_on_rpi_rabbitmq_user  | Rabbit MQ username  | `james2`          |
| james_on_rpi_rabbitmq_password  | Rabbit MQ password    | `YOURPASSWORD`          |
| james_on_rpi_rabbitmq_port  | Rabbit MQ port    | `5672`          |
| james_on_rpi_rabbitmq_fallbackport | Rabbit MQ fallback port    | `15672`          |
| james_on_rpi_features  | JamesII features to configure. List options are: <br> `i2c`, `mpd`, `evdev`, `usb_mpc_remote`, `btpresence`    | `[]`          |
| james_on_rpi_gpio_ir_rx_pin | Raspberry Pi GPIO pin for IR RX | `25`          |
| james_on_rpi_gpio_ir_tx_pin | Raspberry Pi GPIO pin for IR TX    | `4`          |
| james_on_rpi_evdev_remotes  | Current available files: <br> `atv_bedroom`, `atv_livingroom`, `atv_old_livingroom`   | `[]`          |
| james_on_rpi_lircd_default_device  | Set the LIRC default device | `auto`          |
| james_on_rpi_rpi_boot_dev | The boot device where the `config.txt` is located. Will be overwritten if `raspberry_pi_boot_dev` is set! | `/dev/mmcblk0p1` |


The `evdev` stuff uses the GPIO numbers. Please be aware, that there are three (!) pin numbering schemes. Find more information about this in the [JamesII Readme](https://github.com/oxivanisher/JamesII).

There where more `james_on_rpi_features`, but they are currently not maintained: `lircd`, `motion`
Use them at your own risk!

Example Playbook
----------------

```yaml
- name: JamesII
  hosts: james_rpi
  collections:
    - oxivanisher.raspberry_pi
  roles:
    - role: oxivanisher.raspberry_pi.james_on_rpi
      tags:
        - james2
```

License
-------

BSD

Author Information
------------------

This role is part of the [oxivanisher.raspberry_pi](https://galaxy.ansible.com/ui/repo/published/oxivanisher/raspberry_pi/) collection, and the source for that is located on [github](https://github.com/oxivanisher/collection-raspberry_pi).
