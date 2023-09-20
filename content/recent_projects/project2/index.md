---
title: "Into the eBPF (1): Introduction & Installation of eBPF"
date: 2023-08-28
draft: false
recent_projects_tags: ["eBPF", "bcc"]
status: "evergreen"
weight: 1
summary: Introduction & Installation of eBPF
---

## Introduction of eBPF
- eBPF (extended Berkeley Packet Filter, now called BPF) is an in-kernel virtual machine that helps users dynamically load custom code into the kernel. Programming BPF makes users attach smaller BPF programs to the various kernel hook points. By doing so, users can extend the kernel’s capabilities effectively and safely since BPF does not require users to reboot the entire kernel to add functionalities, and BPF programs are supposed to be passed by the verifier, which is a crucial component of BPF and checks if BPF programs have security-critical problems such as loops. It prevents the kernel from crashing due to the eBPF programs.

- BPF is event-driven and runs when a kernel passes particular hook points such as system call, function entry/exit, tracepoints, network stack, and etc.

- The execution flow of BPF programs is as follows:
    - Developers write BPF programs.
    - These are compiled into BPF bytecode programs.
    - BPF bytecode programs go through BPF verifier to check if there are some security-critical problems.
    - When these pass BPF verifier, they are compiled into native kernel code (machine code) using the JIT compiler.
    - Finally, these programs are attached to the pre-defined hooks. Whenever hooks are called, the event is stored in the Maps and accessed from userspace programs.

<br>

## BPF Installation
1. Install build dependencies for Ubuntu 18.04 version
```python
sudo apt-get -y install bison build-essential cmake flex git libedit-dev \
  libllvm6.0 llvm-6.0-dev libclang-6.0-dev python zlib1g-dev libelf-dev libfl-dev python3-setuptools
```
<br>

2. Install and compile BCC
```python
git clone https://github.com/iovisor/bcc.git
mkdir bcc/build; cd bcc/build
cmake ..
make
sudo make install
cmake -DPYTHON_CMD=python3 .. # build python3 binding
pushd src/python/
make
sudo make install
popd
```
<br>

### Note 1
If you face an error due to the LLVM version, you can remove the existing LLVM 6.0 and installed latest llvm and clang version.
```python
sudo apt-get remove --purge llvm-6.0
sudo apt-get install llvm-12 clang-12
```
<br>

### Note 2
You can install dev package if the file 'libclang.so' didn't exist in /usr/lib/llvm-12/lib/ directory.
```python
sudo apt install libclang-12-dev
```
<br>

Then now, you can process the remaining procedure 😊. You can test by running the hello_world.py program in the bcc/example directory. From the next post, I will post what I study and do with eBPF!