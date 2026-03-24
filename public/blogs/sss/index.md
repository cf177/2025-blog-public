🎶Solara（光域） 是一个极简风格的基于免费API的音乐播放器。由轻量后端服务支撑的现代化网页音乐播放器，整合多种音乐聚合接口，覆盖搜索、播放与音频下载全流程。
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