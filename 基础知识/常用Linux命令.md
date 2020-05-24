后台启动：nohup command >X.file 2>&1 &
用tar打包时想剔除打包目录中的某个子目录或文件：tar -zcvf home.tar.gz   /home --exclude=/home/afish   --exclude=/home/www/afish.php
只打包指定目录下的文件：tar zcvf /tar/chao.tar.gz  -C /chao .
解压到指定目录中：tar zxvf test.tar.gz -C test
watch指令可以间歇性的执行程序：watch -n 10 'cat /proc/loadavg' 十秒一次输出系统的平均负载
列出谁在使用特定的tcp端口：lsof -i tcp:80
以服务器方式运行监听某个端口：nc -l 3306
确认是否存活:nc -vw 2 192.168.21.248 11111 
分割一个文件:split -5 a.txt