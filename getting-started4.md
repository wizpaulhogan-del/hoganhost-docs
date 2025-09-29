# Getting Started

Welcome to the **HoganHost Cloud API**.
This guide will help you authenticate, create, manage, and delete servers using our API.
All requests are made over **HTTPS** and require authentication with your API key.

---

## Authentication

Every request must include your API key in the `Authorization` header:

```bash
curl -X GET "https://cloud.hoganhost.com/api/v1/servers"   -H "Authorization: Bearer YOUR_API_KEY"
```

---

## Available Plans

When creating a server, you must specify a **plan slug**.
Below are the supported slugs.

| Slug                      | Description                                     |
| ------------------------- | ----------------------------------------------- |
| `s-1vcpu-1gb`             | Standard: 1 vCPU, 1 GB RAM                      |
| `s-1vcpu-2gb`             | Standard: 1 vCPU, 2 GB RAM                      |
| `s-2vcpu-2gb`             | Standard: 2 vCPU, 2 GB RAM                      |
| `s-2vcpu-4gb`             | Standard: 2 vCPU, 4 GB RAM                      |
| `g-2vcpu-8gb`             | General Purpose: 2 vCPU, 8 GB RAM               |
| `g-4vcpu-16gb`            | General Purpose: 4 vCPU, 16 GB RAM              |
| `g-8vcpu-32gb`            | General Purpose: 8 vCPU, 32 GB RAM              |
| `g-16vcpu-64gb`           | General Purpose: 16 vCPU, 64 GB RAM             |
| `c-2`                     | Compute Optimized: 2 vCPU                       |
| `c-4`                     | Compute Optimized: 4 vCPU                       |
| `c-8`                     | Compute Optimized: 8 vCPU                       |
| `c-16`                    | Compute Optimized: 16 vCPU                      |
| `s-1vcpu-1gb-35gb-intel`  | Standard (Intel): 1 vCPU, 1 GB RAM, 35 GB Disk  |
| `s-1vcpu-2gb-70gb-intel`  | Standard (Intel): 1 vCPU, 2 GB RAM, 70 GB Disk  |
| `s-2vcpu-2gb-90gb-intel`  | Standard (Intel): 2 vCPU, 2 GB RAM, 90 GB Disk  |
| `s-2vcpu-4gb-120gb-intel` | Standard (Intel): 2 vCPU, 4 GB RAM, 120 GB Disk |
| `g-2vcpu-8gb-intel`       | General Purpose (Intel): 2 vCPU, 8 GB RAM       |
| `g-4vcpu-16gb-intel`      | General Purpose (Intel): 4 vCPU, 16 GB RAM      |
| `g-8vcpu-32gb-intel`      | General Purpose (Intel): 8 vCPU, 32 GB RAM      |
| `g-16vcpu-64gb-intel`     | General Purpose (Intel): 16 vCPU, 64 GB RAM     |
| `c-4-intel`               | Compute Optimized (Intel): 4 vCPU               |
| `c-8-intel`               | Compute Optimized (Intel): 8 vCPU               |
| `c-16-intel`              | Compute Optimized (Intel): 16 vCPU              |
| `c-32-intel`              | Compute Optimized (Intel): 32 vCPU              |

---

## Available Locations

Choose a **location slug** when creating a server.
We use the same region slugs as DigitalOcean.

| Slug   | Location        | Country     |
| ------ | --------------- | ----------- |
| `nyc1` | New York 1      | USA         |
| `nyc3` | New York 3      | USA         |
| `sfo2` | San Francisco 2 | USA         |
| `sfo3` | San Francisco 3 | USA         |
| `ams3` | Amsterdam 3     | Netherlands |
| `sgp1` | Singapore 1     | Singapore   |
| `lon1` | London 1        | UK          |
| `fra1` | Frankfurt 1     | Germany     |
| `tor1` | Toronto 1       | Canada      |
| `blr1` | Bangalore 1     | India       |

---

## Endpoints

### Create a Server

```bash
curl -X POST "https://cloud.hoganhost.com/api/v1/servers"   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{
        "name": "myserver",
        "plan": "s-1vcpu-1gb",
        "region": "nyc1",
        "image": "ubuntu-22-04-x64"
      }'
```

---

### List Servers

```bash
curl -X GET "https://cloud.hoganhost.com/api/v1/servers"   -H "Authorization: Bearer YOUR_API_KEY"
```

---

### Get Server Details

```bash
curl -X GET "https://cloud.hoganhost.com/api/v1/servers/{server_id}"   -H "Authorization: Bearer YOUR_API_KEY"
```

---

### Power On

```bash
curl -X POST "https://cloud.hoganhost.com/api/v1/servers/{server_id}/actions"   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{"type": "power_on"}'
```

---

### Power Off

```bash
curl -X POST "https://cloud.hoganhost.com/api/v1/servers/{server_id}/actions"   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{"type": "power_off"}'
```

---

### Shutdown

```bash
curl -X POST "https://cloud.hoganhost.com/api/v1/servers/{server_id}/actions"   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{"type": "shutdown"}'
```

---

### Reboot

```bash
curl -X POST "https://cloud.hoganhost.com/api/v1/servers/{server_id}/actions"   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{"type": "reboot"}'
```

---

### Delete a Server

```bash
curl -X DELETE "https://cloud.hoganhost.com/api/v1/servers/{server_id}"   -H "Authorization: Bearer YOUR_API_KEY"
```

---

## Next Steps

* Explore available images (`ubuntu-22-04-x64`, `debian-12-x64`, `centos-9-x64`, etc.).
* Use our API to automate provisioning, scaling, and lifecycle management of your HoganHost servers.
