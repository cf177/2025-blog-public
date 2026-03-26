# Sun-Panel
NAS、服务器导航面板、简易 docker 管理器、Homepage、浏览器首页

---

## 📖 默认账号密码
- **账号**：`admin@sun.cc`  
- **密码**：`12345678`

---

## 🚀 Docker Compose 配置
```yaml
version: "3.2"
services:
  sun-panel:
    image: "hslr/sun-panel:latest"
    container_name: sun-panel
    volumes:
      - ./conf:/app/conf
      - /var/run/docker.sock:/var/run/docker.sock
      # - ./runtime:/app/runtime
      # - /mnt/sata1-1:/os
    ports:
      - 3002:3002
    restart: always
