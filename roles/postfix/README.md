# postfix

Install and configure Postfix as a local MTA or relay host.

## Supported platforms

- Ubuntu 22.04+
- Debian 12+
- RHEL 9+

## Role Variables

The role interface is validated through `meta/argument_specs.yml`. Defaults are defined in `defaults/main.yml`.

```yaml
---
postfix_hostname: "{{ ansible_host.split('.')[0] }}"
postfix_domain: "{{ ansible_host.split('.')[1:] | join('.') | default('') }}"
postfix_relayhost: ''
postfix_root_mail: root
postfix_manage_service: true
postfix_service_enabled: true
postfix_service_state: started
postfix_manage_mailrc: true
postfix_mynetworks:
- 127.0.0.0/8
postfix_aliases:
  support: root
postfix_sasl_user: ''
postfix_sasl_password: ''
postfix_sasl_relayhost: '{{ postfix_relayhost }}'
postfix_inet_interfaces: loopback-only
postfix_inet_protocols: ipv4
postfix_tls_use: true
postfix_tls_security_level: encrypt
postfix_tls_cafile: ''
postfix_compatibility_level: '2'
postfix_use_sender_canonical: true
postfix_use_header_check: true
```

## Example Playbook

```yaml
- name: Apply postfix
  hosts: all
  become: true
  roles:
    - role: lenmail.mailserver.postfix
```

## Testing

The collection CI runs `ansible-lint`, `ansible-test sanity`, repository consistency tests, and per-role syntax checks using `roles/postfix/tests/test.yml`.
