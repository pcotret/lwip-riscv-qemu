# lwip-riscv-qemu

## Prerequisites

> **Note 1:** This repository has been tested under CentOS 7 with `***centos6` files. Please download files related to your OS if different.

> **Note 2:** Please note that this PoC runs for 64-bits RISC-V for the moment.

You need a cross-compiler and an emulator. SiFive has pre-built toolchains in a repository: https://github.com/sifive/freedom-tools/releases. As the original repository, it is suggested to use the [August 2019 release](https://github.com/sifive/freedom-tools/releases/tag/v2019.08.0). Please download :

- [riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-centos6.tar.gz](https://static.dev.sifive.com/dev-tools/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-centos6.tar.gz)
- [riscv-qemu-4.1.0-2019.08.0-x86_64-linux-centos6.tar.gz](https://static.dev.sifive.com/dev-tools/riscv-qemu-4.1.0-2019.08.0-x86_64-linux-centos6.tar.gz)

Then, install them to a suitable location (`/opt` in this Readme):

```bash
$ cd /opt
$ tar xvzf riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-centos6.tar.gz
$ tar xvzf riscv-qemu-4.1.0-2019.08.0-x86_64-linux-centos6.tar.gz
```

## Introduction

- lwIP ported to RISC-V http://savannah.nongnu.org/projects/lwip/
- lwIP taken from https://github.com/ReturnInfinity/BareMetal-lwIP and https://github.com/ReturnInfinity/BareMetal-OS.
- riscv code and e1000 driver from https://github.com/mit-pdos/xv6-riscv

## Configuration

- Modify `INSTALL_DIR` in the [Makefile](./Makefile) to the location where is the cross-compiler.
- Modify the [mk](./mk) file for the location of the emulator.

## Build instructions

```bash
$ make
$ mk
```

Output should be similar to:

```
hello
hello1
hello2
reip started v1.00reip started v1httpd_inithttpd_init 1tcp_bind: bind to port %hu
httpd_init 2after httpd_initnetif_set_ipaddr: netif address being changednetif: IP address of interface %c%c set to %hu.%hu.%hu.%hu
netif: netmask of interface %c%c set to %hu.%hu.%hu.%hu
netif: GW address of interface %c%c set to %hu.%hu.%hu.%hu
reif drv init is OKMAC: %X:%X:%X:%X:%X:%X
netif: added interface %c%c IP addr %hu.%hu.%hu.%hu netmask %hu.%hu.%hu.%hu gw %hu.%hu.%hu.%hu
netif_add1netif: setting default interface %c%c
etharp_request: sending ARP request.pbuf_alloc(length=%hu)
pbuf_alloc(length=%hu) == 0x000000000000002c
etharp_raw: sending raw ARP packet.reif_ll_outputpbuf_header: old 0x0000000080079358 new 0x000000008007935a (%hd)
reif_ll_output: pbuf 0 . len: 42 used: 0 
ethernet_txe1000_trans len =42 tail =0
do memcpy in e1000_trans
pbuf_header: old 0x000000008007935a new 0x0000000080079358 (%hd)
pbuf_free(0x0000000080079340)
pbuf_free: deallocating 0x0000000080079340
Interface is UP 
sct calling h=ip_reass_timer arg=0x0000000000000000
time
```

