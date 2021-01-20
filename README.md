# Ansible role: prometheus-nginxlog-exporter

[![Build Status](https://travis-ci.com/mbaran0v/ansible-role-prometheus-nginxlog-exporter.svg?branch=master)](https://travis-ci.com/mbaran0v/ansible-role-prometheus-nginxlog-exporter) [![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT) [![GitHub tag](https://img.shields.io/github/tag/mbaran0v/ansible-role-prometheus-nginxlog-exporter.svg)](https://github.com/mbaran0v/ansible-role-prometheus-nginxlog-exporter/tags/) [![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.svg?v=103)](https://github.com/ellerbrock/open-source-badges/) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

Ansible role for install and configure [Prometheus Nginx logs Exporter](https://github.com/martin-helmich/prometheus-nginxlog-exporter). Currently this works on Debian and RedHat based linux systems. Tested platforms are:

* Ubuntu 16.04
* CentOS 7

Requirements
------------

No special requirements; note that this role requires root access, so either run it in a playbook with a global become: yes

Role Variables
--------------

The variables that can be passed to this role and a brief description about them are as follows. (For all variables, take a look at defaults/main.yml)

```yaml
nginxlog_exporter_version: 1.3.0
```
version for installation

```yaml
nginxlog_exporter_listen_port: 4040
```
listen port

```yaml
nginxlog_exporter_root_dir: /opt/nginxlog_exporter
```
directory for installation

```yaml
nginxlog_exporter_config_vars: |
  listen:
    port: {{ nginxlog_exporter_listen_port }}
    address: {{ nginxlog_exporter_listen_address }}
  namespaces:
    - name: nginx
      format: "$remote_addr [$time_local] \"$request\" $status $body_bytes_sent $request_time $upstream_response_time"
      source_files:
        - "/var/log/nginx/exporter.log"
      histogram_buckets: [.1, .3, .5, .7, 1, 3, 5, 7]
```
configuration file https://github.com/martin-helmich/prometheus-nginxlog-exporter#configuration-file

Dependencies
------------

None

Example Playbook
----------------

```yaml
- hosts: app
  become: yes
  roles:
      - mbaran0v.prometheus-nginxlog-exporter
```

License
-------

MIT / BSD

Author Information
------------------

This role was created in 2019 by [Maxim Baranov](https://github.com/mbaran0v).
