---
title: 贴一个Amazon EC2的micro实例的benchmark
author: fluke
layout: post
permalink: /2013/02/%e8%b4%b4%e4%b8%80%e4%b8%aaamazon-ec2%e7%9a%84micro%e5%ae%9e%e4%be%8b%e7%9a%84benchmark/
categories:
  - 服务器维护
tags:
  - Amazon EC2
  - vps
  - 性能测试
--- 

性能比较烂，如果不需要考虑灵活横向扩展资源以及哪些专用基础设施的话，那建议还是上linode等知名的vps。

	make[1]: Leaving directory `/tmp/unixbench-5.1.2'
	
	sh: 1: 3dinfo: not found
	
	 
	
	   # # # # # # # ##### ###### # # #### # #
	
	   # # ## # # # # # # # ## # # # # #
	
	   # # # # # # ## ##### ##### # # # # ######
	
	   # # # # # # ## # # # # # # # # #
	
	   # # # ## # # # # # # # ## # # # #
	
	    #### # # # # # ##### ###### # # #### # #
	
	 
	
	   Version 5.1.2 Based on the Byte Magazine Unix Benchmark
	
	 
	
	   Multi-CPU version Version 5 revisions by Ian Smith,
	
	                                      Sunnyvale, CA, USA
	
	   December 22, 2007 johantheghost at yahoo period com
	
	 
	
	 
	
	1 x Dhrystone 2 using register variables 1 2 3 4 5 6 7 8 9 10
	
	 
	
	1 x Double-Precision Whetstone 1 2 3 4 5 6 7 8 9 10
	
	 
	
	1 x Execl Throughput 1 2 3
	
	 
	
	1 x File Copy 1024 bufsize 2000 maxblocks 1 2 3
	
	 
	
	1 x File Copy 256 bufsize 500 maxblocks 1 2 3
	
	 
	
	1 x File Copy 4096 bufsize 8000 maxblocks 1 2 3
	
	 
	
	1 x Pipe Throughput 1 2 3 4 5 6 7 8 9 10
	
	 
	
	1 x Pipe-based Context Switching 1 2 3 4 5 6 7 8 9 10
	
	 
	
	1 x Process Creation 1 2 3
	
	 
	
	1 x System Call Overhead 1 2 3 4 5 6 7 8 9 10
	
	 
	
	1 x Shell Scripts (1 concurrent) 1 2 3
	
	 
	
	1 x Shell Scripts (8 concurrent) 1 2 3
	
	 
	
	========================================================================
	
	   BYTE UNIX Benchmarks (Version 5.1.2)
	
	 
	
	   System: ip-10-158-198-5: GNU/Linux
	
	   OS: GNU/Linux — 3.2.0-31-virtual — #50-Ubuntu SMP Fri Sep 7 16:36:36 UTC 2012
	
	   Machine: x86\_64 (x86\_64)
	
	   Language: en_US.utf8 (charmap="UTF-8", collate="UTF-8")
	
	   CPU 0: Intel(R) Xeon(R) CPU E5645 @ 2.40GHz (3999.9 bogomips)
	
	          Hyper-Threading, x86-64, MMX, Physical Address Ext, SYSENTER/SYSEXIT, SYSCALL/SYSRET
	
	   15:00:57 up 19:22, 1 user, load average: 0.32, 0.11, 0.08; run level 2
	
	 
	
	————————————————————————
	
	Benchmark Run: Sat Feb 02 2013 15:00:57 – 15:31:12
	
	1 CPU in system; running 1 parallel copy of tests
	
	 
	
	Dhrystone 2 using register variables 9257467.2 lps (10.1 s, 7 samples)
	
	Double-Precision Whetstone 1412.6 MWIPS (17.2 s, 7 samples)
	
	Execl Throughput 424.3 lps (29.8 s, 2 samples)
	
	File Copy 1024 bufsize 2000 maxblocks 102253.8 KBps (30.1 s, 2 samples)
	
	File Copy 256 bufsize 500 maxblocks 21627.7 KBps (30.1 s, 2 samples)
	
	File Copy 4096 bufsize 8000 maxblocks 265826.1 KBps (30.1 s, 2 samples)
	
	Pipe Throughput 76852.8 lps (10.1 s, 7 samples)
	
	Pipe-based Context Switching 12908.4 lps (10.1 s, 7 samples)
	
	Process Creation 801.0 lps (30.1 s, 2 samples)
	
	Shell Scripts (1 concurrent) 595.0 lpm (60.3 s, 2 samples)
	
	Shell Scripts (8 concurrent) 60.8 lpm (61.2 s, 2 samples)
	
	System Call Overhead 58984.2 lps (10.1 s, 7 samples)
	
	 
	
	System Benchmarks Index Values BASELINE RESULT INDEX
	
	Dhrystone 2 using register variables 116700.0 9257467.2 793.3
	
	Double-Precision Whetstone 55.0 1412.6 256.8
	
	Execl Throughput 43.0 424.3 98.7
	
	File Copy 1024 bufsize 2000 maxblocks 3960.0 102253.8 258.2
	
	File Copy 256 bufsize 500 maxblocks 1655.0 21627.7 130.7
	
	File Copy 4096 bufsize 8000 maxblocks 5800.0 265826.1 458.3
	
	Pipe Throughput 12440.0 76852.8 61.8
	
	Pipe-based Context Switching 4000.0 12908.4 32.3
	
	Process Creation 126.0 801.0 63.6
	
	Shell Scripts (1 concurrent) 42.4 595.0 140.3
	
	Shell Scripts (8 concurrent) 6.0 60.8 101.3
	
	System Call Overhead 15000.0 58984.2 39.3
	
	                                                                   ========
	
	System Benchmarks Index Score 129.4
	
	 
	
	 
	
	 
	
	 
	
	======= Script description and score comparison: ======= 
	
	 
	
	http://www.ctohome.com/FuWuQi/c5/172.html
	
	 
	
	 
	
	ubuntu@ip-10-158-198-5:/tmp$ cat /proc/cpuinfo 
	
	processor : 0
	
	vendor_id : GenuineIntel
	
	cpu family : 6
	
	model : 44
	
	model name : Intel(R) Xeon(R) CPU E5645 @ 2.40GHz
	
	stepping : 2
	
	microcode : 0×13
	
	cpu MHz : 1999.976
	
	cache size : 12288 KB
	
	physical id : 0
	
	siblings : 1
	
	core id : 0
	
	cpu cores : 1
	
	apicid : 0
	
	initial apicid : 18
	
	fpu : yes
	
	fpu_exception : yes
	
	cpuid level : 11
	
	wp : yes
	
	flags : fpu de tsc msr pae cx8 sep cmov pat clflush mmx fxsr sse sse2 ss ht syscall nx lm constant\_	c up rep\_good nopl nonstop\_tsc pni pclmulqdq ssse3 cx16 pcid sse4\_1 sse4\_2 popcnt aes hypervisor 	hf\_lm
	
	bogomips : 3999.95
	
	clflush size : 64
	
	cache_alignment : 64
	
	address sizes : 40 bits physical, 48 bits virtual
	
	power management:
	
	 
	
	ubuntu@ip-10-158-198-5:/tmp$ free
	
	             total used free shared buffers cached
	
	Mem: 604376 522304 82072 0 29612 412976
	
	-/ buffers/cache: 79716 524660
	
	Swap: 0 0 0
	
	ubuntu@ip-10-158-198-5:/tmp$  
	  

另外作为对比，贴一下另外一个vps的：

	768M budgetvm xen
	
	 
	
	 
	
	# # # # # # # ##### ###### # # #### # #  
	# # ## # # # # # # # ## # # # # #  
	# # # # # # ## ##### ##### # # # # ######  
	# # # # # # ## # # # # # # # # #  
	# # # ## # # # # # # # ## # # # #  
	#### # # # # # ##### ###### # # #### # #
	
	Version 5.1.2 Based on the Byte Magazine Unix Benchmark
	
	Multi-CPU version Version 5 revisions by Ian Smith,  
	Sunnyvale, CA, USA  
	December 22, 2007 johantheghost at yahoo period com
	
	  
	1 x Dhrystone 2 using register variables 1 2 3 4 5 6 7 8 9 10
	
	1 x Double-Precision Whetstone 1 2 3 4 5 6 7 8 9 10
	
	1 x Execl Throughput 1 2 3
	
	1 x File Copy 1024 bufsize 2000 maxblocks 1 2 3
	
	1 x File Copy 256 bufsize 500 maxblocks 1 2 3
	
	1 x File Copy 4096 bufsize 8000 maxblocks 1 2 3
	
	1 x Pipe Throughput 1 2 3 4 5 6 7 8 9 10
	
	1 x Pipe-based Context Switching 1 2 3 4 5 6 7 8 9 10
	
	1 x Process Creation 1 2 3
	
	1 x System Call Overhead 1 2 3 4 5 6 7 8 9 10
	
	1 x Shell Scripts (1 concurrent) 1 2 3
	
	1 x Shell Scripts (8 concurrent) 1 2 3
	
	3 x Dhrystone 2 using register variables 1 2 3 4 5 6 7 8 9 10
	
	3 x Double-Precision Whetstone 1 2 3 4 5 6 7 8 9 10
	
	3 x Execl Throughput 1 2 3
	
	3 x File Copy 1024 bufsize 2000 maxblocks 1 2 3
	
	3 x File Copy 256 bufsize 500 maxblocks 1 2 3
	
	3 x File Copy 4096 bufsize 8000 maxblocks 1 2 3
	
	3 x Pipe Throughput 1 2 3 4 5 6 7 8 9 10
	
	3 x Pipe-based Context Switching 1 2 3 4 5 6 7 8 9 10
	
	3 x Process Creation 1 2 3
	
	3 x System Call Overhead 1 2 3 4 5 6 7 8 9 10
	
	3 x Shell Scripts (1 concurrent) 1 2 3
	
	3 x Shell Scripts (8 concurrent) 1 2 3
	
	========================================================================  
	BYTE UNIX Benchmarks (Version 5.1.2)
	
	System: syncapi.com: GNU/Linux  
	OS: GNU/Linux — 3.2.0-24-virtual — #37-Ubuntu SMP Wed Apr 25 12:51:49 UTC 2012  
	Machine: i686 (i386)  
	Language: en_US.utf8 (charmap="UTF-8", collate="UTF-8")  
	CPU 0: Intel(R) Xeon(R) CPU E5-2620 0 @ 2.00GHz (4000.1 bogomips)  
	Hyper-Threading, MMX, Physical Address Ext, SYSENTER/SYSEXIT  
	CPU 1: Intel(R) Xeon(R) CPU E5-2620 0 @ 2.00GHz (4000.1 bogomips)  
	Hyper-Threading, MMX, Physical Address Ext, SYSENTER/SYSEXIT  
	CPU 2: Intel(R) Xeon(R) CPU E5-2620 0 @ 2.00GHz (4000.1 bogomips)  
	Hyper-Threading, MMX, Physical Address Ext, SYSENTER/SYSEXIT  
	14:57:48 up 16 min, 1 user, load average: 0.05, 0.23, 0.17; runlevel 2
	
	————————————————————————  
	Benchmark Run: Mon Nov 26 2012 14:57:48 – 15:25:51  
	3 CPUs in system; running 1 parallel copy of tests
	
	Dhrystone 2 using register variables 9460536.2 lps (10.0 s, 7 samples)  
	Double-Precision Whetstone 1819.3 MWIPS (10.4 s, 7 samples)  
	Execl Throughput 446.6 lps (29.7 s, 2 samples)  
	File Copy 1024 bufsize 2000 maxblocks 166475.6 KBps (30.0 s, 2 samples)  
	File Copy 256 bufsize 500 maxblocks 49369.0 KBps (30.0 s, 2 samples)  
	File Copy 4096 bufsize 8000 maxblocks 495627.4 KBps (30.0 s, 2 samples)  
	Pipe Throughput 98511.1 lps (10.0 s, 7 samples)  
	Pipe-based Context Switching 8241.9 lps (10.0 s, 7 samples)  
	Process Creation 1081.0 lps (30.0 s, 2 samples)  
	Shell Scripts (1 concurrent) 1703.7 lpm (60.0 s, 2 samples)  
	Shell Scripts (8 concurrent) 428.5 lpm (60.1 s, 2 samples)  
	System Call Overhead 349054.2 lps (10.0 s, 7 samples)
	
	System Benchmarks Index Values BASELINE RESULT INDEX  
	Dhrystone 2 using register variables 116700.0 9460536.2 810.7  
	Double-Precision Whetstone 55.0 1819.3 330.8  
	Execl Throughput 43.0 446.6 103.8  
	File Copy 1024 bufsize 2000 maxblocks 3960.0 166475.6 420.4  
	File Copy 256 bufsize 500 maxblocks 1655.0 49369.0 298.3  
	File Copy 4096 bufsize 8000 maxblocks 5800.0 495627.4 854.5  
	Pipe Throughput 12440.0 98511.1 79.2  
	Pipe-based Context Switching 4000.0 8241.9 20.6  
	Process Creation 126.0 1081.0 85.8  
	Shell Scripts (1 concurrent) 42.4 1703.7 401.8  
	Shell Scripts (8 concurrent) 6.0 428.5 714.2  
	System Call Overhead 15000.0 349054.2 232.7  
	========  
	System Benchmarks Index Score 234.7
	
	————————————————————————  
	Benchmark Run: Mon Nov 26 2012 15:25:51 – 15:54:07  
	3 CPUs in system; running 3 parallel copies of tests
	
	Dhrystone 2 using register variables 24001583.7 lps (10.0 s, 7 samples)  
	Double-Precision Whetstone 4815.2 MWIPS (11.1 s, 7 samples)  
	Execl Throughput 1435.9 lps (29.9 s, 2 samples)  
	File Copy 1024 bufsize 2000 maxblocks 250817.5 KBps (30.0 s, 2 samples)  
	File Copy 256 bufsize 500 maxblocks 69379.3 KBps (30.0 s, 2 samples)  
	File Copy 4096 bufsize 8000 maxblocks 749753.0 KBps (30.0 s, 2 samples)  
	Pipe Throughput 609289.2 lps (10.0 s, 7 samples)  
	Pipe-based Context Switching 68117.4 lps (10.0 s, 7 samples)  
	Process Creation 2632.3 lps (30.0 s, 2 samples)  
	Shell Scripts (1 concurrent) 2829.5 lpm (60.1 s, 2 samples)  
	Shell Scripts (8 concurrent) 443.4 lpm (60.2 s, 2 samples)  
	System Call Overhead 879496.8 lps (10.0 s, 7 samples)
	
	System Benchmarks Index Values BASELINE RESULT INDEX  
	Dhrystone 2 using register variables 116700.0 24001583.7 2056.7  
	Double-Precision Whetstone 55.0 4815.2 875.5  
	Execl Throughput 43.0 1435.9 333.9  
	File Copy 1024 bufsize 2000 maxblocks 3960.0 250817.5 633.4  
	File Copy 256 bufsize 500 maxblocks 1655.0 69379.3 419.2  
	File Copy 4096 bufsize 8000 maxblocks 5800.0 749753.0 1292.7  
	Pipe Throughput 12440.0 609289.2 489.8  
	Pipe-based Context Switching 4000.0 68117.4 170.3  
	Process Creation 126.0 2632.3 208.9  
	Shell Scripts (1 concurrent) 42.4 2829.5 667.3  
	Shell Scripts (8 concurrent) 6.0 443.4 739.0  
	System Call Overhead 15000.0 879496.8 586.3  
	========  
	System Benchmarks Index Score 564.2
	
	 
	
	  
	======= Script description and score comparison: =======
	
	http://www.ctohome.com/FuWuQi/c5/172.html
	
	  
	root@syncapi:/tmp#

