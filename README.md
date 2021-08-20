# URsim 5.11 Installation Guide for Ubuntu 20.04

Currently this document describes how to install **URSim 5.11** in **Ubuntu 20.04**. Assume you have installed both Ubuntu 20.04 ([Ubuntu 20.04 releases page](https://releases.ubuntu.com/20.04/)) and URSim 5.11 packacge ([Universal Robots Download Page](https://www.universal-robots.com/download/software-e-series/simulator-linux/offline-simulator-e-series-ur-sim-for-linux-5110/)).

If you have futher additions, feel free to create a pull request.

# Dependency requirements

The install script requires **openjdk-8**, you need to remove openjdk that comes with Ubuntu 20.04 before installing **openjdk-8**.

```bash
sudo apt remove openjdk-*
sudo apt install openjdk-8-jdk openjdk-8-jre
```

## Run URSim Install Script

Before running `install.sh`, open it and change `libcurl4` to `libcurl3` in the file.

Using your bash prompt run the `install.sh` script using the following command.

```bash
sudo ./install.sh
```


## net-statistics Script

To make network working for the simulator in Ubuntu 20.04, the simplest way is to create a script named `net-statistics` in `/sbin`, which outputs the network information of your computer.

```bash
sudo vi /sbin/net-statistics
```
with the following content (replace values with yours from the output of `ifconfig` command):

```Python3
#!/usr/bin/python3

netinfo = """Mode:static
Net up
Address:192.168.190.134
Mask:255.255.255.0
Gateway:
nameserver1:
nameserver2:
Hostname:ubuntu"""

print(netinfo)

```

Alternatively, you can download `net-statistics` from `src` folder and copy/move it to `/sbin`. Change the configuration (mainly `interface`) at the beginning of the Python script to match your computer settings and change its file mode:

```bash
chmod 755 /sbin/net-statistics
```

* `net-statistics` is a Python script I wrote for myself to run with **URsim** and is not extensively tested. Use at your own risk.


## Start URSim

Now you can start URSim from the command line from **URsim** folder:

```bash
./start-ursim.sh UR5
```

URSim should start without any errors now. If you see errors, then you can
check the log output on the console to get information what is going wrong.

## Install URCap Files

To install URCap files, you need to start the simulator first. Then you can find a folder called `programs` under `ursim-5.11.1.108318` folder. Simply copy `.urcap` file into it and you will be able to install URCap file from the GUI.

