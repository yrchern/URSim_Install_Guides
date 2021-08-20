# URsim 5.11 Installation Guide for Ubuntu 20.04

Currently this document describes how to install **URSim 5.11** in **Ubuntu 20.04.** 

If you have futher additions, feel free to create a pull request.

## Install Ubuntu 20.04

Download and install Ubuntu 20.04 from to [Ubuntu 20.04 releases page](https://releases.ubuntu.com/20.04/).


## Download and unpack URSim 5.11

Download the URSim 5.11 packacge from the [Universal Robots Download Page](https://www.universal-robots.com/download/software-e-series/simulator-linux/offline-simulator-e-series-ur-sim-for-linux-5110/). You need a user account for this download.

Extract the downloaded archive as per the instructions.

# Dependency requirements

The scipt needs Java 6-8 installed, but automatically installs Java 11. If Java 8 is installed prior to running the install script it won't install Java 11. Do so by running: `sudo apt install openjdk-8-jdk openjdk-8-jre`

## Run URSim Install Script

Before running `install.sh`, open it and change `libcurl4` to `libcurl3`.

Using your bash prompt run the `install.sh` script using the following command.

```bash
sudo ./install.sh
```



## net-statistics Script ##

To make network working for the simulator, the easiest way is to create a python script to output the network information of your computer. The easiest way is creating a Python file named `net-statistics` in `/sbin`:

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

Alternatively, you can download `net-statistics` from `src` folder and copy/move it to `/sbin`. Modify the configuration at the beginning of the Python script.


Next, change its file mode:

```bash
chmod 755 /sbin/net-statistics
```


## Start URSim

Now you can start URSim from the command line from `ursim-5.11.1.108318` folder:

```bash
./start-ursim.sh UR5
```

URSim should start without any errors now. If you see errors, then you can
check the log output on the console to get information what is going wrong.

## Install URCap Files

To install URCap files, you need to start the simulator first. Then you can find a folder called `programs` under `ursim-5.11.1.108318` folder. Simply copy `.urcap` file into it and you will be able to install URCap file from the GUI.

