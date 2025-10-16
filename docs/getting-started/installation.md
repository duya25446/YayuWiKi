# 安装指南

本指南将帮助您快速安装和配置产品。

## 系统要求

在开始之前，请确保您的系统满足以下要求：

- **操作系统**: Linux, macOS, Windows
- **Python**: 3.8 或更高版本
- **内存**: 最低 2GB RAM
- **磁盘空间**: 500MB 可用空间

## 安装步骤

### 1. 下载安装包

=== "使用 pip"

    ```bash
    pip install yayu-product
    ```

=== "从源码安装"

    ```bash
    git clone https://github.com/yourcompany/yayu-product.git
    cd yayu-product
    pip install -e .
    ```

=== "使用 Docker"

    ```bash
    docker pull yourcompany/yayu-product:latest
    docker run -d -p 8080:8080 yourcompany/yayu-product:latest
    ```

### 2. 配置环境

创建配置文件 `config.yaml`：

```yaml
# 基础配置
server:
  host: 0.0.0.0
  port: 8080
  
# 数据库配置
database:
  type: postgresql
  host: localhost
  port: 5432
  name: yayu_db
  
# 日志配置
logging:
  level: INFO
  file: /var/log/yayu/app.log
```

### 3. 初始化数据库

```bash
yayu-cli db init
yayu-cli db migrate
```

### 4. 启动服务

```bash
yayu-cli start
```

## 验证安装

访问 `http://localhost:8080` 验证服务是否正常运行。

您应该看到欢迎页面：

```json
{
  "status": "success",
  "message": "YaYu Product is running",
  "version": "1.0.0"
}
```

## 常见问题

!!! question "端口被占用怎么办？"
    您可以在配置文件中修改端口号，或使用以下命令指定端口：
    ```bash
    yayu-cli start --port 8888
    ```

!!! question "数据库连接失败？"
    请检查：
    - 数据库服务是否运行
    - 配置文件中的连接信息是否正确
    - 网络防火墙设置

## 下一步

- 查看 [产品概述](../products/overview.md) 了解核心功能
- 阅读 [API 参考](../api/reference.md) 开始集成开发

