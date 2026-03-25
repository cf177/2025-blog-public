一个NAS、服务器导航面板、简易docker管理器、Homepage、浏览器首页

默认账号密码
账号：admin@sun.cc
密码：12345678

docker-compose 运行
仅供参考，请根据自己的需求修改 v1.4.0及以上版本

version: "3.2"

services:
  sun-panel:
    image: "hslr/sun-panel:latest"
    container_name: sun-panel
    volumes:
      - ./conf:/app/conf
      - /var/run/docker.sock:/var/run/docker.sock # 挂载docker.sock
      # - ./runtime:/app/runtime # 挂载日志目录
      # - /mnt/sata1-1:/os # 硬盘挂载点（根据自己需求修改）
    ports:
      - 3002:3002
    restart: always