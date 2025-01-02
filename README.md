[中文Readme](https://github.com/jerry048/Dedicated-Seedbox/blob/main/README-zh.md)
# !! ALERT
BBR v3 is currently unavailable
## Supported Platform
	1. OS
		1. Debian 10+
		2. Ubuntu 20.04+
	
	2. CPU Architecture
		1. x86_64
		2. ARM64
## Functions
###### 1. Seedbox Environment
	1. qBittorrent
	2. autobrr
	3. vertex
	4. autoremove-torrents

###### 2. System Tunning
	CPU Optimization
	Network Optimization
	Kernel Values
	Drive Optimization
	BBRv3 or BBRx
 ### Fine Tunning Note
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

# Seedbox Installation Script
## Usage
`bash <(wget -qO- https://raw.githubusercontent.com/jerry048/Dedicated-Seedbox/main/Install.sh) -u <自定义用户名> -p <自定义密码> -c <缓存大小(unit:MiB最低1,之后安装完成建议调成-1)> -q <qBittorrent版本> -l <libtorrent版本> -b -v -r -3 -x -o`
#### Options
	1. -u: username 用户名
	2. -p: password 密码
	3. -c: Cache size for torrent client  缓存大小
	4. -q: qBittorrent versions  qb版本
	5. -l: libtorrent versions    lib版本
	6. -b: Install autobrr    安装autobrr
	7. -v: Install vertex     安装vertex
	8. -r: Install autoremove-torrents  安装autoremove-torrents自动删种
	9. -3: Enable BBR V3    安装BBR V3暂时不要加貌似失效了
	10.-x: Enable BBRx      安装BBRx
	11. Customize ports     自定义端口 不加就是默认8080
##### Explanation
	1. username is sgws
	2. password is sgws6036
	3. Cache size is 1
	4. Install qBittorrent 4.3.8 - libtorrent-v1.2.19
	5. Install autobrr
	6. Install autoremove-torrents
	7. Enable BBRx
 #### Example
`bash <(wget -qO- https://raw.githubusercontent.com/chinayxc/Dedicated-Seedbox/main/Install.sh) -u sgws -p sgws6036 -c 1 -q 4.3.8 -l v1.2.19 -x -o 18080`
       你可以用这个默认的,用户名sgws,密码sgws6036，端口18080，QB版本为4.3.8
