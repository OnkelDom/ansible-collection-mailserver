# dovecot

Install and configure a basic Dovecot IMAP/POP3 service.

## Supported platforms

- Ubuntu 22.04+
- Debian 12+
- RHEL 9+

## Role Variables

The role interface is validated through `meta/argument_specs.yml`. Defaults are defined in `defaults/main.yml`.

```yaml
---
dovecot_manage_service: true
dovecot_service_enabled: true
dovecot_service_state: started
```

## Example Playbook

```yaml
- name: Apply dovecot
  hosts: all
  become: true
  roles:
    - role: lenmail.mailserver.dovecot
```

## Testing

The collection CI runs `ansible-lint`, `ansible-test sanity`, repository consistency tests, and per-role syntax checks using `roles/dovecot/tests/test.yml`.
