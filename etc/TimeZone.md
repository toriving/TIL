# TimeZone.md

## time zone 확인
```shell script
$ more /etc/timezone
```

## time zone 변경
```shell script
$ sudo dpkg-reconfigure tzdata
```

## 시간 동기화
```shell script
$ sudo apt install rdate

$ sudo rdate time.bora.net
```
## 주기적 자동 동기화
```shell script
$ vi /etc/crontab

0 5 * * * root sduo /usr/bin/rdate -s time.bora.net && sudo /sbin/hwclock -w
```
## 부팅시 동기화
```shell script
$ vi /etc/rc.d/rc.local

#!/bin/sh 
# date sync 
sudo /usr/bin/rdate -s time.bora.net 
sudo /sbin/hwclock -w
```
