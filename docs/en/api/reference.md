# API Reference

This document provides complete REST API interface documentation.

## Basic Information

### API Endpoints

```
Production: https://api.yourcompany.com/v1
Testing: https://api-test.yourcompany.com/v1
```

### Authentication

All API requests must include an authentication token in the request header:

```http
Authorization: Bearer YOUR_ACCESS_TOKEN
```

### Response Format

All responses are in JSON format:

```json
{
  "code": 200,
  "message": "success",
  "data": {},
  "timestamp": 1234567890
}
```

## User Management API

### Get User List

Retrieve all user information.

**Request**

```http
GET /api/users
```

**Query Parameters**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| page | integer | No | Page number, default 1 |
| size | integer | No | Items per page, default 20 |
| keyword | string | No | Search keyword |

**Response Example**

```json
{
  "code": 200,
  "message": "success",
  "data": {
    "total": 100,
    "page": 1,
    "size": 20,
    "items": [
      {
        "id": 1,
        "username": "john_doe",
        "email": "john@example.com",
        "created_at": "2025-01-01T00:00:00Z"
      }
    ]
  }
}
```

**Code Examples**

=== "Python"

    ```python
    import requests
    
    url = "https://api.yourcompany.com/v1/api/users"
    headers = {
        "Authorization": "Bearer YOUR_ACCESS_TOKEN"
    }
    params = {
        "page": 1,
        "size": 20
    }
    
    response = requests.get(url, headers=headers, params=params)
    data = response.json()
    print(data)
    ```

=== "JavaScript"

    ```javascript
    const url = 'https://api.yourcompany.com/v1/api/users';
    const headers = {
        'Authorization': 'Bearer YOUR_ACCESS_TOKEN'
    };
    
    fetch(url + '?page=1&size=20', { headers })
        .then(response => response.json())
        .then(data => console.log(data));
    ```

=== "cURL"

    ```bash
    curl -X GET "https://api.yourcompany.com/v1/api/users?page=1&size=20" \
         -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
    ```

### Create User

Create a new user.

**Request**

```http
POST /api/users
```

**Request Body**

```json
{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "secure_password",
  "role": "user"
}
```

**Response Example**

```json
{
  "code": 201,
  "message": "User created successfully",
  "data": {
    "id": 1,
    "username": "john_doe",
    "email": "john@example.com",
    "role": "user",
    "created_at": "2025-01-01T00:00:00Z"
  }
}
```

### Get User Details

Retrieve detailed information for a specific user.

**Request**

```http
GET /api/users/{user_id}
```

**Path Parameters**

| Parameter | Type | Description |
|-----------|------|-------------|
| user_id | integer | User ID |

**Response Example**

```json
{
  "code": 200,
  "message": "success",
  "data": {
    "id": 1,
    "username": "john_doe",
    "email": "john@example.com",
    "role": "user",
    "profile": {
      "avatar": "https://example.com/avatar.jpg",
      "bio": "Software Developer"
    },
    "created_at": "2025-01-01T00:00:00Z",
    "updated_at": "2025-01-02T00:00:00Z"
  }
}
```

### Update User

Update user information.

**Request**

```http
PUT /api/users/{user_id}
```

**Request Body**

```json
{
  "email": "newemail@example.com",
  "profile": {
    "bio": "Senior Software Developer"
  }
}
```

### Delete User

Delete a specific user.

**Request**

```http
DELETE /api/users/{user_id}
```

**Response Example**

```json
{
  "code": 200,
  "message": "User deleted successfully"
}
```

## Data Management API

### Get Data List

**Request**

```http
GET /api/data
```

**Query Parameters**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| category | string | No | Data category |
| start_date | string | No | Start date (YYYY-MM-DD) |
| end_date | string | No | End date (YYYY-MM-DD) |

**Code Example**

```python
import requests
from datetime import datetime, timedelta

# Get data from the last 7 days
end_date = datetime.now()
start_date = end_date - timedelta(days=7)

params = {
    "category": "sales",
    "start_date": start_date.strftime("%Y-%m-%d"),
    "end_date": end_date.strftime("%Y-%m-%d")
}

response = requests.get(
    "https://api.yourcompany.com/v1/api/data",
    headers={"Authorization": "Bearer YOUR_ACCESS_TOKEN"},
    params=params
)

data = response.json()
```

### Create Data Record

**Request**

```http
POST /api/data
```

**Request Body**

```json
{
  "category": "sales",
  "value": 1000.50,
  "metadata": {
    "region": "Asia",
    "product": "Product A"
  },
  "timestamp": "2025-01-01T12:00:00Z"
}
```

## WebSocket API

### Real-time Data Subscription

Connect to the WebSocket server to receive real-time data updates.

**Connection URL**

```
wss://api.yourcompany.com/ws
```

**Connection Example**

```javascript
const ws = new WebSocket('wss://api.yourcompany.com/ws');

// Connection established
ws.onopen = () => {
    console.log('Connected to WebSocket');
    
    // Subscribe to specific channel
    ws.send(JSON.stringify({
        action: 'subscribe',
        channel: 'data_updates',
        token: 'YOUR_ACCESS_TOKEN'
    }));
};

// Receive messages
ws.onmessage = (event) => {
    const data = JSON.parse(event.data);
    console.log('Received:', data);
};

// Connection closed
ws.onclose = () => {
    console.log('Disconnected from WebSocket');
};
```

## Error Codes

| Code | Description |
|------|-------------|
| 200 | Request successful |
| 201 | Created successfully |
| 400 | Invalid request parameters |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Resource not found |
| 429 | Too many requests |
| 500 | Internal server error |

**Error Response Example**

```json
{
  "code": 400,
  "message": "Invalid request parameters",
  "errors": [
    {
      "field": "email",
      "message": "Invalid email format"
    }
  ],
  "timestamp": 1234567890
}
```

## Rate Limiting

API requests are subject to the following rate limits:

- **Standard Users**: 100 requests/minute
- **Premium Users**: 1000 requests/minute
- **Enterprise Users**: 10000 requests/minute

Exceeding the limit will return a `429 Too Many Requests` error.

## SDK Support

We provide SDKs in multiple languages:

- [Python SDK](https://github.com/yourcompany/python-sdk)
- [JavaScript SDK](https://github.com/yourcompany/js-sdk)
- [Java SDK](https://github.com/yourcompany/java-sdk)
- [Go SDK](https://github.com/yourcompany/go-sdk)

## Related Links

- [Getting Started](../getting-started/installation.md)
- [Product Overview](../products/overview.md)

