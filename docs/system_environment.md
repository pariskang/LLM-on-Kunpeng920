# System Environment Preparation for Large Language Model Deployment on Huawei Kunpeng 920

This document outlines the steps for preparing the system environment for deploying large language models on the Huawei Kunpeng 920 platform.

## Table of Contents

1. [System Information](#1-system-information)
2. [Disk Management](#2-disk-management)
3. [Package Management](#3-package-management)
4. [Conda Environment Setup](#4-conda-environment-setup)
5. [Network Configuration](#5-network-configuration)
6. [Development Tools Installation](#6-development-tools-installation)

## 1. System Information

Before starting the setup, it's crucial to gather information about the system:

```bash
# Check system release information
lsb_release -a
hostnamectl

# Check operating system details
cat /etc/os-release

# Check kernel version
uname -a

# Check CPU information
lscpu | grep "Model name"
cat /proc/cpuinfo

# Check available disk space
df -h

# Check available memory
free -h
```

## 2. Disk Management

If additional storage is required:

```bash
# Create mount points
mkdir /mnt/disk1 /mnt/disk2 /mnt/disk3

# Format new disks (if necessary)
mkfs.ext4 /dev/sdb
mkfs.ext4 /dev/sdc
mkfs.ext4 /dev/sdd

# Mount the disks
mount /dev/sdb /mnt/disk1
mount /dev/sdc /mnt/disk2
mount /dev/sdd /mnt/disk3

# Make mounts persistent
echo "/dev/sdb    /mnt/disk1    ext4    defaults    0    2" >> /etc/fstab
echo "/dev/sdc    /mnt/disk2    ext4    defaults    0    2" >> /etc/fstab
echo "/dev/sdd    /mnt/disk3    ext4    defaults    0    2" >> /etc/fstab

# Apply fstab changes
mount -a
```

## 3. Package Management

Ensure the package manager is up-to-date:

```bash
sudo apt-get update
sudo apt-get upgrade
```

Install essential packages:

```bash
sudo apt-get install software-properties-common dirmngr build-essential
```

## 4. Conda Environment Setup

Conda is used for managing Python environments:

```bash
# Download and install Miniconda
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh

# Initialize conda
source ~/.bashrc
conda init

# Create and activate a new environment
conda create -n llm python=3.9
conda activate llm
```

## 5. Network Configuration

If you're behind a proxy or need to configure network settings:

```bash
# Check current proxy settings
echo $http_proxy
echo $https_proxy

# Set proxy (if needed)
export http_proxy="http://proxy.example.com:port"
export https_proxy="http://proxy.example.com:port"

# Add to .bashrc for persistence
echo "export http_proxy='http://proxy.example.com:port'" >> ~/.bashrc
echo "export https_proxy='http://proxy.example.com:port'" >> ~/.bashrc

# Test internet connectivity
curl -I http://google.com
```

## 6. Development Tools Installation

Install necessary development tools:

```bash
# Install GCC and G++
sudo apt-get install gcc g++

# Install CMake
wget https://github.com/Kitware/CMake/releases/download/v3.28.1/cmake-3.28.1-linux-aarch64.sh
chmod +x cmake-3.28.1-linux-aarch64.sh
sudo mkdir -p /opt/cmake
sudo ./cmake-3.28.1-linux-aarch64.sh --prefix=/opt/cmake --skip-license
export PATH=/opt/cmake/bin:$PATH
echo "export PATH=/opt/cmake/bin:$PATH" >> ~/.bashrc

# Verify CMake installation
cmake --version

# Install Git (if not already installed)
sudo apt-get install git

# Install Python development files
sudo apt-get install python3-dev
```

After completing these steps, your Huawei Kunpeng 920 system should be prepared for the next stages of large language model deployment, including model-specific setups and compilations.

Remember to logout and log back in (or source your `.bashrc`) after making changes to environment variables or PATH to ensure they take effect.
