# opendkim

Install and configure OpenDKIM for outbound mail signing.

## Supported platforms

- Ubuntu 22.04+
- Debian 12+
- RHEL 9+

## Role Variables

The role interface is validated through `meta/argument_specs.yml`. Defaults are defined in `defaults/main.yml`.

```yaml
---
opendkim_manage_service: true
opendkim_service_enabled: true
opendkim_service_state: started
opendkim_manage_selinux: true
opendkim_config:
  AutoRestart: Yes
  AutoRestartRate: 10/1h
  Syslog: yes
  SyslogSuccess: yes
  LogWhy: yes
  Canonicalization: relaxed/simple
  Mode: sv
  SubDomains: no
  Socket: inet:8891@127.0.0.1
  SignatureAlgorithm: rsa-sha256
  PidFile: /run/opendkim/opendkim.pid
  UserID: opendkim:opendkim
  KeyTable: file:/etc/opendkim/KeyTable
  SigningTable: refile:/etc/opendkim/SigningTable
  ExternalIgnoreList: /etc/opendkim/TrustedHosts
  InternalHosts: /etc/opendkim/TrustedHosts
opendkim_domains:
- domain: example.com
  selector: default
opendkim_trustedhosts:
- 127.0.0.1
- ::1
- localhost
```

## Example Playbook

```yaml
- name: Apply opendkim
  hosts: all
  become: true
  roles:
    - role: lenmail.mailserver.opendkim
```

## Testing

The collection CI runs `ansible-lint`, `ansible-test sanity`, repository consistency tests, and per-role syntax checks using `roles/opendkim/tests/test.yml`.
