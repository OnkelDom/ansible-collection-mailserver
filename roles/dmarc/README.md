# dmarc

Install and configure OpenDMARC for DMARC policy checks.

## Supported platforms

- Ubuntu 22.04+
- Debian 12+
- RHEL 9+

## Role Variables

The role interface is validated through `meta/argument_specs.yml`. Defaults are defined in `defaults/main.yml`.

```yaml
---
dmarc_manage_service: true
dmarc_service_enabled: true
dmarc_service_state: started
dmarc_manage_selinux: true
dmarc_authserv_id: '{{ ansible_fqdn | default(ansible_hostname) }}'
dmarc_ignore_hosts:
- 127.0.0.1
- ::1
- localhost
dmarc_config:
  AuthservID: '{{ dmarc_authserv_id }}'
  IgnoreAuthenticatedClients: 'true'
  IgnoreHosts: /etc/opendmarc/ignore.hosts
  PidFile: /run/opendmarc/opendmarc.pid
  RejectFailures: 'false'
  Socket: local:/run/opendmarc/opendmarc.sock
  Syslog: 'true'
  TrustedAuthservIDs: '{{ dmarc_authserv_id }}'
  UMask: '007'
```

## Example Playbook

```yaml
- name: Apply dmarc
  hosts: all
  become: true
  roles:
    - role: lenmail.mailserver.dmarc
```

## Testing

The collection CI runs `ansible-lint`, `ansible-test sanity`, repository consistency tests, and per-role syntax checks using `roles/dmarc/tests/test.yml`.
