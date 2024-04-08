# Install and configure xrdp to use Remote Desktop with Ubuntu
When new to Linux, or for quick troubleshooting scenarios, the use of remote desktop may be easier than Secure Shell (SSH) access. This article details how to install and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org/)) for your Linux VM running Ubuntu.

> **Note**
>
> Using Remote Desktop over the internet will introduce noticeable "lag" (input latency) when compared to local desktop use. This can be influenced by multiple factors including local internet speed and distance from the datacenter where the virtual machine is hosted. This lag does not usually reflect the performance of the VM itself.

## Prerequisites
Ubuntu 18.04 LTS or Ubuntu 20.04 LTS VM in Azure.

## Install a desktop environment on your Linux VM
Most Linux VMs in Azure don't have a desktop environment installed by default. Linux VMs are commonly managed using SSH connections rather than a desktop environment, however there are several desktop environments that you can choose to install. Depending on your choice of desktop environment, it consumes up to 2 GB of disk space and take up to ten minutes to both install and configure all the required packages.

The following example installs the lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM. Commands for other distributions vary slightly (use `yum` to install on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` to install on SUSE, for example).

First, SSH to your VM. The following example connects to the VM named `myvm.westus.cloudapp.azure.com` with the username of `azureuser`. Use your own values:

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Next, install xfce using `apt` :

```bash
sudo apt-get update
sudo DEBIAN_FRONTEND=noninteractive apt-get -y install xfce4
sudo apt install xfce4-session
```

## Install and configure a remote desktop server

Now that you have a desktop environment installed, configure a remote desktop service to listen for incoming remote access connections. [xrdp](http://www.xrdp.org/) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions and works well with xfce. Install xrdp on your Ubuntu VM as follows:

```bash
sudo apt-get -y install xrdp
sudo systemctl enable xrdp
```

On Ubuntu 20, you need to give certificate access to an xrdp user:

```bash
sudo adduser xrdp ssl-cert
```

Tell xrdp what desktop environment to use when you start your session. Configure xrdp to use xfce as your desktop environment as follows:

```bash
echo xfce4-session &gt;~/.xsession
```

Restart the xrdp service for the changes to take effect as follows:

```bash
sudo service xrdp restart
```

## Set a local user account password

If you created a password for your user account when you created your VM, skip this step. If you only use SSH key authentication and don't have a local account password set, specify a password before you use xrdp to log in to your VM. xrdp can't accept SSH keys for authentication. The following example specifies a password for the user account `azureuser`:

```bash
sudo passwd azureuser
```

> **Note**
>
> Specifying a password does not update your SSHD configuration to permit password logins if it currently does not. From a security perspective, you may wish to connect to your VM with an SSH tunnel using key-based authentication and then connect to xrdp. If so, skip the following step on creating a network security group rule to allow remote desktop traffic.
> 
## Create a Network Security Group rule for Remote Desktop traffic

To allow Remote Desktop traffic to reach your Linux VM, a network security group rule needs to be created that allows TCP on port 3389 to reach your VM.

The following example creates a network security group rule with `az vm open-port` on port `3389`. From the Azure CLI, not the SSH session to your VM, open the following network security group rule:

Azure CLI

```bash
az vm open-port --resource-group myResourceGroup --name myVM --port 3389
```

## Connect your Linux VM with a Remote Desktop client

Open your local remote desktop client and connect to the IP address or DNS name of your Linux VM.

Enter the username and password for the user account on your VM as follows:

![xrdp-login.png (346×425) (microsoft.com)](https://learn.microsoft.com/en-us/azure/virtual-machines/linux/media/use-remote-desktop/xrdp-login.png)

After authenticating, the xfce desktop environment will load.

If your local RDP client uses network level authentication (NLA), you may need to disable that connection setting. XRDP does not currently support NLA. You can also look at alternative RDP solutions that do support NLA, such as [FreeRDP](https://www.freerdp.com).

## Troubleshoot

If you can't connect to your Linux VM using a Remote Desktop client, use `netstat` on your Linux VM to verify that your VM is listening for RDP connections as follows:

```bash
sudo netstat -plnt | grep rdp
```

The following example shows the VM listening on TCP port 3389 as expected:

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

If the `xrdp-sesman` service isn't listening, on an Ubuntu VM restart the service as follows:

```bash
sudo service xrdp restart
```

Review logs in `/var/log` on your Ubuntu VM for indications as to why the service may not be responding. You can also monitor the syslog during a remote desktop connection attempt to view any errors:

```bash
tail -f /var/log/syslog
```

Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways to restart services and alternate log file locations to review.

If you don't receive any response in your remote desktop client and don't see any events in the system log, this behavior indicates that remote desktop traffic can't reach the VM. Review your network security group rules to ensure that you have a rule to permit TCP on port 3389.