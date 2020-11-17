
## 1、前言
感謝 koolshare.cn 提供 KoolProxy, 使用风险由用户自行承担
本程序运行需要联网下载最新的 KoolProxy 到内存中运行, 也正因此本程序大小可以忽略不计.为了区分，暂且更名为：LedeProxy

## 2、简介
本软件包是 KoolProxy 的 LuCI 控制界面,

## 3、软件包文件结构:
 相比原koolproxy，做了调整。

## 4、依赖
软件包的正常使用需要依赖 curl, dnsmasq-full, iptables, ipset 和 dnsmasq-extra.

## 5、配置
软件包的配置文件路径: /etc/config/koolproxy
此文件为 UCI 配置文件, 配置方式可参考 Wiki -> Use-UCI-system 和 OpenWrt Wiki

## 6、编译
git clone https://github.com/lede/luci-app-ledeproxy.git package/luci-app-ledeproxy

make && sudo make install

选择要编译的包 LuCI -> 3. Applications 

make menuconfig

开始编译

make package/feeds/luci-app-koolproxy/compile V=s

# 7、关于IPv6支持(基于透明代理一刀切)
需要在防火墙添加一条规则：

ip6tables -t nat -I PREROUTING -p tcp -j REDIRECT --to-ports 3000

```
#已知副作用:
#一刀切劫持内网所以设备的IPv6 TCP流量.
#无法使用IPv6建立主动传入连接.
#如果未安装证书,打开启用HTTPS的网站会报错.
```

**NOTE:**

如果出现国外流量无法去广告(IPv4),请修改所使用代理的防火墙规则,必须让KP的规则在代理规则之上,检测命令:

``` bash
iptables -t nat -L PREROUTING
```

观察**KOOLPROXY**规则是否在所使用的代理的规则之上.

### 8、内置规则列表

[静态规则](https://gitee.com/ledewrt/ledeproxyrule/raw/master/rules/koolproxy.txt)

[每日规则](https://gitee.com/ledewrt/ledeproxyrule/raw/master/rules/daily.txt)

[视频规则](https://gitee.com/ledewrt/ledeproxyrule/raw/master/rules/kp.dat)

[ipset](https://gitee.com/ledewrt/ledeproxyrule/raw/master/ipsetadblock/koolproxy_ipset.conf)

[adblock](https://gitee.com/ledewrt/ledeproxyrule/raw/master/ipsetadblock/dnsmasq.adblock)

### 9、第三方规则

[ABP规则](https://gitee.com/ledewrt/ledeproxyrule/raw/master/rules/easylistchina.txt) 

（ABP规则是CJX's Annoyance List+China+EasyList的二合一规则） 注：CJX's Annoyance List (反自我推广,移除anti adblock,防跟踪规则列表)是"EasyList China+EasyList" & "EasyPrivacy"的补充）

[Yhosts规则](https://gitee.com/ledewrt/ledeproxyrule/raw/master/rules/yhosts.txt)

[Fanboy规则](https://ledewrt.coding.net/p/ledeproxy/d/rulebin/git/raw/master/rules/fanboy.txt)

(gitee的地址会导致大于1M的下载出问题，故用coding的地址）

[AntiAD规则](https://gitee.com/ledewrt/ledeproxyrule/raw/master/rules/antiad.txt)

[乘风视频](https://gitee.com/ledewrt/ledeproxyrule/raw/master/rules/mv.txt)

### 10、订阅规则

[订阅规则](https://gitee.com/ledewrt/ledeproxyrule/raw/master/rules/kpr_our_rule.txt

