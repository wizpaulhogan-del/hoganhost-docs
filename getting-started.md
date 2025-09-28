# Getting Started with HoganHost Cloud API

Welcome to the **HoganHost Cloud API**. This guide will help you authenticate, create, manage, and delete your cloud servers programmatically.

All API requests require a **Bearer Token** for authentication.

---

## Authentication

Every request must include your **API Key** in the `Authorization` header:

```bash
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
Base URL: https://api.hoganhost.com.ng/v1/
```

- Replace `YOUR_API_KEY` with the key generated in your HoganHost account.  
- Without this token, requests will be rejected with an `Unauthorized` error.  

---

## Create a Server

Use this endpoint to **provision a new server**. Specify the region, size, and image you want.

```bash
curl -X POST "https://api.hoganhost.com.ng/v1/servers.php" -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: application/json" -d '{
    "name": "my-server",
    "region": "nyc3",
    "size": "s-1vcpu-1gb",
    "image": "ubuntu-22-04-x64"
}'
```

**Response:** Returns JSON with the server ID, IP address, and initial status.  

---

## Get Server Information

Retrieve details about an existing server, including IP, region, size, and current status.

```bash
curl -X GET "https://api.hoganhost.com.ng/v1/servers.php?id=SERVER_ID" -H "Authorization: Bearer YOUR_API_KEY"
```

- Replace `SERVER_ID` with the ID returned when the server was created.  
- The response will include resource usage, image type, and power state.  

---

## Server Actions

Perform lifecycle operations on a server.  
These actions let you power on/off, reboot, or shut down a server without deleting it.

### Power On
Starts a stopped server.

```bash
curl -X POST "https://api.hoganhost.com.ng/v1/servers.php?id=SERVER_ID&action=actions" -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: application/json" -d '{"type":"power_on"}'
```

### Power Off
Forcefully powers down the server. Use this if shutdown does not work.

```bash
curl -X POST "https://api.hoganhost.com.ng/v1/servers.php?id=SERVER_ID&action=actions" -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: application/json" -d '{"type":"power_off"}'
```

### Shutdown
Attempts a graceful shutdown from inside the OS. Safer than `power_off`.

```bash
curl -X POST "https://api.hoganhost.com.ng/v1/servers.php?id=SERVER_ID&action=actions" -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: application/json" -d '{"type":"shutdown"}'
```

### Reboot
Restarts the server (like pressing the reset button).

```bash
curl -X POST "https://api.hoganhost.com.ng/v1/servers.php?id=SERVER_ID&action=actions" -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: application/json" -d '{"type":"reboot"}'
```

---

## Delete a Server

Permanently remove a server and all its data.

```bash
curl -X DELETE "https://api.hoganhost.com.ng/v1/servers.php?id=SERVER_ID" -H "Authorization: Bearer YOUR_API_KEY"
```

⚠️ **Warning**: This action is irreversible. The server and its data cannot be recovered once deleted.  

---

## Best Practices

- Always **shut down** gracefully before running `power_off` or `delete`.  
- Use `reboot` for planned updates, not for recovery from major failures.  
- Keep track of `SERVER_ID` values returned when creating servers.  

---

## Next Steps
- Browse the [API Reference](/api-reference/introduction) for advanced endpoints.  
- Automate deployments using your favorite tools (Terraform, Ansible, CI/CD).  
- Integrate HoganHost Cloud into your apps for full infrastructure control.
