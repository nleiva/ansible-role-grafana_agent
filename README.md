# Ansible Role: Grafana Cloud Agent

![Ansible Lint](https://github.com/nleiva/ansible-role-grafana_agent/workflows/Ansible%20Lint/badge.svg?branch=main) ![Ansible Role](https://img.shields.io/ansible/role/52768?style=plastic) ![Quality Score](https://img.shields.io/ansible/quality/52768) ![Downloads](https://img.shields.io/ansible/role/d/52768?style=plastic)

Installs [Grafana Cloud Agent](https://github.com/grafana/agent) on RedHat/CentOS or Debian/Ubuntu servers to collect observability data and sends it to [Grafana Cloud](https://grafana.com/products/cloud/). Available on [Galaxy](https://galaxy.ansible.com/nleiva/grafana_agent).

This role installs and configures the latest version of [Grafana Cloud Agent](https://github.com/grafana/agent) from [GitHub releases](https://github.com/grafana/agent/releases). It also creates a [systemd service to manage the agent](https://grafana.com/docs/grafana-cloud/agent/agent_as_service/).

It optionally installs [Promtail](https://grafana.com/docs/loki/latest/clients/promtail/), which is an agent which ships the contents of local logs to [Grafana Cloud](https://grafana.com/products/cloud/) ([Loki](https://grafana.com/oss/loki/)).

**WHY**? => [Monitoring your home lab devices in the cloud for free](https://nleiva.medium.com/monitoring-your-home-lab-devices-in-the-cloud-for-free-54c4d11ac471). 

## Requirements

None. Other than an account on [Grafana Cloud](https://grafana.com/products/cloud/) -> [Create account](https://grafana.com/signup/cloud/connect-account).

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`). You can get the values for your enviroment from the [Grafana Cloud Portal](https://grafana.com/docs/grafana-cloud/cloud-portal/).

    prometheus_user: <username>

Each service in [Grafana Cloud](https://grafana.com/products/cloud/) has a unique service id or user. Once in the [Grafana Cloud Portal](https://grafana.com/docs/grafana-cloud/cloud-portal/) click on Prometheus to get the value you need to provide for `prometheus_user`.

    grafana_api_key: <key>

You can generate a new API Key in the API Keys section of the [Grafana Cloud Portal](https://grafana.com/docs/grafana-cloud/cloud-portal/). The role has to be `MetricsPublisher`.

    agent_location: /usr/local/bin

Location where the [Grafana Cloud Agent](https://github.com/grafana/agent)'s binary will be installed. The default location (`/usr/local/bin`) is preferred in systems where SELinux is enabled.

    config_location: /etc/grafana

Location where the [Grafana Cloud Agent](https://github.com/grafana/agent)'s config will be stored. The default location (`/etc/grafana`) is preferred in systems where SELinux is enabled.

By default, this role will ensure [Grafana Cloud Agent](https://github.com/grafana/agent) is running and enabled at boot.

    loki_user: <username>

Each service in [Grafana Cloud](https://grafana.com/products/cloud/) has a unique service id or user. Once in the [Grafana Cloud Portal](https://grafana.com/docs/grafana-cloud/cloud-portal/) click on Loki to get the value you need to provide for `loki_user`. If this value is present, this role will install the [Promtail](https://grafana.com/docs/loki/latest/clients/promtail/) agent and create a Systemd service for it. It will scrape messages from `/var/log` and `journald`. For reference, see [Journal Scraping](https://grafana.com/docs/loki/latest/clients/promtail/scraping/#journal-scraping-linux-only).

    install_unzip: true

Whether to install `unzip`, to extract files from agent's zip releases. By default is set to `true`.

    grafana_location_prometheus: us-central1
    grafana_location_promtail: us-central1

The closest Grafana region for promtail or prometheus. As displayed in `@logs-prod-us-central1.grafana.net/api/prom/push` for example. By default is `us-central1`

To override the agent configuration template, you can define your own template. By default it'll source it from the role file `templates/agent-config.yaml.j2`. 

    grafana_agent_config_template: agent-config.yaml.j2

The grafana agent systemd service template can be set using the following variable:

    grafana_agent_systemd_template: grafana-agent.service.j2

To override the promtail configuration template, you can define your own template. By default it'll source it from the role file `templates/promtail-config.yaml.j2`. 

    grafana_promtail_config_template: promtail-config.yaml.j2

The promtail systemd service template can be set using the following variable:

    grafana_promtail_systemd_template: promtail.service.j2

## Dependencies

None.

## Example Playbook

    - hosts: server
      roles:
        - { role: nleiva.grafana_agent }

See an example playbook I run for my home-lab [here](https://github.com/nleiva/ansible-home/blob/main/grafana-cloud.yml).

## License

GPL-3.0 License

## Author Information

This role was created in 2021 by [Nicolas Leiva](https://github.com/nleiva).
