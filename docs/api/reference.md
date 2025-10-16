# API 参考文档

本文档提供完整的 REST API 接口说明。

## 基础信息

### 接口地址

```
生产环境: https://api.yourcompany.com/v1
测试环境: https://api-test.yourcompany.com/v1
```

### 认证方式

所有 API 请求需要在请求头中包含认证令牌：

```http
Authorization: Bearer YOUR_ACCESS_TOKEN
```

### 响应格式

所有响应均为 JSON 格式：

```json
{
  "code": 200,
  "message": "success",
  "data": {},
  "timestamp": 1234567890
}
```

## 用户管理 API

### 获取用户列表

获取所有用户信息。

**请求**

```http
GET /api/users
```

**查询参数**

| 参数 | 类型 | 必填 | 说明 |
|-----|------|-----|------|
| page | integer | 否 | 页码，默认 1 |
| size | integer | 否 | 每页数量，默认 20 |
| keyword | string | 否 | 搜索关键词 |

**响应示例**

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

**代码示例**

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

### 创建用户

创建新用户。

**请求**

```http
POST /api/users
```

**请求体**

```json
{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "secure_password",
  "role": "user"
}
```

**响应示例**

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

### 获取用户详情

获取指定用户的详细信息。

**请求**

```http
GET /api/users/{user_id}
```

**路径参数**

| 参数 | 类型 | 说明 |
|-----|------|------|
| user_id | integer | 用户 ID |

**响应示例**

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

### 更新用户

更新用户信息。

**请求**

```http
PUT /api/users/{user_id}
```

**请求体**

```json
{
  "email": "newemail@example.com",
  "profile": {
    "bio": "Senior Software Developer"
  }
}
```

### 删除用户

删除指定用户。

**请求**

```http
DELETE /api/users/{user_id}
```

**响应示例**

```json
{
  "code": 200,
  "message": "User deleted successfully"
}
```

## 数据管理 API

### 获取数据列表

**请求**

```http
GET /api/data
```

**查询参数**

| 参数 | 类型 | 必填 | 说明 |
|-----|------|-----|------|
| category | string | 否 | 数据分类 |
| start_date | string | 否 | 开始日期 (YYYY-MM-DD) |
| end_date | string | 否 | 结束日期 (YYYY-MM-DD) |

**代码示例**

```python
import requests
from datetime import datetime, timedelta

# 获取最近7天的数据
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

### 创建数据记录

**请求**

```http
POST /api/data
```

**请求体**

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

### 实时数据订阅

连接到 WebSocket 服务器以接收实时数据更新。

**连接地址**

```
wss://api.yourcompany.com/ws
```

**连接示例**

```javascript
const ws = new WebSocket('wss://api.yourcompany.com/ws');

// 连接建立
ws.onopen = () => {
    console.log('Connected to WebSocket');
    
    // 订阅特定频道
    ws.send(JSON.stringify({
        action: 'subscribe',
        channel: 'data_updates',
        token: 'YOUR_ACCESS_TOKEN'
    }));
};

// 接收消息
ws.onmessage = (event) => {
    const data = JSON.parse(event.data);
    console.log('Received:', data);
};

// 连接关闭
ws.onclose = () => {
    console.log('Disconnected from WebSocket');
};
```

## 错误代码

| 代码 | 说明 |
|-----|------|
| 200 | 请求成功 |
| 201 | 创建成功 |
| 400 | 请求参数错误 |
| 401 | 未授权 |
| 403 | 禁止访问 |
| 404 | 资源不存在 |
| 429 | 请求过于频繁 |
| 500 | 服务器内部错误 |

**错误响应示例**

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

## 速率限制

API 请求受到以下速率限制：

- **标准用户**: 100 请求/分钟
- **高级用户**: 1000 请求/分钟
- **企业用户**: 10000 请求/分钟

超过限制将返回 `429 Too Many Requests` 错误。

## SDK 支持

我们提供多种语言的 SDK：

- [Python SDK](https://github.com/yourcompany/python-sdk)
- [JavaScript SDK](https://github.com/yourcompany/js-sdk)
- [Java SDK](https://github.com/yourcompany/java-sdk)
- [Go SDK](https://github.com/yourcompany/go-sdk)

## 相关链接

- [快速开始](../getting-started/installation.md)
- [产品概述](../products/overview.md)

