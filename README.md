# Virtualization Scripts

Quick summary: This project repositroy contains virtualization scripts. We will be building minimal / tiny linux kernel and use QEMU to run the kernel.

<h2 id="1_">1. Getting started </h2>

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

<h2 id="resources"> Resources </h2>

- https://www.subrat.info/build-kernel-and-userspace/