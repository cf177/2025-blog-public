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
```

其它必填项可自定义。
在操作列点击「执行」。

前往应用商店点击「更新应用列表」。
搜索 `Meting-API` 并点击安装。

⚠️ 安装时需要设置端口，并放行对应防火墙。如果面板开启了防火墙，请勾选 **端口外部访问**。

### 验证安装
在「已安装」中找到该应用，检查状态是否为 **已启动**。

在浏览器访问：
```text
http://服务器IP:端口
```
验证是否部署成功。

---

## 2. 配置 HTTPS

如需通过 HTTPS 安全访问，需要绑定域名、安装 SSL 证书并设置反向代理。

### 域名解析
在域名服务商处，将自定义二级域名解析到部署 Meting-API 的服务器 IP。

### SSL 证书
可在域名服务商处申请免费 SSL 证书。

### 1Panel 配置反向代理
1. 进入「网站」页面，创建网站，选择 **反向代理**
2. 主域名填写已解析的域名
3. 代理地址填写：
```text
127.0.0.1:3000
```
> 保持与创建容器时设置的端口一致

创建完成后进入网站配置，在 `HTTPS` 选项中启用 HTTPS，导入证书文件 `.pem` 和密钥文件 `.key`。

在 Nginx 配置文件中，与其它 `location` 同级添加以下代码：

```nginx
location /meting/ {
  proxy_pass http://localhost:3000/; # 替换为你的实际端口
  proxy_set_header X-Forwarded-Host $scheme://$host:$server_port/meting;
}
```

⚠️ 注意事项：
- 根据官方文档，反向代理规则必须按上述配置填写
- 访问时必须在域名后拼接 `/meting/`，否则 HTTPS 会降级为 HTTP

最终访问地址：
```text
https://你的域名/meting/
```

---

## 3. 防火墙端口放行示例

若服务器开启防火墙，需放行 Meting 容器端口（示例：`3000`）

### 使用 UFW
```bash
sudo ufw allow 3000/tcp
sudo ufw reload
```

### 使用 firewalld
```bash
sudo firewall-cmd --permanent --add-port=3000/tcp
sudo firewall-cmd --reload
```

---

## 4. 总结
1. 通过第三方应用商店一键部署 Meting API
2. 放行服务器防火墙对应端口
3. 绑定域名并配置免费 SSL 证书
4. 在 1Panel 配置 Nginx 反向代理
5. 携带 `/meting/` 路径实现 HTTPS 正常访问

最终安全访问地址：
```text
https://你的域名/meting/
```