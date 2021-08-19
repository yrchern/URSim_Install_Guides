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

## Add binaries to PATH

```bash
echo -e "\nPATH="$PATH:$HOME/ursim-5.11.1.108318/usr/bin" >> ~/.profile
source ~/.profile
```

## Faking net-statistics Script ##

To make network working for the simulator, you can create a python script to output the network information of your computer. The easiest way is creating a Python file named `net-statistics` in `/sbin`:

```bash
sudo vi /sbin/net-statistics
```
with the following content (replace values with yours from the output of `ifconfig`):

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

then change its mode:

```bash
chmod 755 /sbin/net-statistics
```


## Start URSim

Now you can start URSim from the command line:

```bash
./start-ursim.sh UR5
```

URSim should start without any errors now. If you see errors, then you can
check the log output on the console to get information what is going wrong.

## Configure Firewall for remote control

By default, Ubuntu has a built-in firewall: UFW, which stands for "Uncomplicated Firewall".
To access the UR robot ports remotely, you need to properly configure this
firewall. Here is the list of [UR client interfaces with port numbers](https://www.universal-robots.com/articles/ur/interface-communication/overview-of-client-interfaces/).

The quick and dirty solution is, to simply allow all incoming connections:

```bash
sudo ufw default allow incoming
sudo ufw default allow outgoing
```

If you would like to have better security, you need deny all incoming connections
and then properly allow all [ports]((https://www.universal-robots.com/articles/ur/interface-communication/overview-of-client-interfaces/)) required by UR robot:

```bash
sudo ufw default deny incoming
sudo ufw allow ssh
sudo ufw allow 29999
...
```

If you prefer a UI for firewall configuration, you can install a graphical
frontend:

```bash
sudo apt install gufw
```
