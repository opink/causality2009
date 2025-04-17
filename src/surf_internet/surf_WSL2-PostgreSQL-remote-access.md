# WSL2中PostgreSQL数据库在Windows主机上的远程访问配置

## 1 在 WSL2 中直接安装 PostgreSQL（非 Docker）并让 Windows 主机访问服务，需解决 **WSL2 网络隔离**和 **PostgreSQL 远程访问配置**问题。以下是完整步骤：
### 1.1.  在 WSL2 中安装 PostgreSQL

安装并启动服务：

```bash
# 更新包列表
sudo apt update

# 安装 PostgreSQL
sudo apt install postgresql postgresql-contrib

# 启动 PostgreSQL 服务
sudo service postgresql start

# 设置开机自启（若需，但 WSL2 默认无 systemd，需手动启动）
# 可选：在 ~/.bashrc 中添加启动命令
echo "sudo service postgresql start" >> ~/.bashrc
```

验证 PostgreSQL 运行状态：

```bash
sudo service postgresql status
```

### 1.2. 配置 PostgreSQL 允许远程连接

修改监听地址：

```bash
# 编辑配置文件（使用 nano 或 vim）
sudo vim /etc/postgresql/*/main/postgresql.conf
```

```ini
listen_addresses = '*'   # 监听所有网络接口
```

配置客户端认证规则：

```bash
sudo vim /etc/postgresql/*/main/pg_hba.conf
```

在文件末尾添加规则（允许所有远程 IPv4/IPv6 连接）：

```ini
# IPv4
host    all             all             0.0.0.0/0               md5

# IPv6
host    all             all             ::/0                    md5
```

重启 PostgreSQL 生效配置：

```bash
sudo service postgresql restart
```

### 1.3.  配置 WSL2 网络
#### 方案 1：通过 `localhost` 直接访问（推荐）
##### **配置 Windows 防火墙**

允许入站连接到 `5432` 端口：

1. 打开 **Windows Defender 防火墙** > **高级设置**。
    
2. 新建入站规则：
    
    - 规则类型：**端口** → **TCP** → 特定端口 `5432`。
        
    - 操作：**允许连接**。
        
    - 配置文件：全选（域、专用、公用）。
        
    - 名称：`PostgreSQL (WSL2)`。

### 1.4. 创建数据库用户和密码

默认 PostgreSQL 用户为 `postgres`（无密码），建议创建新用户：

```bash
# 切换到 postgres 系统用户
sudo -u postgres psql
```

```psql
# 在 PostgreSQL 命令行中执行
CREATE USER myuser WITH PASSWORD 'mypassword';
CREATE DATABASE mydb OWNER myuser;
GRANT ALL PRIVILEGES ON DATABASE mydb TO myuser;

# 退出
\q
```

```bash
# 退回到wsl2主用户
exit

# 查看是否创建成功和用户权限
sudo -u postgres psql -c "\l"
sudo -u postgres psql -c "\du"
```
### 1.5. 从 Windows 连接 PostgreSQL
##### 测试连接：

- **使用 PowerShell 的 `psql`**（需先[安装](https://www.postgresql.org/download/windows/)）：
```powershell 
psql -h localhost -U myuser -d mydb
```

- **使用图形化工具**（如 [pgAdmin](https://www.pgadmin.org/) 或 [DBeaver](https://dbeaver.io/)）：
	- 填写主机、端口、用户名、密码即可。

## 2. wsl2中使用docker安装的postgresql docker镜像(不使用docker desktop)，给本机的windows上的应用提供服务

### 2.1. 在WSL中安装Docker引擎
若不使用Docker Desktop，需手动安装Docker CE：

```bash
# 更新包列表
sudo apt update
# 安装依赖
sudo apt install apt-transport-https ca-certificates curl software-properties-common
# 添加Docker官方GPG密钥
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
# 添加Docker仓库
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
# 安装Docker引擎
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
# 启动Docker服务并设置开机自启
sudo service docker start
sudo systemctl enable docker
# 将当前用户加入docker组（避免每次使用sudo）
sudo usermod -aG docker $USER
# 退出并重新登录WSL使配置生效
```

### 2.2. 运行PostgreSQL容器
使用以下命令启动PostgreSQL容器，并映射端口：

```bash
docker run --name postgres \
  -e POSTGRES_PASSWORD=mypassword \
  -e POSTGRES_USER=myuser \
  -p 0.0.0.0:5432:5432 \
  -d postgres
```

**关键参数说明**：
- `-p 0.0.0.0:5432:5432`：将容器的5432端口绑定到WSL2的所有网络接口，确保可从外部（Windows主机）访问。
    
- 环境变量设置用户名和密码，按需调整。

### 2.3. 配置docker 镜像中的PostgreSQL允许远程连接
1.  **进入容器修改配置**：
```bash
docker exec -it postgres bash
```
2.  **编辑`postgresql.conf`**：
```bash
echo "listen_addresses = '*'" >> /var/lib/postgresql/data/postgresql.conf
```
3. **编辑`pg_hba.conf`**：
```bash
echo "host all all 0.0.0.0/0 md5" >> /var/lib/postgresql/data/pg_hba.conf
```
4. **重启容器**：
```bash
docker restart postgres
```

> 配置Windows防火墙
   允许入站连接到5432端口：同前1.3


### 2.4. 从Windows连接PostgreSQL

使用以下方式查询WSL2的IP地址：

```bash
# 在WSL2中执行：
hostname -I | awk '{print $1}'
```

```powershell
# 或从Windows命令行通过：
wsl hostname -I
```

#### 2.4.1 验证连接

- **主机/IP**：WSL2的IP地址（如`172.21.0.1`）或`localhost`（若WSL版本支持回环）。
    
- **端口**：5432
    
- **用户名/密码**：步骤2中设置的值（如`myuser`/`mysecretpassword`）。