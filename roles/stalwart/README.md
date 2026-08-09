# stalwart

Deploy the Stalwart mail and collaboration server as a hardened Docker service.

## Supported platforms

- Ubuntu 22.04+
- Debian 12+

## Role Variables

The role interface is validated through `meta/argument_specs.yml`. Defaults are defined in `defaults/main.yml`.

```yaml
---
stalwart_image: stalwartlabs/stalwart:v0.16.15
stalwart_service_name: stalwart
stalwart_base_path: /data/stalwart
stalwart_config_path: '{{ stalwart_base_path }}/config'
stalwart_data_path: '{{ stalwart_base_path }}/data'
stalwart_public_url: ''
stalwart_recovery_admin_user: admin
stalwart_recovery_admin_password: ''
stalwart_recovery_mode: false
stalwart_recovery_port: 8080
stalwart_restart_policy: unless-stopped
stalwart_manage_firewall: false
stalwart_firewall_tcp_ports:
- 25
- 465
- 587
- 143
- 993
- 110
- 995
- 4190
- 8080
stalwart_service_enabled: true
stalwart_service_state: started
```

## Example Playbook

```yaml
- name: Apply stalwart
  hosts: all
  become: true
  roles:
    - role: onkeldom.mailserver.stalwart
```

## Testing

The collection CI runs `ansible-lint`, `ansible-test sanity`, repository consistency tests, and per-role syntax checks using `roles/stalwart/tests/test.yml`.
