# Sun-Panel 部署完整教程
专为 NAS / 服务器打造的轻量导航面板，支持 Docker 可视化管理、自定义首页，部署简单、稳定好用。

---

## 一、一键部署（直接复制即用）

```bash
mkdir -p sun-panel && cd sun-panel

version: "3.2"
services:
  sun-panel:
    image: hslr/sun-panel:latest
    container_name: sun-panel
    volumes:
      # 核心配置文件持久化（必须挂载）
      - ./conf:/app/conf
      # 允许面板管理宿主机 Docker（必须挂载）
      - /var/run/docker.sock:/var/run/docker.sock
    ports:
      # 主机端口:容器端口，可自行修改 3002 为你想要的端口
      - 3002:3002
    # 开机自启
    restart: always
 ```

# 后台启动容器
```
docker-compose up -d
```

# 查看容器运行状态
```
docker ps
```

# 二、面板访问
# 访问地址
```
http://你的服务器IP:3002
```

# 访问示例
```
http://192.168.1.100:3002
```

# 默认账号密码
```
账号：admin@sun.cc
密码：12345678
```
✅ 安全提示：首次登录务必修改默认密码。
# 三、核心功能
自定义导航：自由添加 NAS、内网服务、网页书签
Docker 可视化：图形化启停、删除、查看容器与日志
浏览器首页：可设置为默认主页，统一管理所有自建服务
数据持久化：配置存放本地 conf 目录，重装、升级数据不丢失
# 四、注意事项 & 常见问题
## 1. 端口被占用
如需更换访问端口，只修改左侧端口：
```
ports:
  - 8080:3002
```
修改后重启服务：
运行
```
docker-compose up -d
```
## 2. 无法管理 Docker
必须保留以下挂载，删除会导致 Docker 管理失效：
```
- /var/run/docker.sock:/var/run/docker.sock
```
## 3. 数据备份与迁移
直接完整备份 sun-panel 整个文件夹，更换设备直接覆盖即可恢复全部配置。
## 4. 面板版本更新
运行
```
docker-compose pull
docker-compose up -d
```
# 五、部署总结
新建 sun-panel 目录并写入编排配置
执行
```
 docker-compose up -d 
```
一键部署
浏览器访问 
```
IP:3002 
```
登录使用
轻量好用，NAS、服务器自建服务必备导航面板