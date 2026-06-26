# Synology Hyper Backup Template for Zabbix

Monitor **Synology Hyper Backup** jobs using the Synology DSM Web API with a **pure Zabbix JavaScript implementation**. No external scripts or agents are required.

## Overview

This template automatically discovers Hyper Backup tasks and monitors their status, execution state, scheduling, and last backup result.

It is designed to provide simple and reliable monitoring of Synology backup jobs directly from Zabbix.

## Features

* Hyper Backup task auto-discovery (LLD)
* Monitor all backup jobs
* Current task activity
* Task state monitoring
* Last backup result
* Last execution time
* Next scheduled execution
* Built-in triggers for backup failures and unexpected task states
* Native Zabbix JavaScript implementation (no external dependencies)

## Compatibility

Tested with:

* Synology DSM 6.2
* Synology DSM 7.x
* Zabbix 6.x
* Zabbix 7.x (recommended)

## Installation

1. Import `template_synology_hyperbackup.yaml` into Zabbix.
2. Link the template to your Synology host.
3. Configure the required macros:

| Macro                             | Description                            |
| --------------------------------- | -------------------------------------- |
| `{$SYNO.REST.USER}`               | DSM user with Hyper Backup permissions |
| `{$SYNO.REST.PASSWORD}`           | DSM password                           |
| `{$SYNO.REST.API.PORT}`           | DSM HTTPS port (default: `5001`)       |
| `{$SYNO.REST.API.BACKUP.LLD_INT}` | Discovery interval (default: `15m`)    |

### DSM Permissions

The configured DSM account must have permission to manage Hyper Backup.

Recommended:

* **Delegate → Hyper Backup Management**

If the **Delegate** menu is unavailable, the account must belong to the **administrators** group.

## Monitored Items

The template collects the following information for every Hyper Backup task:

* Current activity
* Task state
* Last backup result
* Last execution time
* Next scheduled execution

## Discovery

Low-Level Discovery (LLD) automatically detects every Hyper Backup task configured on the NAS.

No manual configuration is required when new backup jobs are created.

## Triggers

The template includes built-in alerts for:

* Backup task failures
* Unexpected task states
* Missing schedules
* Running backup information

## Credits

This project is based on the excellent work of **lestoilfante**:

https://github.com/lestoilfante @ https://www.itsbalto.com/en/posts/synology-hyper-backup-under-control-with-zabbix/

The original template has been updated and improved with additional compatibility fixes, enhancements, and maintenance for newer Zabbix and DSM versions.

## Contributing

Contributions, bug reports, and improvements are welcome.

Feel free to open an Issue or submit a Pull Request.

## License

This project remains distributed under the **GNU General Public License v3.0 (GPLv3)**, following the original work.
