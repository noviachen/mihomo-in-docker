# 声明
仅限技术交流，请勿用于非法用途。

# 简单的说明
基于 https://github.com/lululau/clashindocker 修改，里面的设置尽量简化了，让小白也可以快速上手。主要更改的内容有：
> 1. 自动创建 macvlan 网络（仅限 IPv4）
> 2. 默认打开 IPv4 转发功能
> 3. 内置 metacubexd，以免网络问题下载失败
> 4. 使用 ACL4SSR_Online 分流规则

# 制作 Docker 镜像并创建容器

1. 获取代码

```bash
git clone https://github.com/noviachen/mihomo-in-docker
cd mihomo-in-docker
cp example.yml config.yml
```

2. 将`docker-compose.yml`中的`ipv4_address`修改为需要给 Docker 容器分配的 IP 地址，`eth0`为机器的网卡名称，`subnet`为局域网的网段，`gateway`为局域网的网关。

3. 修改`config.yml`中的`proxy-provider`的`url`为你的订阅地址。示例中是两个地址的情况，如果只有一个，删除其中一个和下面`proxy-groups`对应的部分即可。

4. 制作和启动容器
```bash
docker-compose up -d 
```

5. 假设你的 Docker 容器 IP 地址为`192.168.3.23`，通过`http://192.168.3.23:9090/ui/`可以管理。后端地址为`http://192.168.3.23:9090/`，密码为`yourpassword`。

6. 在同一个局域网下，将其他机器的网关和 DNS 设置为`192.168.3.23`，或者在网关的 DHCP 中设置。
