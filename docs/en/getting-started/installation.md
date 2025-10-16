# Installation Guide

This guide will help you quickly install and configure the product.

## System Requirements

Before you begin, ensure your system meets the following requirements:

- **Operating System**: Linux, macOS, Windows
- **Python**: 3.8 or higher
- **Memory**: Minimum 2GB RAM
- **Disk Space**: 500MB available space

## Installation Steps

### 1. Download Installation Package

=== "Using pip"

    ```bash
    pip install yayu-product
    ```

=== "Install from Source"

    ```bash
    git clone https://github.com/yourcompany/yayu-product.git
    cd yayu-product
    pip install -e .
    ```

=== "Using Docker"

    ```bash
    docker pull yourcompany/yayu-product:latest
    docker run -d -p 8080:8080 yourcompany/yayu-product:latest
    ```

### 2. Configure Environment

Create configuration file `config.yaml`:

```yaml
# Basic Configuration
server:
  host: 0.0.0.0
  port: 8080
  
# Database Configuration
database:
  type: postgresql
  host: localhost
  port: 5432
  name: yayu_db
  
# Logging Configuration
logging:
  level: INFO
  file: /var/log/yayu/app.log
```

### 3. Initialize Database

```bash
yayu-cli db init
yayu-cli db migrate
```

### 4. Start Service

```bash
yayu-cli start
```

## Verify Installation

Visit `http://localhost:8080` to verify the service is running properly.

You should see the welcome page:

```json
{
  "status": "success",
  "message": "YaYu Product is running",
  "version": "1.0.0"
}
```

## Common Issues

!!! question "What if the port is already in use?"
    You can modify the port number in the configuration file, or specify a port using the following command:
    ```bash
    yayu-cli start --port 8888
    ```

!!! question "Database connection failed?"
    Please check:
    - Is the database service running
    - Is the connection information in the configuration file correct
    - Network firewall settings

## Next Steps

- Check [Product Overview](../products/overview.md) to learn about core features
- Read [API Reference](../api/reference.md) to start integration development

