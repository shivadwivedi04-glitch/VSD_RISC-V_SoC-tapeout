# RISC-V SoC Tapeout Program – VSD

## Tool Setup Guide

### System Prerequisites
- Minimum **6 GB RAM**
- At least **50 GB disk space**
- **Ubuntu 20.04 LTS or newer**
- **Quad-core CPU (4 vCPUs)**

---

### Adjusting Ubuntu Window Size  
Run the following commands to enable proper screen resizing inside VirtualBox:

```bash
sudo apt update
sudo apt install build-essential dkms linux-headers-$(uname -r)
cd /media/spatha/VBox_GAs_7.1.8/
./autorun.sh
```

### Yosys (Synthesis Tool)
```bash
sudo apt-get update
git clone https://github.com/YosysHQ/yosys.git
cd yosys
sudo apt install make
sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
make config-gcc
git submodule update --init --recursive
make
sudo make install
```

### Icarus Verilog (Simulation Tool)

```bash
sudo apt-get update
sudo apt-get install iverilog
```

### GTKWave

```bash
sudo apt-get update
sudo apt install gtkwave
```
