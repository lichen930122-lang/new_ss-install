# new_ss-install

和旧仓库 **`lichen930122-lang/ss-install` 不是同一套**。旧仓库继续给 Airlink / 认设备 / HTTPS 443，不要混用。

本仓库独享：**每口同时 1 个公网 IP**。同一人从 WiFi1 切到 WiFi2（公网 IP 变了）：旧 IP 大约 **1 秒**没流量就清坑，新 IP **密码和端口对了**就能连。没有报名口、没有令牌、没有指纹。普通 Shadowsocks 直接用 `ss://`。

脚本地址：

```text
https://raw.githubusercontent.com/lichen930122-lang/new_ss-install/main/shadowsocks.sh
```

下面命令若机器上的脚本偏旧，先 wget 再跑。

## 1. 新机器

```bash
wget -O shadowsocks.sh https://raw.githubusercontent.com/lichen930122-lang/new_ss-install/main/shadowsocks.sh
chmod +x shadowsocks.sh
./shadowsocks.sh 2>&1 | tee shadowsocks.log
```

多用户时选「每端口 1 个公网 IP」。云安全组只放行业务口 **TCP+UDP**，不必开 443。账号在屏幕上，并写入 `/root/shadowsocks-users.txt`。

## 2. 已经用本仓库装过、只补独享

```bash
./shadowsocks.sh limit-on
```

不改密码。不要对旧仓库那批「认设备」机器跑这个脚本。

## 3. 关掉独享

```bash
./shadowsocks.sh limit-off
```

## 4. 改密码（不用重装）

```bash
./shadowsocks.sh set-pass
./shadowsocks.sh set-pass 23859
./shadowsocks.sh set-pass 23859 '你的新密码'
./shadowsocks.sh set-pass '你的新密码'
```

不写密码就是随机生成。会写回配置、重启服务，并更新 `/root/shadowsocks-users.txt`（如果有）。旧链接立刻不能用。

## 5. 看账号（和 users.txt 同一格式）

```bash
./shadowsocks.sh show 23865
./shadowsocks.sh show 23865 23867
./shadowsocks.sh show
```

打印用户、端口、密码、普通链接。不写端口就是全部。本仓库没有 Airlink。也可以：

```bash
grep -A4 '23865' /root/shadowsocks-users.txt
cat /root/shadowsocks-users.txt
```

## 6. 卸载

```bash
./shadowsocks.sh uninstall
```

## 对照

| 机器状态 | 命令 |
|---|---|
| 新机器 | `wget` + `chmod` + `./shadowsocks.sh 2>&1 \| tee shadowsocks.log` |
| 补独享 | `./shadowsocks.sh limit-on` |
| 关独享 | `./shadowsocks.sh limit-off` |
| 改某一口密码 | `./shadowsocks.sh set-pass` / `set-pass 23859` / `set-pass 23859 '新密码'` |
| 看账号 | `./shadowsocks.sh show 23865` ；多个口空格分开；不写端口=全部 |
| 卸载 | `./shadowsocks.sh uninstall` |
