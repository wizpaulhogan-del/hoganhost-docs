---
title: Power Actions
---

# Server Actions

You can manage the lifecycle of your servers via the API.

### Power On

```bash
POST "https://cloud.hoganhost.com/api/v1/servers/{id}/actions"   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{"type":"power_on"}'
```

### Power Off

```bash
POST "https://cloud.hoganhost.com/api/v1/servers/{id}/actions"   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{"type":"power_off"}'
```

### Reboot

```bash
POST "https://cloud.hoganhost.com/api/v1/servers/{id}/actions"   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{"type":"reboot"}'
```

### Shutdown

```bash
POST "https://cloud.hoganhost.com/api/v1/servers/{id}/actions"   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{"type":"shutdown"}'
```

### Delete

```bash
DELETE "https://cloud.hoganhost.com/api/v1/servers/{id}"   -H "Authorization: Bearer YOUR_API_KEY"
```
