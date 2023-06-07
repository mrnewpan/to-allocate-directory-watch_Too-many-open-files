## To allocate directory watch: Too many open files
### Для Debian/Ubuntu

#### С помощью этой команды можно увидеть максимальное системное количество дескрипторов файлов
```
cat /proc/sys/fs/file-max
```
### Узнать, сколько файлов открыто
```
cat /proc/sys/fs/file-nr
```
### Максимальное количество файлов, которые может открыть один из ваших процессов
```
ulimit -n
```
### временно задать
```
ulimit -n 4096
```
### максимальное количество процессов, которые может иметь пользователь
```
ulimit -u
```
### текущие мягкие и жесткие ограничения
```
ulimit -Sn
ulimit -Hn
```
### пятнадцать самых активных пользователях файловых дескрипторов на вашем компьютере
```
lsof | awk '{ print $1 " " $2; }' | sort -rn | uniq -c | sort -rn | head -15
```
----
### Внесение постоянных изменений

/etc/pam.d/common-session
```
session required pam_limits.so
```

/etc/security/limits.conf
```
* hard nofile 65536
* soft nofile 200000
root hard nofile 65536
root soft nofile 200000
```
```
reboot
```
