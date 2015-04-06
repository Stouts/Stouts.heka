Stouts.heka
===========

[![Build Status](http://img.shields.io/travis/Stouts/Stouts.heka.svg?style=flat-square)](https://travis-ci.org/Stouts/Stouts.heka)
[![Galaxy](http://img.shields.io/badge/galaxy-Stouts.heka-blue.svg?style=flat-square)](https://galaxy.ansible.com/list#/roles/1907)

Ansible role which manage [heka](http://http://http://hekad.readthedocs.org/)

* Install and configure Heka


#### Variables

Here is the list of all variables and their default values:

```yaml
heka_enabled: yes                           # The role is enabled
heka_version: 0.9.1                         # Set version
heka_deb: https://github.com/mozilla-services/heka/releases/download/v{{heka_version}}/heka_{{heka_version}}_amd64.deb

heka_etc_dir: /etc/heka.d

heka_base_dir: /var/cache/hekad
heka_pid_file: /var/run/hekad.pid
heka_maxproc: 1

heka_inputs: ""
heka_decoders: ""
heka_encoders: ""
heka_outputs: ""
```

#### Usage

Add `Stouts.heka` to your roles and setup the variables in your playbook file.
Example:

```yaml

- hosts: all

  roles:
    - Stouts.heka

  vars:
    heka_inputs: |
        [UdpInput]
        address = ":2003"
        decoder = "StatsToFieldsDecoder"

    heka_decoders: |
        [StatsToFieldsDecoder]

    heka_encoders: |
        [PayloadEncoder]

    heka_outputs: |
        [FileOutput]
        message_matcher = "TRUE"
        encoder = "PayloadEncoder"
        path = "/tmp/heka"
```

#### License

Licensed under the MIT License. See the LICENSE file for details.

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Stouts/Stouts.heka/issues)!
