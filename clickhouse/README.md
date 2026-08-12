# ClickHouse Docker Compose

这个 Docker Compose 配置提供了一个 ClickHouse **26.3 LTS** 开发环境，适合与 TablePlus、DBeaver 等本地数据库客户端配合使用。

## 版本说明

- 镜像: `clickhouse/clickhouse-server:26.3`（2026 年 3 月发布的 LTS 版本）
- LTS 规则：ClickHouse 每年 3 月和 8 月发布的版本是长期支持版（如 25.3、25.8、26.3）
- 升级版本时，把 `docker-compose.yml` 里的镜像标签改成新版本号即可

## 快速开始

### 1. 启动服务

```bash
docker-compose up -d
```

### 2. 验证是否启动成功

```bash
docker-compose ps
```

看到状态为 `healthy` 就说明准备好了。

### 3. 进入客户端

```bash
docker exec -it clickhouse clickhouse-client -u admin --password admin
```

进去后看到 `mydb :)` 提示符就可以敲 SQL 了，比如 `SELECT version();`

## 连接信息

| 项目 | 值 |
|------|-----|
| 主机 | `localhost` |
| HTTP 端口 | `8123`（连接工具大多用这个） |
| 原生端口 | `9000` |
| 数据库 | `mydb` |
| 用户名 | `admin` |
| 密码 | `admin` |

## 环境变量配置

默认密码是 `admin`，**建议改掉**。复制示例文件并修改：

```bash
cp env.example .env
```

然后编辑 `.env`：

```env
CLICKHOUSE_DB=mydb
CLICKHOUSE_USER=admin
CLICKHOUSE_PASSWORD=改成你的密码
```

改完重启生效：

```bash
docker-compose up -d
```

## 数据持久化

- 数据目录: `~/docker-volumes/clickhouse-data`
- 日志目录: `~/docker-volumes/clickhouse-logs`

删掉容器数据不会丢，重新 `up -d` 就回来了。

## 常用命令

```bash
# 启动服务
docker-compose up -d

# 查看日志
docker-compose logs -f

# 停止服务（数据保留）
docker-compose down

# 完全清理（连同数据卷一起删，慎用）
docker-compose down -v

# 进入 ClickHouse 容器
docker exec -it clickhouse clickhouse-client -u admin --password admin
```

## 用 HTTP 接口测试（浏览器访问）

浏览器打开 `http://localhost:8123/`，用户名填 `admin`，密码填你设置的密码，能返回版本信息就说明一切正常。