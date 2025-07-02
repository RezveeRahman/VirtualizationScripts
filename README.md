# Virtualization Scripts

Quick summary: This project repositroy contains virtualization scripts. We will be building minimal / tiny linux kernel and use QEMU to run the kernel.

<h2 id="1_">Quick start </h2>

<h3 id="1_1"> project directory setup </h3>

Your directory will be structured as such.

```
├── documentation
│   ├── directory_structure.txt
│   └── images
├── LICENSE
├── linux (submodule)
├── linux_build
├── README.md
└── scripts

6 directories, 3 files
```
you will download the kernel in linux directory <b> See initializing submodules</b>.

<h3 id="1_2"> initializing submodules </h3>
You'll need to initialize the submodule. The submodule points to the linux kernel maintained and owned by Linus Torvalds.

```bash
$ git submodule update --init <depth=1>
```
- `depth=1` if you want the master branch history only.

<h3 id="1_3"> configuring for a tiny / small configuration </h3>

You want to configure the linux kernel to minimum / smallest configuration possible. Thankfully the `makefile` provided by Torvalds et al. does have a small configuration we can use. To set up our kernel, we will do the following:

<b>Be sure to be in the <u> linux directory </u> and also have the <u>linux `make` build tools.</u> </b>

```bash
$ make tinyconfig
```

I would suggest you use the `linux_build` directory to output the configuration and build the results there.

```bash
$ make O=../linux_build tinyconfig
```

You might've heard about the `allnoconfig` as an alternative configuration. You can use `allonoconfig` instead of `tinyconfig`. However, for embedded devices, `tinyconfig` is the way to go. `tinyconfig` is based on `allnoconfig` with some slight additions. I will not be going over the details. <b> [LWM.net - [PATCH] x86: Add "make tinyconfig" to configure the tiniest possible kernel ](https://lwn.net/Articles/608427/) </b>

Once you have configured the kernel, now you are ready to build the kernel.

Simply just invoke `make` on the command line.
```bash
$ make
```

<b> Alternatively </b> if you want to build the kernel using more workers / processors you can use the following command.

```bash
$ make <optional target directory | use ../linux_build> -j8

or
$ make O=../linux_build -j8
# Assuming you are in the linux directory itself.
```
<b>Expected output of making the kernel: </b>

```bash
$ Kernel: arch/x86/boot/bzImage is ready  (#1)
```

notice that the kernel is a `bzImage`

Here is the output when we have compiled the kernel Image. Note that this is only one small part of compiled file structure.
```bash
[rezvee@fedora ~/Projects/VirtualizationScripts]$ tree linux_build/arch/x86/boot/
linux_build/arch/x86/boot/
├── a20.o
├── bioscall.o
├── bzImage
├── cmdline.o
├── compressed
│   ├── cmdline.o
│   ├── cpuflags.o
│   ├── error.o
│   ├── head_32.o
│   ├── kernel_info.o
│   ├── misc.o
│   ├── mkpiggy
│   ├── piggy.o
│   ├── piggy.S
│   ├── string.o
│   ├── vmlinux
│   ├── vmlinux.bin
│   ├── vmlinux.bin.xz
│   └── vmlinux.lds
├── copy.o
├── cpucheck.o
├── cpuflags.o
├── cpu.o
├── cpustr.h
├── early_serial_console.o
├── edd.o
├── header.o
├── main.o
├── memory.o
├── mkcpustr
├── pmjump.o
├── pm.o
├── printf.o
├── regs.o
├── setup.bin
├── setup.elf
├── startup
│   ├── built-in.a
│   └── lib.a
├── string.o
├── tty.o
├── version.o
├── video-bios.o
├── video-mode.o
├── video.o
├── video-vesa.o
├── video-vga.o
├── vmlinux.bin
├── voffset.h
└── zoffset.h

3 directories, 48 files
```


<h2 id="resources"> Resources </h2>

- https://www.subrat.info/build-kernel-and-userspace/
- https://lwn.net/Articles/608427/
