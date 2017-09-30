# ansible-macos-standby
Ansible role to manage macOS standby, hibernate and sleep settings.

[![Build Status](https://img.shields.io/travis/feffi/ansible-macos-standby.svg)](https://travis-ci.org/feffi/ansible-macos-standby) [![Github All Releases](https://img.shields.io/github/downloads/feffi/ansible-macos-standby/total.svg)](https://github.com/feffi/ansible-macos-standby) [![GitHub forks](https://img.shields.io/github/forks/feffi/ansible-macos-standby.svg?style=social&label=Fork)](https://github.com/feffi/ansible-macos-standby) [![GitHub stars](https://img.shields.io/github/stars/feffi/ansible-macos-standby.svg?style=social&label=Star)](https://github.com/feffi/ansible-macos-standby) [![GitHub watchers](https://img.shields.io/github/watchers/feffi/ansible-macos-standby.svg?style=social&label=Watch)](https://github.com/feffi/ansible-macos-standby) [![Twitter Follow](https://img.shields.io/twitter/follow/feffi1.svg?style=social&label=Follow)](https://twitter.com/feffi1) [![License](http://img.shields.io/:license-mit-blue.svg)](https://github.com/feffi/ansible-macos-standby/blob/master/LICENSE)

## Requirements
- Ansible 2.3

### ansible.cfg
```
hash_behaviour = merge
```

## Install
Just add the role to your ``requirements.yml`` file:
```yaml
- src: https://github.com/feffi/ansible-macos-standby.git
  name: feffi.macos-standby
```

## Role Variables
All role based variables are listed below, along with default values:

```yaml
---
macos_standby:
  # Set standby delay in seconds, default = 3600, 24 hours = 86400, disabled = false
  standby_delay: 86400

  # Set hibernate mode:
  # hibernatemode = 0 (binary 0000) by default on supported desktops. The system will not back memory up to
  #   persistent storage. The system must wake from the contents of memory; the system will lose context on
  #   power loss. This is, historically, plain old sleep.
  #
  # hibernatemode = 3 (binary 0011) by default on supported portables. The system will store a copy of mem-ory memory
  #   ory to persistent storage (the disk), and will power memory during sleep. The system will wake from
  #   memory, unless a power loss forces it to restore from disk image.
  #
  # hibernatemode = 25 (binary 0001 1001) is only settable via pmset. The system will store a copy of mem-ory memory
  #   ory to persistent storage (the disk), and will remove power to memory. The system will restore from
  #   disk image. If you want "hibernation" - slower sleeps, slower wakes, and better battery life, you
  #   should use this setting.
  hibernate_mode: 0

  # Remove the sleep image file to save disk space
  remove_sleepimage: false

  # Automatically illuminate built-in MacBook keyboard in low light
  bezel_dim: true

  # Turn off keyboard illumination when computer is not used for x seconds
  bezel_dim_delay: 300

  # Automatic termination of inactive apps
  terminate_inactive: false

  # Set display sleep time delay in minutes
  sleep_display: "Never"

  # Set computer sleep time delay in minutes
  sleep_computer: "Never"

  # Set harddisk sleep time delay in minutes
  sleep_harddisk: "Never"

  # Set wake on network access to either <on> or <off>
  wake_on_lan: true

  # Sleep on pressing the power button, direct sleep = true, show dialog = false
  powerbutton_sleep: false

  # Set usage of PowerNap
  powernap: true

  # wake the machine when the laptop lid (or clamshell) is opened
  lidwake: true

  # wake the machine when power source (AC/battery) is changed
  acwake: false


  # display sleep will use an intermediate half-brightness state between full brightness and fully off
  halfdim: true

  # prevent idle system sleep when any tty (e.g. remote login session) is 'active'. A tty is 'inactive'
  # only when its idle time exceeds the system sleep timer.
  ttyskeepawake: true

  # Destroy File Vault Key when going to standby mode. By default File vault keys are retained even
  # when system goes to standby. If the keys are destroyed, user will be prompted to enter the
  # password while coming out of standby mode.
  destroyfvkeyonstandby: false
```

## Dependencies
None.

## Example Playbook

```yaml
    - hosts: all
      vars:
        macos_standby:
          standby_delay: 86400
          hibernate_mode: 0
          remove_sleepimage: false
          bezel_dim: true
          bezel_dim_delay: 300
          terminate_inactive: false
          sleep_display: "Never"
          sleep_computer: "Never"
          sleep_harddisk: "Never"
          wake_on_lan: true
          powerbutton_sleep: false
          powernap: true
          lidwake: true
          acwake: false
          halfdim: true
          ttyskeepawake: true
          destroyfvkeyonstandby: false
      roles:
        - { role: feffi.macos-standby }
```
Or with local parameters:

```yaml
    - hosts: all
      roles:
        - { role: feffi.macos-standby,
            macos_standby: {
              standby_delay: 86400,
              hibernate_mode: 0,
              remove_sleepimage: false,
              bezel_dim: true,
              bezel_dim_delay: 300,
              terminate_inactive: false,
              sleep_display: "Never",
              sleep_computer: "Never",
              sleep_harddisk: "Never",
              wake_on_lan: true,
              powerbutton_sleep: false,
              powernap: true,
              lidwake: true,
              acwake: false,
              halfdim: true,
              ttyskeepawake: true,
              destroyfvkeyonstandby: false
          }
        }
```
