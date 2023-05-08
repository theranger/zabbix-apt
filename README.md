Zabbix template for monitoring APT package updates.

This template uses `-s` simulation option when invoking `apt-get`, so no root access is needed for Zabbix user during polling.

# Notes
However, root access is required for updating APT repositories. Since Zabbix runs under a dedicated user, it can be done either by using `sudo` in agent configuration script below, using a dedicated `crontab` entry to invoke `apt-get update` periodically or use `APT::Periodic` functionality bundled inside the APT system itself. Support for the `APT::Periodic` is included in this setup.

Since `APT::Periodic` is executed via already existing APT maintenace script located in `cron.daily`, the minimum period of updating  repositories is once a day. If shorter period is required, a spearate `cron.hourly` script is needed instead.


# Installation
1. Copy `apt.conf.d/02periodic` script to `/etc/apt/apt.conf.d` directory to configure daily automatic package repository updates using `APT::Periodic`.
2. Copy `zabbix_agentd.d/apt.conf` to the Zabbix agent's configuration directory (usually located in `/etc/zabbix`).
3. Import `templates/apt-updates.xml` to Zabbix frontend.
4. Change "Timeout" value to something higher in the zabbix agent configuration
