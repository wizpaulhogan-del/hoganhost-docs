---
title: Getting Started
---

# Getting Started with HoganHost Cloud API

The HoganHost Cloud API allows you to programmatically manage cloud servers.  
All requests must be authenticated with your **API Key**.

Example request:

```bash
POST "https://cloud.hoganhost.com/api/v1/servers"   -H "Authorization: Bearer YOUR_API_KEY"   -H "Content-Type: application/json"   -d '{
        "name": "myserver",
        "plan": "s-1vcpu-1gb",
        "region": "nyc1",
        "image": "ubuntu-22-04-x64"
      }'
```

### Parameters

- **name** – The hostname for your server.  
- **plan** – The slug of the plan you want (see [Plans](./plans.md)).  
- **region** – The datacenter region slug (see [Regions](./regions.md)).  
- **image** – The OS image slug (see [Images](./images.md)).  
