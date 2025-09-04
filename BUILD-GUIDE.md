# Compiling Clang 6 from Source for TunSafe Linux Build

A comprehensive guide to building Clang 6.0 from source code to successfully compile TunSafe on Linux systems.

## Why This Guide?

TunSafe provides an official Linux installation guide on their [website](https://tunsafe.com/user-guide/linux), but it no longer works out of the box. The issue is that TunSafe's build scripts require Clang 6.0, which is no longer available through official repositories in current Debian and Ubuntu distributions.

Rather than relying on unofficial third-party sources, this guide demonstrates how to build a working TunSafe installation using only trusted sources:
- **LLVM Project**: https://github.com/llvm/llvm-project/
- **TunSafe**: https://github.com/TunSafe/TunSafe

## About This Guide

The technical solution and compilation process described here is my own work - I figured out how to solve the Clang 6.0 dependency issue through research and testing. However, since my strength is problem-solving rather than writing, I used an LLM to help make this documentation more readable and well-structured.

## ⚠️ Disclaimer

**Use at your own risk.** As of September 4, 2025:
- Both Clang 6.0 and TunSafe are **no longer actively developed or maintained**
- I am not affiliated with the TunSafe or LLVM/Clang projects
- This guide is provided as-is, without warranty of any kind
- You are solely responsible for any consequences of following this guide

**TL;DR: Everything you do with this guide is your responsibility.**

## Prerequisites

Before starting, ensure you have the following tools installed:
- `wget` - for downloading source code
- `git` - for cloning repositories  
- Build essentials (gcc, make, cmake)
- `sudo` privileges - required for certain installation steps
- Sufficient disk space (several GB for LLVM compilation)

**Tested Environment:** This guide has been tested on Debian Trixie.

## Step 1: Download LLVM 6.x Source Code

Navigate to the LLVM project repository at the 6.x release branch:
**https://github.com/llvm/llvm-project/tree/release/6.x**

1. Click on **"Code"** button (green button)
2. Select **"Download ZIP"** 
3. Copy the download link for use with wget

The download URL should be:
```
https://github.com/llvm/llvm-project/archive/refs/heads/release/6.x.zip
```

![LLVM Download Screenshot](https://github.com/user-attachments/assets/57edf9ab-93c2-4027-ad85-c3c3ce78423f)

## Step 2: Download and Extract LLVM Source

Download the source code using wget:
```bash
wget https://github.com/llvm/llvm-project/archive/refs/heads/release/6.x.zip
```

Verify the download:
```bash
$ ls
6.x.zip
```

Extract the archive:
```bash
unzip 6.x.zip
```

Check the extracted contents:
```bash
$ ls
6.x.zip  llvm-project-release-6.x
```

## Step 3: Configure LLVM Build

Navigate to the extracted directory and set up the build:
```bash
cd llvm-project-release-6.x/
mkdir build
cd build/
```

Configure the build with cmake (following the official [LLVM getting started guide](https://clang.llvm.org/get_started.html) with convenience modifications):
```bash
cmake -DLLVM_ENABLE_PROJECTS=clang -DCMAKE_BUILD_TYPE=Release -G "Unix Makefiles" ../llvm
```

## Step 4: Build LLVM and Clang

**⚠️ WARNING: This step takes a very long time!**

The compilation process is extremely resource-intensive and time-consuming. Build times tested:
- **Older 2c/4t i5**: Over 1 hour
- **Ryzen 5900HX 8c/16t**: Approximately 25 minutes

Start the build process using all available CPU cores:
```bash
time make -j $(nproc)
```

**Notes:**
- `time` is added to show you how long the build took on your system
- `-j $(nproc)` uses all available CPU cores and threads for fastest compilation
- Only use this if you're not doing other intensive tasks on the system

## Step 5: Install Clang 6.0

**Important:** This guide assumes you want only one Clang installation on your system. While having multiple Clang versions is absolutely possible, this guide doesn't cover managing multiple installations - if you need that, you'll have to figure out the setup yourself and adapt the following TunSafe compilation steps accordingly.

After the build completes successfully, install Clang system-wide:
```bash
sudo make install
```
