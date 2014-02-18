# Fail2ban Role for Ansible

This role installs [fail2ban](http://www.fail2ban.org/) which is a service that scans log files (e.g. /var/log/apache/error_log) and bans IPs that show malicious signs.

## Requirements

This role requires [Ansible](http://www.ansibleworks.com/) version 1.4 or higher and the Debian/Ubuntu platform.

## Role Variables

The variables that can be passed to this role and a brief description about
them are as follows (additional variables are available in the source):

```yaml
# The default list of machines that are white-listed
fail2ban_ignoreip:
  - 127.0.0.1/8

# The default duration (in seconds) an IP will be banned
fail2ban_bantime: 86400

# The default number of matches that trigger a ban action on the IP
fail2ban_maxretry: 3

# The default banning action
fail2ban_banaction: 'iptables-multiport'

# The default action executed on ban: ban and send email with whois report
fail2ban_action: '%(action_mwl)s'

# The default recipient of email reports
fail2ban_destemail: 'root@localhost'

# The default port for monitoring SSH service
fail2ban_sshport: 22
```

## Examples

1. Install fail2ban with default settings

    ```yaml
    ---
    # This playbook installs fail2ban
    
    - name: Apply fail2ban to all nodes
      hosts: all
      roles:
        - fail2ban
    ```

2. Install with custom settings

    ```yaml
    ---
    # This playbook installs fail2ban
    
    - name: Apply fail2ban to all nodes
      hosts: all
      roles:
        - { role: fail2ban,
            fail2ban_bantime: 600,
            fail2ban_sshport: 2222
          }
    ```

## Dependencies

None.

## License

MIT.
