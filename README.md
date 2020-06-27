详细教程：[进入](https://github.com/sprov065/soga/wiki)

商业版价格：[进入](https://github.com/sprov065/soga/wiki/05-%E8%8E%B7%E5%8F%96%E5%95%86%E4%B8%9A%E7%89%88%E6%8E%88%E6%9D%83%E7%A0%81)

# soga 后端
soga 后端是一个支持 v2ray 和 trojan 的后端

## v2ray
soga 后端针对 v2ray 占内存的特点使用 C 语言特别优化了 v2ray 的内存占用，在相同用户数量和 alterId 下，相对于原版 v2ray 来说可节省 40-60% 的内存空间，用户数量越多，节省的内存就越多，用户较少则节省不明显。

## trojan
soga 同时实现了 trojan 协议，trojan 协议相对于 v2ray 来说更轻量和高效，在大量用户下也几乎不占多少内存，推荐优先选择 trojan。

## 支持的前端
|前端              |v2ray              |trojan           |
|------------------|------------------|------------------|
|sspanel-uim	   |√                 |√                 |
|v2board	   |√                 |√                 |
|WHCMS             |开发中             |计划中            |
|v2-ui             |计划中             |计划中            |


## 功能介绍
|功能              |v2ray              |trojan           |
|------------------|------------------|------------------|
|单端口多用户	   |√                 |√                 |
|用户流量统计	   |√                 |√                 |
|限速              |√                 |√                 |
|限连接数           |√                 |√                |
|服务器信息上报      |√                |√                 |
|在线人数上报        |√                |√                 |
|在线IP上报         |√                 |√                 |
|自动增删用户       |√                 |√                  |
|审计规则           |√                 |√                 |
|禁止封禁IP连接      |√                |√                 |
|中转规则           |√                 |√                 |
|自动申请tls证书     |√                 |√                 |
|自动续签tls证书     |√                 |√                 |

## v2ray 支持的协议
|协议              |支持情况           |
|----------------- |------------------|
|tcp               |√                 |
|tcp+tls	       |√                 |
|ws                |√                 |
|ws+tls            |√                 |
|cdn+ws            |√                 |
|cdn+ws+tls        |√                 |

## trojan 支持的协议
|协议              |支持情况           |
|----------------- |------------------|
|trojan协议         |√                 |


## 对接方式
|对接方式           |v2ray             |trojan           |
|------------------|------------------|------------------|
|webapi     	   |√                 |√                 |
|数据库   	        |开发中             |开发中            |
|docker webapi     |√                 |√                 |
|docker 数据库     |开发中             |开发中            |

## 前端对接方式对照表
<table>
    <tr>
        <th>前端</th>
        <th>后端</th>
        <th>webapi</th>
        <th>数据库</th>
        <th>docker</th>
    </tr>
    <tr>
        <th rowspan="2">sspanel-uim</th>
        <td>v2ray</td>
        <td>√</td>
        <td rowspan="4" align="center">开发中</td>
        <td>√</td>
    </tr>
    <tr>
        <td>trojan</td>
        <td>√</td>
        <td>√</td>
    </tr>
    <tr>
        <th rowspan="2">v2board</th>
        <td>v2ray</td>
        <td>√</td>
        <td>√</td>
    </tr>
    <tr>
        <td>trojan</td>
        <td>√</td>
        <td>√</td>
    </tr>
    <tr>
        <th rowspan="2">WHCMS</th>
        <td>v2ray</td>
        <td rowspan="2" colspan="3" align="center">开发中</td>
    </tr>
    <tr>
        <td>trojan</td>
    </tr>
    <tr>
        <th rowspan="2">v2-ui</th>
        <td>v2ray</td>
        <td rowspan="2">计划中</td>
        <td>×</td>
        <td rowspan="2">计划中</td>
    </tr>
    <tr>
        <td>trojan</td>
        <td>×</td>
    </tr>
</table>

加入我们：[Telegram群组](https://t.me/soga_v2ray)
021 SSPanel Uim 对接教程 v2ray
sprov edited this page 6 days ago · 20 revisions
详细图文教程（推荐）
https://blog.sprov.xyz/2020/06/06/sspanel-uim-v2ray-trojan/

一键安装&更新
bash <(curl -Ls https://blog.sprov.xyz/soga.sh)
或者，两个都可以

bash <(curl -Ls https://raw.githubusercontent.com/sprov065/soga/master/install.sh)
第一步，配置 soga
第一次安装完成后，编辑配置文件：

配置文件位置在 /etc/soga/soga.conf

配置文件位置在 /etc/soga/soga.conf

配置文件位置在 /etc/soga/soga.conf

基础配置
type=sspanel-uim                             # 必填这个
server_type=v2ray                            # 必填这个
api=webapi                                   # 目前支持 webapi 对接，数据库对接以后更新支持
webapi_url=https://xxx.com/                  # webapi url，填写面板主页地址
webapi_mukey=xxxx                            # webapi key
node_id=1                                    # 节点id
soga_key=                                    # 授权key，社区版无需填写，最多支持88用户，商业版无限制
user_conn_limit=0                            # 限制用户IP数，0代表无限制，默认会优先使用面板设置的限制IP数，在部分旧版面板下可能会获取不到，则使用这个值
配置证书
若未开启 tls，则无需配置证书

soga 支持三种方式配置证书，任选其一即可

① 手动指定证书路径
以 / 开头的绝对路径
cert_file=                                   # 手动指定证书路径
key_file=                                    # 手动指定密钥路径
② http 模式自动申请证书（推荐）
确保服务器中没有其它程序占用 80 端口，申请和续签时需要临时使用
确保域名已解析到本服务器的IP
若开启CDN，则必须确保CDN不会跳转https，否则推荐dns验证
cert_domain=xxx.com                          # 申请证书的域名
cert_mode=http                               # 申请模式
③ dns 模式自动申请证书
支持一百多种 DNS 服务商
此配置方式较复杂，但最通用
该页面列出了所有支持的 DNS 服务商：https://github.com/acmesh-official/acme.sh/wiki/dnsapi
CloudFlare 配置示例

cert_domain=xxx.com                          # 申请证书的域名
cert_mode=dns                                # 申请模式
dns_provider=dns_cf                          # DNS 提供商

DNS_CF_Email=xxx@xx.com                      # CF 邮箱，注意加 DNS_ 前缀
DNS_CF_Key=xxxxx                             # CF API 密钥，注意加 DNS_ 前缀
DNSPod 配置示例

cert_domain=xxx.com                          # 申请证书的域名
cert_mode=dns                                # 申请模式
dns_provider=dns_dp                          # DNS 提供商

DNS_DP_Id=111                                # DNSPod 用户 id，注意加 DNS_ 前缀
DNS_DP_Key=xxxxx                             # DNSPod API 密钥，注意加 DNS_ 前缀
其它的 DNS 服务商都能在这个页面找到：https://github.com/acmesh-official/acme.sh/wiki/dnsapi

配置要点：

找到 DNS 提供商的名称，以 dns_ 开头，后面跟提供商的缩写
找到 DNS 提供商所需要配置的内容，区分大小写，一般都是 API 密钥之类的，注意要在 soga 配置中加上 DNS_ 前缀，防止配置冲突
第二步，配置前端节点地址
假设有域名 hk.domain.com，根据具体示例开启或未开启 CDN，服务器 IP 为 1.3.5.7
path 参数需以 / 开头
server 参数是显示给用户连接的地址，在开启 CDN 的情况下一定要填 CDN 域名，否则将无法使用 CDN
NAT 时使用 inside_port，inside_port 表示节点内部监听的端口，当 NAT 商家提供给你的外部端口和你服务器监听的内部端口不一致时使用
节点地址格式：
IP;用户连接的端口;alterId;(tcp或ws);(tls或不填);path=/xxx|host=xxxx.com|server=xxx.com|inside_port=xxx
tcp 示例，请注意 tcp 后面有两个分号
ip;12345;2;tcp;;server=域名
示例：1.3.5.7;12345;2;tcp;;server=hk.domain.com
tcp + tls 示例
ip;12345;2;tcp;tls;server=域名|host=域名
示例：1.3.5.7;12345;2;tcp;tls;server=hk.domain.com|host=hk.domain.com
ws 示例，若不用CDN，可以去掉host，注意ws后面有两个分号
ip;80;2;ws;;path=/xxx|server=域名|host=CDN域名
示例：1.3.5.7;80;2;ws;;path=/v2ray|server=hk.domain.com|host=hk.domain.com
ws + tls 示例，若不用CDN，可以去掉host
ip;443;2;ws;tls;path=/xxx|server=域名|host=CDN域名
示例：1.3.5.7;443;2;ws;tls;path=/v2ray|server=hk.domain.com|host=hk.domain.com
偏移端口 ws
当用户连接端口与程序监听端口不一致时使用，例如，中转机器连接端口与后端监听端口不同时

ip;监听端口;2;ws;;path=/xxx|server=域名|host=CDN域名|outside_port=用户连接端口
中转使用场景解释

落地服务器IP;落地服务器监听端口;2;ws;;path=/xxx|server=转发服务器IP或域名|host=CDN域名|outside_port=转发服务器监听端口
示例：1.3.5.7;80;2;ws;;path=/v2ray|server=hk.domain.com|host=hk.domain.com|outside_port=34567
偏移端口 ws + tls
当用户连接端口与程序监听端口不一致时使用，例如，中转机器连接端口与后端监听端口不同时

ip;监听端口;2;ws;tls;path=/xxx|server=域名|host=CDN域名|outside_port=用户连接端口
中转使用场景解释

落地服务器IP;落地服务器监听端口;2;ws;tls;path=/xxx|server=转发服务器IP或域名|host=CDN域名|outside_port=转发服务器监听端口
示例：1.3.5.7;443;2;ws;tls;path=/v2ray|server=hk.domain.com|host=hk.domain.com|outside_port=34567
tcp 模式也是同理，这里不再举例。

第三步、启动 soga
soga start
