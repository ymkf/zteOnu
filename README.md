# zteOnu
Type `./zteonu -h` for help
# 备用

` zteonu -u CUAdmin -p CUAdmin --port 80 `

—开永久telnet—

` sendcmd 1 DB p TelnetCfg `

` sendcmd 1 DB set TelnetCfg 0 Lan_Enable 1 `

` sendcmd 1 DB set TelnetCfg 0 TS_UName 用户名 `

` sendcmd 1 DB set TelnetCfg 0 TSLan_UName 用户名 `

` sendcmd 1 DB set TelnetCfg 0 TS_UPwd 密码 `

` sendcmd 1 DB set TelnetCfg 0 TSLan_UPwd 密码 `

` sendcmd 1 DB set TelnetCfg 0 Max_Con_Num 99 `

` sendcmd 1 DB set TelnetCfg 0 ExitTime 999999 `

` sendcmd 1 DB set TelnetCfg 0 InitSecLvl 3 `

` sendcmd 1 DB set TelnetCfg 0 CloseServerTime 9999999 `

` sendcmd 1 DB set TelnetCfg 0 Lan_EnableAfterOlt 1 `

` sendcmd 1 DB save `

` killall telnetd `



—备份mtd0分区–

` dd if=/dev/mtd0 of=/mnt/U盘目录名/f7607p.bin `

或

` cat /dev/mtd0 > /mnt/U盘目录名/f7607p.bin `



—删除Wi-Fi前缀—

` sendcmd 1 DB set WLANCfg 0 ESSIDPrefix ` 设置2.4G的ssid前缀为空

` sendcmd 1 DB set WLANCfg 4 ESSIDPrefix ` 设置5G的ssid前缀为空

` sendcmd 1 DB save `



—切换区域—

` cat /etc/init.d/regioncode ` 查看区域号码

` upgradetest sdefconf 区域号码 `



—修改超密—

` sendcmd 1 DB set DevAuthInfo 0 User 新用户名 `

` sendcmd 1 DB set DevAuthInfo 0 Pass 新密码 `



—修改ponmac—

` setmac 1 32769 MAC地址 `



—删除电信远程控制—

` sendcmd 1 DB p MgtServer ` 查看当前的电信远程控制

` sendcmd 1 DB set MgtServer 0 URL http://127.0.0.1 ` 把服务器 URL 改掉

` sendcmd 1 DB set MgtServer 0 Tr069Enable 0 ` 禁用TR069远程控制

` sendcmd 1 DB save `



—关闭下行GPON光口和WiFi—

` ip link set mini-olt down `

` rmmod optical `

` rmmod mtlk `

` rmmod mtlkroot `



—手动欺骗ITMS注册结果—

` sendcmd 1 DB set PDTCTUSERINFO 0 Status 0 `

` sendcmd 1 DB set PDTCTUSERINFO 0 Result 1 `

` sendcmd 1 DB save `



—查看信息—

` setmac show2 ` 查看系统参数

` cat /proc/capability/boardinfo ` 查看配置信息

` cat /proc/cpuusage ` 查看CPU占用率

` cat /proc/tempsensor ` 查看温度



—user提权—

` sendcmd 1 DB set DevAuthInfo 1 Level 1 `

` sendcmd 1 DB save `



—配置连接数相关—

` sendcmd 1 DB p FWBase ` 查看连接数设置信息

` sendcmd 1 DB set FWBase 0 FwConnMaxEnable 0 ` 禁用连接数限制

` sendcmd 1 DB set FWBase 0 FwConntrackMax 65535 ` 设置最大连接数到65535(默认4000)

` sendcmd 1 DB set FWBase 0 ConntrackMax 65535 ` 设置单用户最大连接数到65535(默认3000)

` sendcmd 1 DB set FWLevel 0 Level 0 ` 关闭防火墙


—修改用户限制—
` sendcmd 1 DB p CltLmt `

` sendcmd 1 DB set CltLmt 8 Max 20 ` 修改最大用户数为20，可以改成其他数目，最大数目不超过255

` sendcmd 1 DB set CltLmt 8 Enable 0 `

` sendcmd 1 DB save `



—关闭开启指示灯—
` sendcmd 1 DB p WLCInfo ` 查看

` sendcmd 1 DB set WLCInfo 0 WLCStatus 1 ` 关闭

` sendcmd 1 DB set WLCInfo 0 WLCStatus 0 ` 开启

` sendcmd 1 DB save ` 保存

` reboot ` 重启生效