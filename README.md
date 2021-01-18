# Ansible Role: Grafana Cloud Agent

![Ansible Lint](https://github.com/nleiva/ansible-role-grafana-agent/workflows/Ansible%20Lint/badge.svg)

Installs [Grafana Cloud Agent](https://github.com/grafana/agent) on RedHat/CentOS or Debian/Ubuntu servers to collect observability data and sends it to [Grafana Cloud](https://grafana.com/products/cloud/).

This role installs and configures the latest version of (Grafana Cloud Agent)[https://github.com/grafana/agent] from [GitHub releases](https://github.com/grafana/agent/releases). It also creates a [systemd service to manage the agent](https://grafana.com/docs/grafana-cloud/agent/agent_as_service/).

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    grafana_user: <username>
    grafana_password: <password>

[Grafana Cloud](https://grafana.com/products/cloud/) username and password for the the Linux integration/Prometheus data source. [Create account](https://grafana.com/signup/cloud/connect-account).

    agent_location: /usr/local/bin

Location where the agent's binary will be installed. The default location (`/usr/local/bin`) is preferred in systems where SELinux is enabled.

    config_location: /etc/grafana

Location where the agent's config will be installed. The default location (`/etc/grafana`) is preferred in systems where SELinux is enabled.

By default, this role will ensure [Grafana Cloud Agent](https://github.com/grafana/agent) is running and enabled at boot.

## Overriding configuration templates

- [ ] TODO


## Dependencies

None.

## Example Playbook

    - hosts: server
      roles:
        - { role: nleiva.grafana-agent }

## License

GPL-3.0 License

## Author Information

This role was created in 2021 by [Nicolas Leiva](https://github.com/nleiva).