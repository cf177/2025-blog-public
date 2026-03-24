🧾 详细介绍
🎶Solara（光域） 是一个极简风格的基于免费API的音乐播放器。由轻量后端服务支撑的现代化网页音乐播放器，整合多种音乐聚合接口，覆盖搜索、播放与音频下载全流程。

动图封面
✨ 核心功能
🎨 沉浸式美学体验：亮/暗模式 + 玻璃拟态界面，自动取色渲染背景，视觉氛围拉满。
📱 移动端友好设计：竖屏布局适配手势操作，单手浏览、播放、收藏都顺手。
🔍 多源曲库检索：支持跨站搜索、分页浏览与批量导入，找歌更高效。
📻 播放队列 & 收藏管理：即时响应、自动持久化，支持导入导出与独立播放设置。
🔁 播放体验丰富：多种播放模式 + 动态歌词视图 + 锁屏控制，听歌更顺畅。
☁️ 轻量后端支持：Cloudflare Functions 聚合数据源，支持多码率下载与跨域播放。
🐳部署指南
🎯 Docker命令
docker run -d \
  --name solara-music \
  --restart unless-stopped \
  -p 3001:3001 \
  -e NODE_ENV=production \
  -e PORT=3001 \
  -e SOLARA_PASSWORD=solara123 \
  -e SESSION_SECRET=KLmlKDruIBRYjrT5ct7B3xqG25ZF2p59 \
  -v ./logs:/app/logs \
  aexus/solara-music:latest
🎯 Docker Compose(本教程使用)
docker-compose.yml

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
      - SOLARA_PASSWORD=solara123  # 修改为你的密码
      - SESSION_SECRET=KLmlKDruIBRYjrT5ct7B3xqG25ZF2p59    # 修改为随机字符串
    volumes:
      - ./logs:/app/logs