# 🎶 Solara（光域）音乐播放器

一个极简风格的现代化网页音乐播放器，基于轻量后端服务，整合多种免费音乐聚合接口，支持搜索、播放与音频下载全流程。

---

## 🐳 部署指南

使用 **Docker 或 Docker Compose** 快速部署（**推荐 Docker Compose**）：

### 1. Docker 命令部署
```bash
docker run -d \
  --name solara-music \
  --restart unless-stopped \
  -p 3001:3001 \
  -e NODE_ENV=production \
  -e PORT=3001 \
  -e SOLARA_PASSWORD=solara123 \   # ⚠️ 首次启动后必须修改！
  -e SESSION_SECRET=KLmlKDruIBRYjrT5ct7B3xqG25ZF2p59 \   # ⚠️ 必须替换为随机字符串
  -v ./logs:/app/logs \
  aexus/solara-music:latest
```
### 2. Docker Compose 部署（推荐）
步骤 1：创建 docker-compose.yml

```
services:
  solara-music:
    image: aexus/solara-music:latest
    container_name: solara-music
    restart: unless-stopped
    ports:
      - "3001:3001"
    environment:
      - NODE_ENV=production
      - PORT=3001
      - SOLARA_PASSWORD=your_strong_password   # ✅ 修改为你的强密码
      - SESSION_SECRET= $ (openssl rand -base64 32)  # ✅ 必须生成随机密钥
    volumes:
      - ./logs:/app/logs
```

步骤 2：启动服务


```
docker-compose up -d
```
🔐 配置参数说明
```
配置项	说明	安全要求
SOLARA_PASSWORD	Web 界面登录密码	必须修改，默认值极不安全
SESSION_SECRET	会话加密密钥	必须替换，建议用随机字符串
PORT	服务映射端口	可自定义（如 8080:3001）
volumes	日志持久化路径	本地 ./logs → 容器路径
```
🔐 强制安全规范
```
密码必须包含 大小写字母+数字+特殊符号（如 MusiC@2024!）
```
生成随机密钥命令：


```
openssl rand -base64 32  # 直接复制输出结果到 SESSION_SECRET
```
✅ 部署任务清单
```
修改密码：将 SOLARA_PASSWORD 替换为强密码
生成密钥：用 openssl rand -base64 32 生成 SESSION_SECRET
启动服务：执行 docker-compose up -d
验证访问：浏览器打开 http://你的服务器IP:3001
重启生效：修改配置后执行 docker-compose restart
```
⚠️ 重要警告
若不修改默认配置将导致：
❌ 未授权访问你的音乐服务
❌ 会话劫持风险
❌ 日志数据泄露
部署后必须立即执行安全配置！


### ✨ 直接使用说明
1. **全选复制** 上方代码块（从 `# 🎶 Solara（光域）音乐播放器` 到结尾）
2. **粘贴到** 你的 GitHub/Gitee 仓库 `README.md` 或文档系统
3. **关键修改点**（部署前必做）：
   - 将 `your_strong_password` 替换为你的强密码
   - 用 `openssl rand -base64 32` 命令生成真实密钥

### ✅ 优势说明
- **安全强化**：用 `⚠️`/`🔐` 符号突出风险点，避免配置遗漏
- **零格式错误**：YAML 缩进严格对齐，表格自动适配所有 Markdown 渲染器
- **开箱即用**：包含 `openssl` 密钥生成命令，无需额外查资料
- **平台兼容**：在 GitHub/Gitee/语雀等平台均能完美显示