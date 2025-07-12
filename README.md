# ProxySQL Master-Slave MySQL Cluster

This repository provides a ready-to-use Docker Compose setup for a MySQL master-slave replication cluster managed by ProxySQL. It is ideal for testing, development, and learning about MySQL replication and ProxySQL load balancing.

## Project Structure

- `master/`: MySQL master configuration and initialization.
- `slave/`: MySQL slave configurations and initialization.
- `proxysql/`: ProxySQL configuration and persistent data files.
- `docker-compose.yml`: Service definitions for master, slaves, and ProxySQL.

## Services

1. **mysql-master**: MySQL master node (port 3306)
2. **mysql-slave1**: MySQL slave node 1 (port 3307)
3. **mysql-slave2**: MySQL slave node 2 (port 3308)
4. **proxysql**: ProxySQL instance (ports 6032 for admin, 6033 for MySQL traffic)

## How to Run

1. **Install Docker and Docker Compose**
   - Make sure Docker is running on your system.

2. **Clone this repository**
   ```bash
   git clone https://github.com/sakibbuddy/proxysql_master_slave.git
   cd proxysql_master_slave
   ```

3. **Start the cluster**
   ```bash
   docker-compose up -d
   ```

4. **Check service status**
   ```bash
   docker-compose ps
   ```

5. **Access MySQL and ProxySQL**
   - MySQL Master: `localhost:3306`
   - MySQL Slave1: `localhost:3307`
   - MySQL Slave2: `localhost:3308`
   - ProxySQL Admin: `localhost:6032`
   - ProxySQL MySQL: `localhost:6033`

## Notes

- Default MySQL root password is `password` (change in `docker-compose.yml` for production).
- Initialization SQL and custom configs are loaded from the respective folders.
- ProxySQL configuration is in `proxysql/proxysql.cnf`.

## Stopping the Cluster

To stop and remove all containers:
```bash
docker-compose down
```
## Troubleshooting

| Problem                                 | Possible Fix                                                 |
| --------------------------------------- | ------------------------------------------------------------ |
| ❌ Replication lag or slaves not syncing | Check GTID settings and slave status (`SHOW SLAVE STATUS\G`) |
| ❌ ProxySQL health check fails           | Confirm `monitor` user credentials and hostgroups            |
| ❌ Can't connect to master/slave         | Verify container ports, firewall, and network                |
| 🐳 Containers restart / crash           | Inspect logs & check volume mounts                           |
| ❗ ProxySQL not routing reads            | Confirm query rules and hostgroup IDs                        |


---
Feel free to modify configs for your own replication or ProxySQL experiments!