## systemd

### 添加 systemd 开机启动项

	1. 配置 test.service:
		[Unit]
		Description=Test
		After=network.target
		
		[Service]
		Type=oneshot
		ExecStart=/opt/test.sh start
		ExecStop=/opt/test.sh stop
		TimeoutSec=0
		RemainAfterExit=yes
		SysVStartPriority=99
		
		[Install]
		WantedBy=multi-user.target
		
	2. cp test.service /usr/lib/systemd/system/
	
	3. ln -s /usr/lib/systemd/system/test.service /etc/systemd/system/multi-user.target.wants/test.service
	
	4. 配置 test.sh
		#!/bin/bash
		case $1 in
		"start")
			;;
		"stop")
			;;
		*)
			;;
		esac
		
	4. systemctl enable test.service
	5. systemctl start test.service
	6. systemctl status test.service
	7. systemctl stop test.service
	8. systemctl disable test.service
