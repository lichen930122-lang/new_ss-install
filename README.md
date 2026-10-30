# new_ss-install

和旧仓库 **`lichen930122-lang/ss-install` 不是同一套**。旧仓库继续给 Airlink / 认设备 / HTTPS 443，不要混用。

本仓库独享：**每口同时 1 个公网 IP**。同一人从 WiFi1 切到 WiFi2（公网 IP 变了）：旧 IP 大约 **1 秒**没流量就清坑，新 IP **密码和端口对了**就能连。没有报名口、没有令牌、没有指纹。普通 Shadowsocks 直接用 `ss://`。

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

不要对旧仓库那批「认设备」机器跑这个脚本。

## 改密码（不用重装）

单端口，随机新密码：

```bash
./shadowsocks.sh set-pass
```

多端口，只改其中一个（随机新密码）：

```bash
./shadowsocks.sh set-pass 23859
```

自己指定新密码（单端口、多端口都行）：

```bash
./shadowsocks.sh set-pass 23859 '你的新密码'
```

单端口也可以直接：

```bash
./shadowsocks.sh set-pass '你的新密码'
```

会写回配置、重启服务，并更新 `/root/shadowsocks-users.txt`（如果有）。旧链接立刻不能用。
