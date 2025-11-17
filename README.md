Imagens esp-hosted e linux xtensa para o ESP32-S3

Images generated with this HOWTO:
```
https://github.com/hpsaturn/esp32s3-linux
```

## Para gravar as imagens
```
 esptool.py --chip esp32s3 -p /dev/ttyUSB0 -b 2000000 --before=default_reset \
	--after=hard_reset write_flash --flash_mode dio --flash_freq 80m --flash_size 8MB \
	0x0     bootloader.bin \
	0x10000 network_adapter.bin \
	0x8000  partition-table.bin

 parttool.py -b 2000000 write_partition --partition-name linux  --input xipImage

 parttool.py -b 2000000 write_partition --partition-name rootfs --input rootfs.cramfs

 parttool.py -b 2000000 write_partition --partition-name etc --input etc.jffs2
```
## Saida
```
linux ptr = 0x42120000
vectors ptr = 0x4037c000
[    0.000000] Linux version 6.11.0 (gabriel@288300a9b387) (xtensa-esp32s3-linux-uclibcfdpic-gcc (crosstool-NG 1.25.0.183_bec302a) 14.1.0, GNU ld (crosstool-NG 1.25.0.183_bec302a) 2.42.50.20240224) #1 PREEMPT Sun Nov 16 22:43:15 UTC 2025
[    0.000000] config ID: c2f0fffe:23090f1f
[    0.000000] earlycon: esp32s3uart0 at MMIO32 0x60000000 (options '115200n8,40000000')
[    0.000000] printk: legacy bootconsole [esp32s3uart0] enabled
[    0.000000] **********************************************************
[    0.000000] **   NOTICE NOTICE NOTICE NOTICE NOTICE NOTICE NOTICE   **
[    0.000000] **                                                      **
[    0.000000] ** This system shows unhashed kernel memory addresses   **
[    0.000000] ** via the console, logs, and other interfaces. This    **
[    0.000000] ** might reduce the security of your system.            **
[    0.000000] **                                                      **
[    0.000000] ** If you see this message and you are not debugging    **
[    0.000000] ** the kernel, report this immediately to your system   **
[    0.000000] ** administrator!                                       **
[    0.000000] **                                                      **
[    0.000000] **   NOTICE NOTICE NOTICE NOTICE NOTICE NOTICE NOTICE   **
[    0.000000] **********************************************************
[    0.000000] Zone ranges:
[    0.000000]   Normal   [mem 0x000000003d800000-0x000000003dffffff]
[    0.000000] Movable zone start for each node
[    0.000000] Early memory node ranges
[    0.000000]   node   0: [mem 0x000000003d800000-0x000000003dffffff]
[    0.000000] Initmem setup node 0 [mem 0x000000003d800000-0x000000003dffffff]
[    0.000000] pcpu-alloc: s0 r0 d32768 u32768 alloc=1*32768
[    0.000000] pcpu-alloc: [0] 0
[    0.000000] Kernel command line: earlycon=esp32s3uart,mmio32,0x60000000,115200n8,40000000 console=ttyS0,115200n8 debug rw root=mtd:rootfs no_hash_pointers
[    0.000000] Dentry cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.000000] Inode-cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.000000] Built 1 zonelists, mobility grouping off.  Total pages: 2048
[    0.000000] mem auto-init: stack:off, heap alloc:off, heap free:off
[    0.000000] virtual kernel memory layout:
[    0.000000]     lowmem  : 0x3d800000 - 0x3e000000  (    8 MB)
[    0.000000]     .text   : 0x42120000 - 0x42380738  ( 2433 kB)
[    0.000000]     .rodata : 0x42381000 - 0x423e7000  (  408 kB)
[    0.000000]     .data   : 0x3d800000 - 0x3d87e440  (  505 kB)
[    0.000000]     .init   : 0x3d87e440 - 0x3d882a68  (   17 kB)
[    0.000000]     .bss    : 0x3d882a68 - 0x3d8ba948  (  223 kB)
[    0.000000] SLUB: HWalign=16, Order=0-3, MinObjects=0, CPUs=1, Nodes=1
[    0.000000] rcu: Preemptible hierarchical RCU implementation.
[    0.000000] rcu: RCU calculated value of scheduler-enlistment delay is 10 jiffies.
[    0.000000] NR_IRQS: 33
[    0.000000] rcu: srcu_init: Setting srcu_struct sizes based on contention.
[    0.000000] Calibrating CPU frequency 240.00 MHz
[    0.000000] clocksource: ccount: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 7963585194 ns
[    0.000067] sched_clock: 32 bits at 240MHz, resolution 4ns, wraps every 8947848189ns
[    0.009380] Calibrating delay loop (skipped)... 240.00 BogoMIPS preset
[    0.013401] pid_max: default: 32768 minimum: 301
[    0.021198] Mount-cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.025540] Mountpoint-cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.082945] rcu: Hierarchical SRCU implementation.
[    0.083679] rcu:     Max phase no-delay instances is 1000.
[    0.095490] Memory: 7008K/8192K available (2433K kernel code, 505K rwdata, 408K rodata, 98K init, 223K bss, 884K reserved, 0K cma-reserved)
[    0.106868] devtmpfs: initialized
[    0.145676] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604462750000 ns
[    0.146961] futex hash table entries: 256 (order: -1, 3072 bytes, linear)
[    0.154069] pinctrl core: initialized pinctrl subsystem
[    0.169395] NET: Registered PF_NETLINK/PF_ROUTE protocol family
[    0.253921] platform soc: Fixed dependency cycle(s) with /soc/intc@600c2000
[    0.400235] platform soc: Fixed dependency cycle(s) with /soc/intc@600c2000
[    0.462718] clocksource: Switched to clocksource ccount
[    0.522491] NET: Registered PF_INET protocol family
[    0.529967] IP idents hash table entries: 2048 (order: 2, 16384 bytes, linear)
[    0.551391] tcp_listen_portaddr_hash hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.555716] Table-perturb hash table entries: 65536 (order: 6, 262144 bytes, linear)
[    0.557673] TCP established hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.566213] TCP bind hash table entries: 1024 (order: 1, 8192 bytes, linear)
[    0.572256] TCP: Hash tables configured (established 1024 bind 1024)
[    0.581046] UDP hash table entries: 256 (order: 0, 4096 bytes, linear)
[    0.586281] UDP-Lite hash table entries: 256 (order: 0, 4096 bytes, linear)
[    0.596615] NET: Registered PF_UNIX/PF_LOCAL protocol family
[    0.610613] RPC: Registered named UNIX socket transport module.
[    0.611391] RPC: Registered udp transport module.
[    0.611680] RPC: Registered tcp transport module.
[    0.616491] RPC: Registered tcp-with-tls transport module.
[    0.620960] RPC: Registered tcp NFSv4.1 backchannel transport module.
[    0.686472] Initialise system trusted keyrings
[    0.690947] workingset: timestamp_bits=30 max_order=11 bucket_order=0
[    0.701848] NFS: Registering the id_resolver key type
[    0.704571] Key type id_resolver registered
[    0.705342] Key type id_legacy registered
[    0.707185] jffs2: version 2.2. (NAND) © 2001-2006 Red Hat, Inc.
[    0.713935] Key type asymmetric registered
[    0.715818] Asymmetric key parser 'x509' registered
[    0.721966] io scheduler mq-deadline registered
[    0.725320] io scheduler kyber registered
[    0.791349] pinctrl-single 60004154.gpio_in_mux: 256 pins, size 1024
[    0.804523] pinctrl-single 60008484.pinctrl: 22 pins, size 88
[    0.816382] pinctrl-single 60009004.pinctrl: 49 pins, size 196
[    3.261506] printk: legacy console [ttyS0] enabled
[    3.261506] printk: legacy console [ttyS0] enabled
[    3.262416] printk: legacy bootconsole [esp32s3uart0] disabled
[    3.262416] printk: legacy bootconsole [esp32s3uart0] disabled
[    3.321548] 60038000.acm: ttyGS3 at MMIO 0x60038000 (irq = 3, base_baud = 0) is a ESP32S3 ACM
[    3.345546] random: crng init done
[    3.400994] physmap-flash 42000000.flash: physmap platform flash device: [mem 0x42000000-0x42ffffff]
[    3.412350] 6 esp32 partitions found on MTD device 42000000.flash
[    3.414795] Creating 6 MTD partitions on "42000000.flash":
[    3.415585] 0x00000000a000-0x00000000f000 : "nvs"
[    3.419763] mtd: partition "nvs" doesn't start on an erase/write block boundary -- force read-only
[    3.466409] 0x00000000f000-0x000000010000 : "phy_init"
[    3.467191] mtd: partition "phy_init" doesn't start on an erase/write block boundary -- force read-only
[    3.504931] 0x000000010000-0x0000000b0000 : "factory"
[    3.539070] 0x0000000b0000-0x000000120000 : "etc"
[    3.574434] 0x000000120000-0x000000480000 : "linux"
[    3.608046] 0x000000480000-0x000000800000 : "rootfs"
[    3.680718] i2c_dev: i2c /dev entries driver
[    3.685704] Chipset=ESP32-S3 ID=09 detected over shmem IPC
[    3.735967] NET: Registered PF_INET6 protocol family
[    3.814159] Segment Routing with IPv6
[    3.815941] In-situ OAM (IOAM) with IPv6
[    3.819951] sit: IPv6, IPv4 and MPLS over IPv4 tunneling driver
[    3.843833] NET: Registered PF_PACKET protocol family
[    3.845185] Key type dns_resolver registered
[    4.062115] Loading compiled-in X.509 certificates
[    4.156782] i2c-gpio i2c0: using lines 582 (SDA) and 583 (SCL)
[    4.166439] cfg80211: Loading compiled-in X.509 certificates for regulatory database
[    4.196550] Loaded X.509 cert 'sforshee: 00b28ddf47aef9cea7'
[    4.219312] Loaded X.509 cert 'wens: 61c038651aabdcf94bd0ac7ff06c7248db18c600'
[    4.226244] platform regulatory.0: Direct firmware load for regulatory.db failed with error -2
[    4.227262] cfg80211: failed to load regulatory.db
[    4.230599] clk: Disabling unused clocks
[    4.246592] cramfs: checking physical address 0x42480000 for linear cramfs image
[    4.247510] cramfs: linear cramfs image on mtd:rootfs appears to be 3284 KB in size
[    4.252532] VFS: Mounted root (cramfs filesystem) readonly on device 31:5.
[    4.260061] devtmpfs: mounted
[    4.262384] Freeing unused kernel image (initmem) memory: 12K
[    4.266863] This architecture does not have kernel memory protection.
[    4.274653] Run /sbin/init as init process
[    4.277327]   with arguments:
[    4.280242]     /sbin/init
[    4.283982]   with environment:
[    4.286091]     HOME=/
[    4.288403]     TERM=linux
Starting syslogd: OK
Starting klogd: OK
Running sysctl: OK
Successfully initialized wpa_supplicant
Starting network: OK
Starting inetd: OK
Starting crond: OK

Welcome to Buildroot
buildroot login: root
~ # cat /proc/cpuinfo
CPU count       : 1
CPU list        : 0
vendor_id       : Tensilica
model           : Xtensa LX7.0.12
core ID         : LX7_ESP32_S3_MP
build ID        : 0x90f1f
config ID       : c2f0fffe:23090f1f
byte order      : little
cpu MHz         : 240.00
bogomips        : 480.00
flags           : nmi debug ocd trax perf density boolean loop nsa minmax sext clamps mac16 mul16 mul32 mul32h fpu s32c1i
physical aregs  : 64
misc regs       : 4
ibreak          : 2
dbreak          : 2
perf counters   : 2
num ints        : 32
ext ints        : 26
int levels      : 6
timers          : 3
debug level     : 6
icache line size: 4
icache ways     : 1
icache size     : 0
icache flags    :
dcache line size: 16
dcache ways     : 1
dcache size     : 0
dcache flags    :
load/store exceptions   : 4811284
load/store clock count  : 552213856
~ #
```

## Compilando binarios no host para rodar no ESP
