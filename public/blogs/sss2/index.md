# Komari 轻量级的自托管服务器监控工具

## 📖 产品介绍
Komari 是一款轻量级的自托管服务器监控工具，旨在提供简单、高效的服务器性能监控解决方案。  
它支持通过 Web 界面查看服务器状态，并通过轻量级 Agent 收集数据。

---

## ✨ 主要功能
- **轻量高效**：低资源占用，适合各种规模的服务器  
- **自托管**：完全掌控数据隐私，部署简单  
- **Web 界面**：直观的监控仪表盘，易于使用  

---

## 🚀 使用 docker-compose 部署

### 步骤 1：创建 `docker-compose.yml` 文件
在你的项目目录下新建一个 `docker-compose.yml` 文件，内容如下：

```yaml
version: '3.8'
services:
  komari:
    image: ghcr.io/komari-monitor/komari:latest
    container_name: komari
    ports:
      - "25774:25774"
    volumes:
      - ./data:/app/data
    environment:
      # 可选：自定义初始管理员账号
      # ADMIN_USERNAME: admin
      # ADMIN_PASSWORD: yourpassword
    restart: unless-stopped

步骤 2：启动服务
bash
docker-compose up -d
这会自动拉取镜像并启动 Komari。

步骤 3：查看日志获取默认账号
bash
docker-compose logs komari
找到类似以下信息：

Code
Default admin account created. Username: ..., Password: ...
🔧 常用命令
停止服务

bash
docker-compose down
重启服务

bash
docker-compose restart
查看容器状态

bash
docker-compose ps
📂 数据持久化说明
./data 文件夹用于持久化数据，建议定期备份

可以通过修改 environment 字段自定义管理员账号和密码

其他参数可参考 Komari 镜像的 --help