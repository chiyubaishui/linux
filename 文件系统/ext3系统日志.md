ext3系统日志
	kjournald是ext3文件系统的日志进程，负责记录ext3文件系统的数据更新日志。
	ext3的日志有三种级别：
		1）journal：记录文件系统的文件数据和元素（metadata）的更新。
		2）ordered：只记录文件系统的元数据的更新日志，但是在元数据发生变更之前，把日志写入磁盘。ordered是ext3的默认日志级别。
		3）writeback：如果你了解raid卡的写入级别，那么也很容易理解这个writeback的含义。writeback级别下，同样只会记录metadata的更新日志。
		但是没有强制日志在metadata更新之前把数据写入到磁盘上，什么时候写入磁盘取决于标准文件系统（操作系统）进行flush脏页操作。
		
	ext3（kjournald）记录了大量的日志，导致iowait升高，而且日志需要强制写入到磁盘（pdflush进程）。
	从fstab文件可以看出，系统的日志级别为ordered，而且文件系统挂载使用的默认挂载参数，没有做任何优化。
	# cat /etc/fstab 
	LABEL=/ / ext3 defaults 1 1 LABEL=/boot /boot ext3 defaults 1 2

磁盘参数优化
磁盘的挂载参数进行优化，增加noatime选项（nodiratime可以不加）。noatime可以提高磁盘5%-10%的读写性能。
LABEL=/ / ext3 defaults,noatime 1