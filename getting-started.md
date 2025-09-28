# Getting Started with HoganHost Cloud API

Welcome to the **HoganHost Cloud API**!  
With this API, you can programmatically create, manage, and delete cloud servers directly from your applications.

---

## Authentication

All API requests require authentication with a **Bearer Token**.  
You can generate your API key from the HoganHost Client Area under **API Management**.

### Example Headers
```bash
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
Base URL: https://api.hoganhost.com.ng/v1/
```

---

## Create a Server

Use this endpoint to create a new cloud server.

```bash
curl -X POST "https://api.hoganhost.com.ng/v1/servers.php" -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: application/json" -d '{
    "name": "test-vps",
    "region": "nyc3",
    "size": "s-1vcpu-1gb",
    "image": "ubuntu-22-04-x64",
    "user_id": 1
}'
```

**Parameters:**
- `name`: The server name  
- `region`: Location (`nyc3`, `lon1`, etc.)  
- `size`: Server size (`s-1vcpu-1gb`, etc.)  
- `image`: Operating system image  
- `user_id`: Your HoganHost account user ID

---

## Get Server Info

Retrieve details of a specific server by its ID.

```bash
curl -X GET "https://api.hoganhost.com.ng/v1/servers.php?id=SERVER_ID" -H "Authorization: Bearer YOUR_API_KEY"
```

Replace `SERVER_ID` with your actual server ID.

---

## Server Actions

Perform power and management actions on your server.

```bash
curl -X POST "https://api.hoganhost.com.ng/v1/servers.php?id=SERVER_ID&action=actions" -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: application/json" -d '{"type":"power_off"}'
```

**Available Actions:**
- `power_on`
- `power_off`
- `reboot`
- `shutdown`

---

## Delete a Server

Permanently delete a server. This action cannot be undone.

```bash
curl -X DELETE "https://api.hoganhost.com.ng/v1/servers.php?id=SERVER_ID" -H "Authorization: Bearer YOUR_API_KEY"
```

---

## Best Practices

- Keep your API keys secret and never expose them in public code.  
- Use **test keys** for development and **live keys** for production.  
- Automate and test requests with tools like **Postman** or **Insomnia**.  
