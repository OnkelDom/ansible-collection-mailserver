# Ansible Collection: `lenmail.mailserver`

Diese Collection bundelt Mailserver-Rollen fuer Linux-Systeme und fuehrt die kopierten Einzelrollen in einer einheitlichen Collection-Struktur zusammen.

Jede Rolle erhaelt ein standardisiertes Geruest mit:

- `README.md`
- `meta/main.yml`
- `meta/argument_specs.yml`
- `tests/test.yml`

## Zielplattformen

Die Collection ist auf folgende Baseline ausgerichtet:

- Ubuntu 22.04+
- Debian 12+
- RHEL 9+

Nicht jede Rolle ist auf jeder Plattform sinnvoll. Effektiv unterstuetzte Plattformen sind pro Rolle im jeweiligen `README.md` und in `meta/main.yml` dokumentiert.

## Rollen

- `dovecot`: installiert den Dovecot-IMAP/POP3-Dienst mit sicherem Minimal-Setup
- `opendkim`: installiert und konfiguriert OpenDKIM fuer ausgehende Signaturen
- `postfix`: installiert und konfiguriert Postfix als MTA bzw. Relay

## Installation

```bash
ansible-galaxy collection install git+https://github.com/lenmail/ansible-collection-mailserver.git
```

Oder ueber eine `requirements.yml`:

```yaml
---
collections:
  - name: git+https://github.com/lenmail/ansible-collection-mailserver.git
```

## Verwendung

```yaml
---
- name: Configure mail services
  hosts: mail
  become: true
  roles:
    - role: lenmail.mailserver.postfix
    - role: lenmail.mailserver.opendkim
```

## Entwicklung

Lokale Hilfsmittel:

- Collection-Abhaengigkeiten: `requirements.yml`
- Test-Abhaengigkeiten: `requirements-test.txt`
- Rollen-Generator: `tools/generate_role_scaffold.py`

Generator ausfuehren:

```bash
python3 tools/generate_role_scaffold.py
```

Drift pruefen:

```bash
python3 tools/generate_role_scaffold.py --check
```

## Lizenz

MIT
