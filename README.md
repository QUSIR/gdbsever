# gdbsever  使用说明  在新塘N3292x平台下


##编译  gdbsever

./configure --target=arm-linux  --host=arm-linux 




arm-linux-gdb -v  查看版本


arm-linux-gdb版本要与gdbsever一致

##问题解决

error while loading shared libraries: libtinfo.so.5: cannot open shared object file: No such file or directory

	sudo ln -s /usr/lib/libncurses.so /usr/lib/libtinfo.so.5
	sudo ln -s /usr/lib/libtinfo.so.5 /usr/lib/libtinfo.so


##查看依赖项

ldd arm-linux-gdb

	linux-gate.so.1 =>  (0x006ea000)
	libncurses.so.5 => /lib/libncurses.so.5 (0x008d8000)
	libm.so.6 => /lib/tls/i686/cmov/libm.so.6 (0x00531000)
	libc.so.6 => /lib/tls/i686/cmov/libc.so.6 (0x00110000)
	libdl.so.2 => /lib/tls/i686/cmov/libdl.so.2 (0x00e4b000)
	/lib/ld-linux.so.2 (0x0027a000)

##开始调试

门口机

	./gdbserver 192.168.56.150:2345 amrnb-dec


linux系统上

	 arm-linux-gdb amrnb-dec
	
	(gdb) target remote 192.168.56.150:2345

##调试指令

	(gdb)list   or l
	(gdb)break func 
	(gdb)break 22
	(gdb)info br    
	(gdb)continue   or c    // 这里不能用 run
	(gdb)next   or n
	(gdb)print or p    result  
	(gdb) finish        // 跳出func函数
	(gdb) next
	(gdb) quit

这里要调试的程序得是交叉编译过的，并且加了-g参数。

	gcc gdb-sample.c -o gdb-sample -g

