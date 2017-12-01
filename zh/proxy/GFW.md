# 科学上网综述


## 主机商

目前市面上常用的主机商有下面一些：

* Google Cloud Platform （以下简称 GCP）
    * 提供一年$300美金的免费试用
    * 需要 Visa/MasterCard 信用卡
    * 机房众多，其中台湾机房更是极品，延迟50ms左右
* Amazon Web Services (AWS)
    * 提供一年免费试用，试用包括一个最低配置的主机和每月15G流量
* Linode
    * $5/月起，东京机房质量较好
* DigitalOcean
    * $5/月起，最近的机房是新加坡
* Vultr
    * $2.5/月起，有东京机房，但2.5的可能缺货买不到
* 搬瓦工
    * KVM/OVZ 皆$2.99或$4.99/月起,有洛杉矶机房,凤凰城机房等等

### 如何选择主机商

在不考虑价格的情况下，阿里云香港机房 > GCP 台湾机房 > 其它日本线路 > 美国线路。


| 地区 | 运营商 | 优先机房 |
| ---- | ---- | ---- |
| 全国 | 长宽、鹏博士等三级运营商 | 反正外网限速 5Mbps 选啥都一样 |
| 北方 | 移动 | Linode/Vultr 东京 |
| 全国 | 电信 | cn2 线路 |


### 推荐链接

如果你使用下面的链接注册，那么你会收到相应的一小笔试用赠金，如果你将来消费开发者会收到$10的奖励。这些奖励将被用来购买主机运营一些 HyperApp 相关的公共项目。

（PS：文中其它地方出现的所有链接没有加推荐代码）

* [Vultr - $10 试用](http://www.vultr.com/?ref=6833039)
* [Linode - $20 试用](https://www.linode.com/?r=ad279824479def3ef162e3e99498242d4046ec1b)
* [Digital Ocean - $10 试用](https://m.do.co/c/a70d556c37f7)


----


## 代理软件

下面主要有两类翻墙手段，一个是轻量级代理，一个是 VPN 类。


| 应用  | iOS | Android | Mac | Windows | 安全性 |
| ---- | ---- | ---- | ---- | ---- | ---- |
| ss   | ✅  | ✅ | ✅ | ✅ | 👍👍👍👍 |
| SSR | ✅ | ✅ | ✅ | ✅ | 👍👍👍👍👍 |
| V2Ray | ⚠️ | ✅ | ✅ | ✅ | 👍👍👍👍👍 |
| kcptun | ❌ | ✅ | ✅ | ✅ | 👍👍 |
| AnyConnect | ✅ | ✅ | ✅ | ✅ | 👍👍👍👍👍 |
| OpenVPN | ✅ | ✅ | ✅ | ✅ | 👍👍 |
| IpSec VPN | ✅ | ✅ | ✅ | ✅ | 👍 |
* iOS使用Shadowrocket作为客户端可支持V2Ray除mkcp外所有链接方式.协议选择Vmess即可


* 轻量级代理
    * Shadowsocks （SS）
        * 专门为墙而生的 socks 代理，HyperApp 中包括两个版本，一个是比较老的 Shadowsocks Python 原版，一个是 C 语言实现的一直在更新的 libev 版。推荐后者。
        * 服务端和客户端均需要专属软件，客户端全平台都支持，选择多
    * ShadowsocksR （SSR）
        * Shadowsocks 的一个魔改版，添加了许多混淆方式，某些运营商可能无法使用 SS （比如长城宽带），这是可以使用 SSR 来代替，SSR 可以将代理伪装成普通的网站请求，以此来跳过运营商的封锁。
        * 服务端和客户端均需要专属软件，客户端全平台都支持，选择多
    * kcptun
        * 如果你的机房线路很好（比如 GCP 台湾机房）那么直接用 SS 就有很好的速度，但是某些线路非常差的机房就需要 kcptun 这种黑科技了，上面的代理都是使用 TCP 来连接的，但 kcptun 使用 UDP （一般的下载软件也都是 UDP）通过多倍发包在延迟高丢包高的线路上来实现网络加速。
        * 服务端和客户端均需要专属软件，客户端全平台都支持，但选择较少
    * V2Ray
        * V2Ray 的志向很大，要做一个全能的代理平台，其内置了 HTTP,Socks,Shadowsocks,VMess等协议的代理。功能非常强大，但缺点是配置非常复杂。不过还好 HyperApp 能方便安装配置其服务端。另外 V2Ray 不仅可以使用 TCP 还支持使用 mKCP 多倍发包来加速。
        * 服务端和客户端均需要专属软件，客户端全平台都支持，但选择较少
* VPN 类
    * IPSec/L2TP VPN： 
        * ⚠️ 不推荐，出墙的话会被秒封，墙内也不推荐使用，但优点是系统都内置支持
    * OpenVPN: 
        * ⚠️ 不推荐，但如果墙内用则推荐，安全性更高，缺点是各个平台都需要手动下载软件
    * OpenConnect (Cisco AnyConnect) 
        * ❤️ 推荐，如果翻墙需要 VPN 则强烈推荐这个。许多外企都使用 Cisco AnyConnect 来办公，所以受到的墙的干扰非常少。安全性也很高。

### 其它加速技术

#### BBR

BBR 是 Google 开发的一种新的TCP发包方式，在较低丢包率和稍微延迟的线路上能够达到比较好的加速效果。而且只需要在服务器端安装即可。


### 如何选择？

1. 如果你机房的线路非常好（香港、台湾机房）那么直接使用 BBR + SS/SSR 即可。
2. 如果你机房的线路很差（比如丢包很高或者距离很远）那么可以使用 BBR + SS/SSR + kcptun。
3. 如果你的运营商会封锁 SS 或者进行 QoS，那么使用 BBR + SSR 混淆，或者 BBR + VMess 的 TLS 混淆。
