# !! 注意
BBR v3 不可用
## 支持的平台
	1. OS 操作系统
		1. Debian 10+
		2. Ubuntu 20.04+
	
	2. CPU 类型
		1. x86_64
		2. ARM64
## 可选功能
###### 1. 盒子环境
	1. qBittorrent   qb下载器
	2. autobrr       外站常用
	3. vertex       VT刷流
	4. autoremove-torrents   自动删种,外站常用

###### 2. 系统优化
	CPU Optimization 处理器优化
	Network Optimization 网络优化
	Kernel Values 内核参数调整
	Drive Optimization 硬盘优化
	BBRv3 or BBRx 开启BBRv3或者BBRx
 ### 一些进阶操作优化等等
- The Cache size should be set to around 1/4 of the machine total available ram. In case you opt for qBittorrent 4.3.x, you need to take account into memory leakage and set it to 1/8. 

- aio_threads default setting is 4 and should be good for HDD. For SSD or even NVMe server, you might consider increase it to 8 or even 16. 
	- For qBittorrent 4.3.x - 4.6.x you can change it in the advance setting tab. 
	- For qBittorrent 4.1.x, you can set it in /home/$username/.config/qBittorrent/qBittorrent.conf by adding `Session\AsyncIOThreadsCount=8` under [BitTorrent] section
		- Please shut down qBittorrent before the editing
	- For Deluge, you can install [ltconfig](https://github.com/ratanakvlun/deluge-ltconfig/releases/tag/v0.3.1) and edit through the plugins
		- aio_threads=8

- send_buffer_low_watermark, send_buffer_watermark & send_buffer_watermark_factor can be set to a lower value if you are running on a machine with poor I/O.
	- For qBittorrent 4.3.x you can change it in the advance setting tab. 
	- For qBittorrent 4.1.x, you can set it in /home/$username/.config/qBittorrent/qBittorrent.conf by adding `Session\SendBufferWatermark=5120`,`Session\SendBufferLowWatermark=1024`and`Session\SendBufferWatermarkFactor=150` under [BitTorrent] section
		- Please shut down qBittorrent before the editing
	- For Deluge, you can install [ltconfig](https://github.com/ratanakvlun/deluge-ltconfig/releases/tag/v0.3.1) and edit through the plugins
		- send_buffer_low_watermark=1048576
		- send_buffer_watermark=5242880
		- send_buffer_watermark_factor=150
  - 
- tick_internal default setting is 100 which can be too high for some weaker CPU. Consider changing it to 250 or 500.
	- Sadly there is no way to change this setting in qBittorrent
	- For Deluge, you can install [ltconfig](https://github.com/ratanakvlun/deluge-ltconfig/releases/tag/v0.3.1) and edit through the plugins
		- tick_interval=250
- A little bit more fine tunning notes can also be found in /etc/sysctl.conf

- For file system, I highly recommend using XFS 

Deluge Password Set - https://github.com/amefs/quickbox-lite

autoremove-torrents - https://github.com/jerrymakesjelly/autoremove-torrents

BBR Install - https://github.com/KozakaiAya/TCP_BBR

# 种子箱安装脚本
## 举例
`bash <(wget -qO- https://raw.githubusercontent.com/chinayxc/Dedicated-Seedbox/main/Install.sh) -u <username> -p <password> -c <缓存大小(unit:MiB最低1,之后安装完成建议调成-1)> -q <qBittorrent版本> -l <libtorrent版本> -b -v -r -3 -x -o`
#### 选项
	1. -u: username
	2. -p: password
	3. -c: Cache size for torrent client
	4. -q: qBittorrent versions
	5. -l: libtorrent versions
	6. -b: Install autobrr    
	7. -v: Install vertex     
	8. -r: Install autoremove-torrents  
	9. -3: Enable BBR V3    
	10.-x: Enable BBRx      
	11. Customize ports     
##### 变量含义解释
	1. username is sgws       #####用户名sgws
	2. password is sgws6036   #####密码sgws6036
	3. Cache size is 1         #####缓存为1M
	4. Install qBittorrent 4.3.8 - libtorrent-v1.2.19   #####QB版本为14.3.8 内置LIB版本-v1.2.19 
	5. Install autobrr    #####安装autobbr
	6. Install autoremove-torrents  #####安装自动删种工具,外站常用
	7. Enable BBRx   #####开启BBRx
        8. -o    #####自定义端口
 ##### 直接复制下方,即可食用
 ##### 
 bash <(wget -qO- https://raw.githubusercontent.com/chinayxc/Dedicated-Seedbox/main/Install.sh) -u sgws -p sgws6036 -c 1 -q 4.3.8 -l v1.2.19 -x -o 18080     
 ##
 你可以用这个默认的,用户名sgws,密码sgws6036，端口18080，QB版本为4.3.8,安装好了可以自行去设置调整，可以开刷了
