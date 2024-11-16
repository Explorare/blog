title: Amazon Cloud Dirve Review

date: 2015-12-04 14:29:38

---

# 介绍

笔者在今天上午<sup>[\[1\]](#R1)</sup>无意间发现渣玛逊黑五特惠<sup>[\[2\]](#R2)</sup>中，ACD(Amazon Cloud Drive) 的 special offer 特别的诱人，unlimited plan 包年 5 USD<sup>[\[3\]](#R3)</sup>.

首先是购买方面，只能使用双币卡如 VISA 或者 MasterCard，从下单到收到 ACD 账户开通邮件耗时一小时左右。

购买之前笔者主要使用百度云来保存分享专辑~~和本子~~这类体积小的数据，尝试同步系统备份上去最后因为文件大小限制而作罢。<sup>[[4]](#R5)</sup>

<!--more-->

# Price & Feature

# 体验

网页端做的挺好看，可以后台上传，支持在线浏览图片和视频，不能预览压缩包的内容，有垃圾箱。建议语言设成英文，因为中文默认的是宋体，丑爆了 ( ´_ゝ`)

![WebPanel.png](https://c.hime.io/images/2Jv.png "Overview")

![WebPanel02.png](https://c.hime.io/images/V3a.png "All")

![Restore.png](https://c.hime.io/images/gjD.png "Deleted")

客户的作用更多的是用来上传和同步，下载的话只能同步全部内容到本地，而不能选择特定文件和文件夹。万一没注意一下子全都同步下来会很伤的，点击 [浏览文件] 功能会直接打开网页端，不过网页端做的挺好的所以也无所谓了。

![Client01.png](https://c.hime.io/images/7JX.png "Login")

![Client02.png](https://c.hime.io/images/Qom.png "Overview")

注意：~~客户端会根据你的系统语言选择登陆区域，也就是说如果你使用简体中文系统，就会默认使用 amazon.cn 登陆，你输入 amazon.com 的账户会提示密码错误。解决办法是暂时将系统语言设为 en-US, 登陆账号后再切换回来。~~

# 测试环境

**系统环境**

VMWare Workstation 12 pro

Windows 8.1 Enterprise x64

**测试工具**

Chrome v47.0.2526.73 m (64-bit)

[Speedtest.net By Ookla](www.speedtest.net)

Speed Meter from NetWorx v5.4.2 64-bit

GlassWire v1.1.36b

Proxifier v3.28

ShadowSocks for Windows v2.5.8

DNS2SOCKS v2.0

**测试方法**

首先在 VMWare 部署了一个 MSDN 版的 Windows 8.1，关闭了系统自动更新避免干扰。SS 连接远程伺服器进行加密代理，通过 Proxifier 强制 Amazon Cloud Drive 通过 SS 的 SOCKS5 加密隧道进行连接。 Speed Meter 手动测速，GlassWire 监测 ACD 发起的连接的目标地址和协议。

# 速度测试

## 直连

**Bandwidth**

![4885946495.png](https://c.hime.io/images/jlq.png "China Unicom; Bandwidth: Download: 12.19 Mb/s; Upload 13.10 Mb/s; Ping: 1 ms")

**Traceroute**

从 DNS 记录能看到它主要访问了 `cdws.us-east-1.amazonaws.com` 这个域名，归属于 AWS 旗下，可推测 ACD 和 AWS 共用部分硬件设施，但采用了不同的销售策略。不通过代理直接 traceroute 这个域名可看到有比较高的丢包率。

|Hop| Host IP | Host Name | AS Name | AS | Loss % | Min Latency | Max Latency | Average Latency | StdDev
|---|---|---|---|---|---|---|---|---|---|
| 5 | 219.158.21.33 | 219.158.21.33 |  |  | 0.0% | 38 | 53 | 42 | 3.7 
| 6 | 219.158.3.234 | 219.158.3.234 |  |  | 11.1% | 99 | 175 | 128 | 26.5 
| 7 | 219.158.97.66 | 219.158.97.66 |  |  | 11.1% | 86 | 224 | 135 | 38.4 
| 8 | 219.158.98.174 | 219.158.98.174 |  |  | 0.0% | 242 | 356 | 303 | 39.0 
| 9 | 63.146.27.85 | sjp-brdr-04.inet.qwest.net |  |  | 11.1% | 263 | 510 | 345 | 85.3 
| 10 | 67.14.28.114 | dca2-edge-02.inet.qwest.net |  |  | 22.2% | 281 | 358 | 310 | 25.1 
| 11 | 65.126.19.90 | 65.126.19.90 |  |  | 0.0% | 283 | 345 | 316 | 23.4 
| 12 | 54.239.109.86 | 54.239.109.86 |  |  | 22.2% | 516 | 557 | 537 | 12.6 
| 13 | 54.239.111.99 | 54.239.111.99 |  |  | 33.3% | 533 | 599 | 563 | 21.3 
| 14 | 205.251.244.233 |  |  |  | 22.2% | 519 | 559 | 533 | 10.3 

**Upload Test**

首先是一个 24.1 MB 的压缩包文件（~~本子~~）

```
Outgoing
	Current transfer rate	390 bytes/s
	Average Transfer Rate	253 KB/s
	Maximum Transfer Rate	3.07 MB/s
Total
	Received	741 KB
	Sent	31.6 MB
	Total Data Transferred	32.3 MB
Since	12/4/2015 1:58:07 PM
Elapsed time: 00-02-08
```

然后是一个 130MB 的 VM disk file.

```
Outgoing
	Current transfer rate	1.17 MB/s
	Average Transfer Rate	1.13 MB/s
	Maximum Transfer Rate	2.88 MB/s
Total
	Received	2.22 MB
	Sent	138 MB
	Total Data Transferred	140 MB
Since	12/4/2015 2:06:57 PM
Elapsed time: 00-02-02
```

**Download Test**

Then download the 130 MB VM disk file.

```
Incoming
	Current transfer rate	14.6 KB/s
	Average Transfer Rate	18.1 KB/s
	Maximum Transfer Rate	46.0 KB/s
Total
	Received	10.6 MB
	Sent	475 KB
	Total Data Transferred	11.1 MB
Since	12/4/2015 2:27:20 PM
Elapsed time: 00-10-00
```

直连的下载速度过于感人，我实在没耐心等待它下载完便提前终止了下载任务，但我想这10分钟的数据足够反映一些情况了。

## Bandwagon-AM

**Bandwidth**

![4886154560.png](https://c.hime.io/images/GDl.png "Bandwagon-AM; Bandwidth: Download: 12.29 Mb/s; Upload 10.24 Mb/s; Ping: 201 ms")

**Traceroute**


|Hop| Host IP | Host Name | AS Name | AS | Loss % | Min Latency | Max Latency | Average Latency | StdDev
|---|---|---|---|---|---|---|---|---|---|
| 5 | 219.158.14.149 | 219.158.14.149 | CHINA169-Backbone CNCGROUP China169 Backbone | 4837 | 0.0% | 27 | 72 | 31 | 8.9
| 6 | 219.158.97.98 | 219.158.97.98 | CHINA169-Backbone CNCGROUP China169 Backbone | 4837 | 0.0% | 102 | 107 | 105 | 1.5
| 7 | 219.158.97.90 | 219.158.97.90 | CHINA169-Backbone CNCGROUP China169 Backbone | 4837 | 3.3% | 78 | 108 | 99 | 8.8
| 8 | 219.158.98.158 | 219.158.98.158 | CHINA169-Backbone CNCGROUP China169 Backbone | 4837 | 3.3% | 190 | 242 | 233 | 14.0
| 9 | 64.71.137.1 | 10ge13-11.core1.lax2.he.net | Hurricane Electric, Inc. | 6939 | 3.3% | 182 | 279 | 240 | 24.6
| 10 | 184.105.81.178 | 100ge4-1.core1.phx2.he.net | Hurricane Electric, Inc. | 6939 | 0.0% | 201 | 253 | 234 | 15.9
| 11 | 65.19.129.154 | it7-1-11.core1.phx2.he.net | Hurricane Electric, Inc. | 6939 | 13.3% | 198 | 270 | 237 | 25.7
| 12 | 198.35.46.5 | v36.sioru.com | All your base are belong to us | 25820 | 3.3% | 234 | 285 | 259 | 12.8


**Upload Test**

24.1 MB Zip file

```
Outgoing
	Current transfer rate	890 KB/s
	Average Transfer Rate	868 KB/s
	Maximum Transfer Rate	3.35 MB/s
Total
	Received	738 KB
	Sent	25.4 MB
	Total Data Transferred	26.2 MB
Since	12/4/2015 2:56:37 PM
Elapsed time: 00-00-30
```

130 MB VM disk file.

```
Outgoing
	Current transfer rate	1.34 MB/s
	Average Transfer Rate	0.96 MB/s
	Maximum Transfer Rate	3.01 MB/s
Total
	Received	3.12 MB
	Sent	138 MB
	Total Data Transferred	141 MB
Since	12/4/2015 3:32:42 PM
Elapsed time: 00-02-24
```

**Downliad Test**

154.6 MB for both of the two files

```
Incoming
	Current transfer rate	1.22 MB/s
	Average Transfer Rate	906 KB/s
	Maximum Transfer Rate	2.64 MB/s
Total
	Received	161 MB
	Sent	1.98 MB
	Total Data Transferred	163 MB
Since	12/4/2015 3:38:41 PM
Elapsed time: 00-03-02
```

## Linode-Tokyo

**Bandwidth**

![4886206352.png](https://c.hime.io/images/0Jq.png "Linode-Tokyo; Bandwidth: Download: 12.33 Mb/s; Upload 12.68 Mb/s; Ping: 154 ms")

**Traceroute**

|Hop| Host IP | Host Name | AS Name | AS | Loss % | Min Latency | Max Latency | Average Latency | StdDev
|---|---|---|---|---|---|---|---|---|---|
| 5 | 219.158.99.177 | 219.158.99.177 | CHINA169-Backbone CNCGROUP China169 Backbone | 4837 | 0.0% | 27 | 29 | 28 | 0.3
| 6 | 219.158.23.110 | 219.158.23.110 | CHINA169-Backbone CNCGROUP China169 Backbone | 4837 | 16.7% | 71 | 117 | 96 | 11.0
| 7 | 219.158.97.86 | 219.158.97.86 | CHINA169-Backbone CNCGROUP China169 Backbone | 4837 | 3.3% | 80 | 114 | 99 | 7.9
| 8 | 203.181.102.57 | 203.181.102.57 | KDDI CORPORATIONKDDI CORPORATION | 2516 | 0.0% | 126 | 155 | 139 | 6.0
| 9 | 106.187.3.29 | otejbb206.int-gw.kddi.ne.jp | KDDI CORPORATIONKDDI CORPORATION | 2516 | 0.0% | 117 | 161 | 128 | 9.3
| 10 | 124.215.194.165 | cm-fcu204.kddnet.ad.jp | KDDI CORPORATIONKDDI CORPORATION | 2516 | 0.0% | 104 | 147 | 130 | 9.9
| 11 | 124.215.199.170 | 124.215.199.170 |  |  | 3.3% | 67 | 140 | 103 | 24.0

**Upload Test**

24.1 MB Zip file

```
Outgoing
	Current transfer rate	1.54 MB/s
	Average Transfer Rate	1.33 MB/s
	Maximum Transfer Rate	3.17 MB/s
Total
	Received	538 KB
	Sent	23.9 MB
	Total Data Transferred	24.5 MB
Since	12/4/2015 4:07:58 PM
Elapsed time: 00-00-18
```

130 MB VM disk file

```
Outgoing
	Current transfer rate	1.29 MB/s
	Average Transfer Rate	1.47 MB/s
	Maximum Transfer Rate	3.14 MB/s
Total
	Received	3.52 MB
	Sent	139 MB
	Total Data Transferred	143 MB
Since	12/4/2015 4:09:45 PM
Elapsed time: 00-01-35
```

**Download Test**

154.6 MB for both of the two files

```
Incoming
	Current transfer rate	805 KB/s
	Average Transfer Rate	1.03 MB/s
	Maximum Transfer Rate	2.85 MB/s
Total
	Received	161 MB
	Sent	1.77 MB
	Total Data Transferred	163 MB
Since	12/4/2015 4:18:58 PM
Elapsed time: 00-02-37
```

# 安全性

桌面客户端和网页端的所有传入传出连接皆通过 `Hypertext Transfer Protocol over SSL/TSL (HTTPS)` 进行加密传输，相比于其他部分 P2P 传输工具来说更为安全可靠。

# 结论

目前从中国大陆直连美国 ACD 伺服器有较严重的丢包率，下载速度过于感人，上传则可以接受。在使用代理后，上传/下载速度都有了明显的改善，但是 VPS 的购入又是一份额外支出，所以还是看你自己觉得值不值了。笔者的建议是如果你有大量敏感数据需要安全的托管而且不经常读取，那么丢到 ACD 上很合适，上传速度不挂代理也足够用。但是如果经常从云盘读取小文档，那么笔者还是推荐用购入 Office 365 with 1T OneDrive。如果只是用来分享~~本子~~和专辑，那么还是用百度云吧，速度够快，客户端做的良心，默认 1T 免费容量也足够用。

另外 ACD 也有在中国大陆地区提供服务[\[4\]](#R4)，笔者将会在发文之后询问是否可以将美国的订阅转移至中国区，届时会在本文更新。

# 更新

**2015-12-08 18:05:13 更新**

从客服邮件获取的一些使用细节：

1. Amazon 没有任何权利去删除你存储的东西； 
2. 你可以保存版权物； 
3. 这个优惠只能买一年的； 
4. 订阅无法转移到大陆，毕竟你国； 
5. 订阅到期后有 30 天的缓冲期，这三十天内可以下载数据，但无法上传， 30 天后会删除数据。

**2016-02-22 20:36:58 更新**

对 Amazon Cloud Drive 的三个 Windows 客户端的评测：

**Amazon Cloud Drive Client for Windows**



**Onedrive**

>Sync keeps your computer synchronized with all your files in odrive. Every file from every link is in the odrive folder. Open, add, change and reorganize cloud files like regular files.

**Todo**
<a id="R5"></a>

* 在 *nix Platform 上使用 ACD
* 对比 AWS / ACD / OneDrive / 百度云 / 七牛 等主流云存储提供商
* 使用 ACD 实时备份监控录像

---

# Reference

<a id="R1">[1]</a> 本文开始撰写于 2015-11-27 23:18:45 (GMT+8)，但由于发现那段时间上海国际出口线路受到严重干扰，traceroute 自己的美国 VPS 丢包率超过 80%，所以暂时等待线路稳定后完成数据采集部分。截至发稿时 (2015-12-04 17:38:25 (GMT+8)) 此活动依然有效。

<a id="R2">[2]</a> [Amazon Cloud Drive: Cloud Storage - Online Backup](https://www.amazon.com/gp/drive/landing/everything/buy?ref_=cd_asin_ue_buy?tag=b0c55-20)

<a id="R3">[3]</a> Current exchange rate: 100 USD = 639.41 CNY (From Google Finanace)

<a id="R4">[4]</a> [Amazon Cloud Drive](http://www.amazon.cn/gp/feature.html?docId=192978)