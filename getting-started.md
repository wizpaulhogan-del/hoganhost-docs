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

### Example Request (PHP) 
```php 
<?php
$apiKey = "YOUR_API_KEY";
$url = "https://api.hoganhost.com.ng/v1/servers.php";
    
$data = [
    "name"   => "my-server",
    "region" => "nyc3",
    "size"   => "s-1vcpu-1gb",
    "image"  => "ubuntu-22-04-x64"
];

$ch = curl_init($url);   
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    "Authorization: Bearer $apiKey",
    "Content-Type: application/json"
]);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
  
$response = curl_exec($ch);
curl_close($ch);

echo $response;
?>
```
### Example Response
```json
{  
  "id": "12345",
  "name": "my-server",
  "region": "nyc3",
  "size": "s-1vcpu-1gb",
  "image": "ubuntu-22-04-x64",
  "ip_address": "203.0.113.10",
  "status": "provisioning"
}
```

---

## Get Server Information

Retrieve details about an existing server, including IP, region, size, and current status.

```bash
curl -X GET "https://api.hoganhost.com.ng/v1/servers.php?id=SERVER_ID" -H "Authorization: Bearer YOUR_API_KEY"
```

- Replace `SERVER_ID` with the ID returned when the server was created.  
- The response will include resource usage, image type, and power state.  

### Example Request (PHP)
```php
<?php
$apiKey = "YOUR_API_KEY";
$serverId = "SERVER_ID";
$url = "https://api.hoganhost.com.ng/v1/servers.php?id=$serverId";

$ch = curl_init($url);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
    "Authorization: Bearer $apiKey"
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($ch);
curl_close($ch);

echo $response;
?>

### Example Response
```json
{
  "id": "12345",
  "name": "my-server",
  "region": "nyc3",
  "size": "s-1vcpu-1gb",
  "image": "ubuntu-22-04-x64",
  "ip_address": "203.0.113.10",
  "status": "active",
  "power_state": "on",
  "created_at": "2025-09-29T10:00:00Z"
}
```


---

## Server Actions

Perform lifecycle operations on a server.  
These actions let you power on/off, reboot, or shut down a server without deleting it.

### Power On
Starts a stopped server.

```bash
curl -X POST "https://api.hoganhost.com.ng/v1/servers.php?id=SERVER_ID&action=actions" -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: application/json" -d '{"type":"power_on"}'
```
### Example Request (PHP)
```php
<?php
$apiKey = "YOUR_API_KEY";
$serverId = "SERVER_ID";
$url = "https://api.hoganhost.com.ng/v1/servers.php?id=$serverId&action=actions";

$data = ["type" => "power_on"];

$ch = curl_init($url);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer $apiKey",
  "Content-Type: application/json"
]);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($ch);
curl_close($ch);

echo $response;



### Power Off
Forcefully powers down the server. Use this if shutdown does not work.

```bash
curl -X POST "https://api.hoganhost.com.ng/v1/servers.php?id=SERVER_ID&action=actions" -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: application/json" -d '{"type":"power_off"}'
```
### Example Request (PHP)
```php
<?php
$apiKey = "YOUR_API_KEY";
$serverId = "SERVER_ID";
$url = "https://api.hoganhost.com.ng/v1/servers.php?id=$serverId&action=actions";

$data = ["type" => "power_off"];

$ch = curl_init($url);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer $apiKey",
  "Content-Type: application/json"
]);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($ch);
curl_close($ch);

echo $response;



### Shutdown
Attempts a graceful shutdown from inside the OS. Safer than `power_off`.

```bash
curl -X POST "https://api.hoganhost.com.ng/v1/servers.php?id=SERVER_ID&action=actions" -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: application/json" -d '{"type":"shutdown"}'
```

### Example Request (PHP)
```php
<?php
$apiKey = "YOUR_API_KEY";
$serverId = "SERVER_ID";
$url = "https://api.hoganhost.com.ng/v1/servers.php?id=$serverId&action=actions";

$data = ["type" => "shutdown"];

$ch = curl_init($url);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer $apiKey",
  "Content-Type: application/json"
]);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($ch);
curl_close($ch);

echo $response;



### Reboot
Restarts the server (like pressing the reset button).

```bash
curl -X POST "https://api.hoganhost.com.ng/v1/servers.php?id=SERVER_ID&action=actions" -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: application/json" -d '{"type":"reboot"}'
```
### Example Request (PHP)
```php
<?php
$apiKey = "YOUR_API_KEY";
$serverId = "SERVER_ID";
$url = "https://api.hoganhost.com.ng/v1/servers.php?id=$serverId&action=actions";

$data = ["type" => "reboot"];

$ch = curl_init($url);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer $apiKey",
  "Content-Type: application/json"
]);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($ch);
curl_close($ch);

echo $response;



---

## Delete a Server

Permanently remove a server and all its data.

```bash
curl -X DELETE "https://api.hoganhost.com.ng/v1/servers.php?id=SERVER_ID" -H "Authorization: Bearer YOUR_API_KEY"
```
### Example Request (PHP)
```php
<?php
$apiKey = "YOUR_API_KEY";
$serverId = "SERVER_ID";
$url = "https://api.hoganhost.com.ng/v1/servers.php?id=$serverId";

$ch = curl_init($url);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "DELETE");
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  "Authorization: Bearer $apiKey"
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($ch);
curl_close($ch);

echo $response;


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
