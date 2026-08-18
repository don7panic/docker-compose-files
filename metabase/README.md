# Metabase Docker Compose

本配置用于本地验证 Metabase 读取已有的 ClickHouse 人才盘点 PoC 数据。

- Metabase: <http://localhost:3000>
- ClickHouse 容器: `clickhouse`
- ClickHouse 网络: `clickhouse_local-services`
- ClickHouse 数据库: `talent_inventory`

## 启动

```bash
cd /Users/oasis/workspace/docker-compose-files/metabase
docker compose up -d
```

首次启动需要下载镜像并初始化，等待健康检查通过：

```bash
docker compose ps
docker compose logs -f metabase
```

访问 <http://localhost:3000> 完成 Metabase 初始设置。

## 连接 ClickHouse

因为 Metabase 和 ClickHouse 在同一个 Docker 网络中，添加数据源时填写：

| 字段 | 值 |
|---|---|
| Database type | ClickHouse |
| Display name | 人才盘点 PoC |
| Host | `clickhouse` |
| Port | `8123` |
| Username | `admin` |
| Password | 使用 ClickHouse 的实际密码 |
| Databases | `talent_inventory` |

> 不要填 `localhost`：这会指向 Metabase 容器本身，而不是 ClickHouse。

添加完成后，在 Metabase 的 **Admin settings → Databases** 对该数据源执行一次 **Sync database schema**。

## 停止与重置

```bash
# 停止服务，保留 Metabase 的配置和看板
docker compose down

# 重置 Metabase 本身的配置、用户、问题和看板（不会删除 ClickHouse 数据）
docker compose down
rm -rf ~/docker-volumes/metabase-data
```

## 数据持久化

Metabase 的内嵌 H2 应用数据库存放在：

```text
~/docker-volumes/metabase-data
```

它保存管理员账号、数据源连接设置、原生 SQL 查询、看板及收藏等元数据。仅用于本地 PoC；生产环境应改用独立 PostgreSQL 作为 Metabase 应用数据库。
