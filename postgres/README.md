# PostgreSQL Docker Compose

这个 Docker Compose 配置提供了一个 PostgreSQL 16 开发环境，适合与 TablePlus 等本地数据库客户端配合使用。

## 服务包含

- **PostgreSQL 16**: 主数据库服务

## 快速开始

### 1. 启动服务

```bash
docker-compose up -d
```

### 2. 访问服务

- **PostgreSQL 数据库**:
  - 主机: `localhost`
  - 端口: `5432`
  - 数据库: `mydb`
  - 用户名: `admin`
  - 密码: `admin`

### 3. 环境变量配置

复制环境变量示例文件并自定义配置：

```bash
cp env.example .env
```

或者直接创建 `.env` 文件：

```env
POSTGRES_DB=mydb
POSTGRES_USER=admin
POSTGRES_PASSWORD=admin
```

## 数据持久化

- PostgreSQL 数据存储在: `~/docker-volumes/postgres-data`
- 初始化脚本目录: `./init-scripts`

## 初始化脚本

在 `init-scripts` 目录中放置 `.sql` 或 `.sh` 文件，这些文件会在数据库首次启动时自动执行。

## 性能优化

配置包含了针对开发环境的 PostgreSQL 性能优化参数：
- 最大连接数: 200
- 共享缓冲区: 256MB
- 有效缓存大小: 1GB

## 常用命令

```bash
# 启动服务
docker-compose up -d

# 查看日志
docker-compose logs -f

# 停止服务
docker-compose down

# 完全清理（包括数据卷）
docker-compose down -v

# 进入 PostgreSQL 容器
docker exec -it postgres16 psql -U admin -d mydb
```

## 使用 TablePlus 连接数据库

在 TablePlus 中创建新连接：
- **类型**: PostgreSQL
- **主机**: localhost
- **端口**: 5432
- **数据库**: mydb
- **用户名**: admin
- **密码**: admin

或者使用连接 URL：
```
postgresql://admin:admin@localhost:5432/mydb
```
