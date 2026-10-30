# new_ss-install

和旧仓库 **`lichen930122-lang/ss-install` 不是同一套**。旧仓库继续给 Airlink / 认设备 / HTTPS 443，不要混用。

本仓库独享：**每口同时 1 个公网 IP**；占坑的人断开后约 **2 秒**清坑；下一台 **密码和端口对了**即可连。没有报名口、没有令牌、没有指纹。普通 Shadowsocks 直接用 `ss://`。

## 新机器

```bash
wget -O shadowsocks.sh https://raw.githubusercontent.com/lichen930122-lang/new_ss-install/main/shadowsocks.sh
chmod +x shadowsocks.sh
./shadowsocks.sh 2>&1 | tee shadowsocks.log
```

多用户时选「每端口 1 个公网 IP」。云安全组只放行业务口 **TCP+UDP**，不必开 443。

## 已经用本仓库装过、只补独享

```bash
./shadowsocks.sh limit-on
```

不改密码。不要对旧仓库那批「认设备」机器跑这个脚本。
