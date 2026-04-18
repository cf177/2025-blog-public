## 1. 安装 Meting API

由于应用商店未上架 Meting API，常规的安装方式是从容器页面拉取镜像并创建容器。这里建议使用 **第三方应用商店一键部署**。

### 获取第三方应用商店列表

1. 打开 **计划任务页**，点击 **创建计划任务**  
2. 任务类型选择 **Shell 脚本**  
3. 脚本内容如下：

```bash
rm -rf /opt/1panel/resource/apps/local/appstore-localApps
git clone -b localApps https://github.com/okxlin/appstore /opt/1panel/resource/apps/local/appstore-localApps
cp -rf /opt/1panel/resource/apps/local/appstore-localApps/apps/* /opt/1panel/resource/apps/local/
rm -rf /opt/1panel/resource/apps/local/appstore-localApps
echo "✅ 安装成功"

其它必填项可自定义。
在操作列点击 执行。

前往应用商店点击 更新应用列表。
搜索 Meting-API 并点击安装。

⚠️ 安装时需要设置端口，并放行对应防火墙。如果面板开启了防火墙，请勾选 端口外部访问。

验证安装
在 已安装中找到该应用，检查状态是否为 已启动。

在浏览器访问 http://IP:端口 验证是否成功。

2. 配置 HTTPS
如需通过 HTTPS 安全访问，需要绑定域名、安装 SSL 证书并设置反向代理。

域名解析
在域名服务商处将自定义二级域名解析到部署 Meting-API 的服务器。

SSL 证书
可在域名服务商处申请免费 SSL 证书。

1Panel 配置反向代理
在 网站页创建网站，选择 反向代理。

主域名填写前面解析的域名。

代理地址添加：

text
127.0.0.1:3000
（保持与创建容器时设置的端口一致）

创建完成后点击配置，在 HTTPS 中启用 HTTPS 并导入证书文件（.pem）和密钥文件（.key）。

在配置文件里与其它 location 项同级添加内容：

nginx
location /meting/ {
  proxy_pass http://localhost:3000/; # 设置的端口
  proxy_set_header X-Forwarded-Host $scheme://$host:$server_port/meting;
}
⚠️ 注意事项：

根据官方文档，配置反向代理时必须使用给定文本。

访问时需在域名后添加 /meting/，否则 HTTPS 会退回到 HTTP。

最终访问地址
text
https://域名/meting/
3. 防火墙端口放行示例
如果服务器启用了防火墙，需要放行容器端口，例如 3000：

使用 UFW
bash
sudo ufw allow 3000/tcp
sudo ufw reload
使用 firewalld
bash
sudo firewall-cmd --permanent --add-port=3000/tcp
sudo firewall-cmd --reload
4. 总结
使用第三方应用商店一键部署 Meting API

配置防火墙端口放行

绑定域名并申请 SSL 证书

在 1Panel 中设置反向代理，访问地址需加 /meting/

最终即可通过 HTTPS 安全访问：

https://域名/meting/