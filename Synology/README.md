# Synology Cloud Sync Monitoring for Zabbix

A Zabbix template for monitoring Synology Cloud Sync tasks using the native DSM API.

Tested and validated on:

- Synology DSM 7.2.x
- Cloud Sync
- Microsoft Azure Blob Storage
- Zabbix 7.4.x

## Features

### Automatic Discovery

The template automatically discovers all configured Cloud Sync tasks.

No task names are hardcoded.

Example:

```json
[
  {
    "{#TASK_NAME}": "Veeam2Azure",
    "{#TASK_ID}": 1
  }
]
```

This allows the same template to be deployed across multiple Synology NAS devices regardless of task naming conventions.

---

## Monitored Metrics

For each Cloud Sync task, the template collects:

| Metric | Description |
|----------|-------------|
| Status | Current synchronization status |
| Link Status | Connectivity status to cloud provider |
| Cloud Status | Cloud service status |
| Provider Type | Azure, AWS, Google Drive, OneDrive, etc. |
| Tray Status | Global Cloud Sync status |
| Unfinished Files | Number of pending files |
| Exceed Maximum Files | Maximum file count warning |

---

## Example Data

```json
[
  {
    "Name": "Veeam2Azure",
    "Id": 1,
    "Status": "uptodate",
    "Link_Status": 1,
    "Cloud_Status": 0,
    "Unfinished_Files": 0,
    "Exceed_Maximum_Files": 0,
    "Type": "azure_cloud_storage",
    "Tray_Status": "uptodate"
  }
]
```

---

## Recommended Triggers

### Synchronization Failure

Trigger when a task is no longer synchronized.

```text
Status <> "uptodate"
```

Severity: High

---

### Cloud Provider Unreachable

Trigger when connectivity to Azure, AWS, Google Drive or another provider is lost.

```text
Link_Status <> 1
```

Severity: Disaster

---

### Pending Files

Trigger when files remain pending for an extended period.

```text
Unfinished_Files > 0
```

Severity: Warning

---

### Maximum File Limit Reached

Trigger when Cloud Sync reports a maximum file limitation.

```text
Exceed_Maximum_Files = 1
```

Severity: Average

---

## Use Case

This template is particularly useful in backup architectures such as:

```text
Veeam
  ↓
Synology NAS
  ↓
Cloud Sync
  ↓
Microsoft Azure Blob Storage
```

In this scenario, local backups may succeed while off-site replication silently fails.

This template provides visibility into the actual cloud synchronization status.

---

## Installation

1. Import the template into Zabbix.
2. Configure the DSM API credentials.
3. Link the template to your Synology NAS host.
4. Wait for automatic task discovery.

---

## Compatibility

| Component | Version |
|------------|-----------|
| DSM | 7.2.x |
| Cloud Sync | Latest |
| Zabbix | 7.4.x |

---

## Author

Jean-Philip Kerloc'h


---

## License

MIT License
