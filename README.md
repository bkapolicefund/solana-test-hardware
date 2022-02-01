# solana

##########################################################################
SOLANA TEST HARDWARE 
##########################################################################

INSTALL TESTS

    apt install slurm iotop htop iftop speedtest tcptrack hddtemp lm-sensors

INSTALL TURBO CONTROL - AND PLEASE RESEARCH HOW TO FULLY UTILIZE AS AMD IS 
                        DIFFERENT COMMANDS AND APPS FROM INTEL CPU TURBOING

    apt-get install indicator-cpufreq acpi-support acpid acpi

TO START TURBO CONTROL UP THE FIRST TIME, RUN THE FOLLOWING COMMAND AND THEN IT STARTS ITSELF NEXT BOOTS:

    indicator-cpufreq &

YOU SHOULD STILL BE ABLE TO CHANGE THE TURBO GOVERNOR WHEN YOU ARE USING INTEL_PSTATE BY RUNNING:

    cpupower frequency-set -g performance
    cpupower frequency-set --max 4600000
    cpupower frequency-set --freq 4600000

TEST TURBO WAY 1

    grep MHz /proc/cpuinfo
    
TEST DISPLAYS
    
    cpu MHz		: 4699.250
    cpu MHz		: 4699.444
    cpu MHz		: 4698.486
    cpu MHz		: 4698.977 ...

TEST TURBO WAY 2

    turbostat --debug sleep 10

TURBOSTAT DISPLAYS

    turbostat version 19.08.31 - Len Brown <lenb@kernel.org>
    cpu 0 pkg 0 die 0 node 0 lnode 0 core 0 thread 0
    cpu 1 pkg 0 die 0 node 0 lnode 0 core 1 thread 0
    cpu 2 pkg 0 die 0 node 0 lnode 0 core 2 thread 0
    cpu 3 pkg 0 die 0 node 0 lnode 0 core 3 thread 0
    cpu 4 pkg 0 die 0 node 0 lnode 0 core 4 thread 0
    cpu 5 pkg 0 die 0 node 0 lnode 0 core 5 thread 0 ...
    CPUID(0): AuthenticAMD 0x10 CPUID levels; 0x80000023 xlevels; family:model:stepping 0x19:21:0 (25:33:0)
    CPUID(1): SSE3 MONITOR - - - TSC MSR - HT -
    CPUID(6): APERF, No-TURBO, No-DTS, No-PTM, No-HWP, No-HWPnotify, No-HWPwindow, No-HWPepp, No-HWPpkg, No-EPB
    CPUID(7): No-SGX
    cpu2: POLL: CPUIDLE CORE POLL IDLE
    cpu2: C1: ACPI FFH MWAIT 0x0
    cpu2: C2: ACPI IOPORT 0x414
    cpu2: cpufreq driver: acpi-cpufreq
    cpu2: cpufreq governor: ondemand
    cpufreq boost: 1
    10.003506 sec
    usec	Time_Of_Day_Seconds	Core	CPU	APIC	X2APIC	Avg_MHz	Busy%	Bzy_MHz	TSC_MHz	IRQ	POLL	C1	C2	POLL%	C1%	C2%
    2006	1643720006.332280	-	-	-	-	2040	56.34	3620	3394	1463085	16040	288049	530638	0.01	7.47	36.49
    83	1643720006.330357	0	0	0	0	4003	100.00	4003	3394	39693	0	0	0	0.00	0.00	0.00
    43	1643720006.330411	0	16	1	1	1760	44.66	3940	3394	39885	654	11937	18824	0.02	11.17	44.45
    62	1643720006.330483	1	1	2	2	2078	58.32	3562	3394	38909	373	7870	14448	0.01	6.39	35.57
    57	1643720006.330553	1	17	3	3	1798	49.97	3599	3394	43297	198	10743	19193	0.01	9.37	41.02
    65	1643720006.330629	2	2	4	4	2001	56.10	3566	3394	39569	312	8000	15238	0.01	7.16	37.03 ...   
    
RUN TEMP CHECK 

    sensors
        
CHECK GPU USAGE

    nvidia-smi

CHECK MEMORY
    
    free    
    
LATENCY TESTS
        
FIRST IS PING
    
    46.4.32.165
    144.76.29.181
    65.108.79.154
    
THAT IS 2 FALKENSTEIN AND ONE HETZNER IN FINLAND SO LETS SEE THE NUMBERS U GET. I GET THIS FROM MOSCOW:
    
    64 bytes from 46.4.32.165: icmp_seq=1 ttl=58 time=39.7 ms
    64 bytes from 144.76.29.181: icmp_seq=1 ttl=58 time=40.0 ms
    64 bytes from 65.108.79.154: icmp_seq=1 ttl=58 time=34.9 ms    
    
CHECK LATENCY AND ETHERNET

    tcptrack -i eno1

CHECK CPU THREAD SPEEDS

    htop
    
CHECK DISK WRITE SPEEDS
    
    iotop
    
    slurm

CHECK NIC SPEEDS

    iftop
    
CHECK BANDWIDTH

    apt install speedtest
            
CHECK DISK SPEED AS IT MUST BE 700 MBYTES/SEC MINIMUM READ AND WRITING
AND BE SURE ITS RUNNING ON THE NVMe LEDGER DRIVE, NOT THE SSD OS DRIVE

    1 GB WRITES    
    fio --name=randwrite --ioengine=libaio --iodepth=1 --rw=randrw --bs=4m --direct=0 --size=1G --numjobs=4 --runtime=60 --group_reporting | egrep '(IOPS|READ|WRITE)'
    
CHECK DISK ARCHITECTURE

    lsblk
    
DISK INFO

    lshw -class disk  

    hwinfo --disk
    
QUERY SYSTEM LOG FOR ABNORMALITIES INSIDE OF

    journalctl | less
