# Install and configure xrdp to use Remote Desktop with Ubuntu


**Applies to:** ✔️ Linux VMs ✔️ Flexible scale sets

When new to Linux, or for quick troubleshooting scenarios, the use of remote desktop may be easier than Secure Shell (SSH) access. This article details how to install and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org/)) for your Linux VM running Ubuntu.

The article was written and tested using an Ubuntu 18.04 VM.

> **Note**
>
> Using Remote Desktop over the internet will introduce noticeable "lag" (input latency) when compared to local desktop use. This can be influenced by multiple factors including local internet speed and distance from the datacenter where the virtual machine is hosted. This lag does not usually reflect the performance of the VM itself.
>
## Prerequisites

This article requires an existing Ubuntu 18.04 LTS or Ubuntu 20.04 LTS VM in Azure.

## Install a desktop environment on your Linux VM
Most Linux VMs in Azure don't have a desktop environment installed by default. Linux VMs are commonly managed using SSH connections rather than a desktop environment, however there are several desktop environments that you can choose to install. Depending on your choice of desktop environment, it consumes up to 2 GB of disk space and take up to ten minutes to both install and configure all the required packages.

The following example installs the lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM. Commands for other distributions vary slightly (use `yum` to install on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` to install on SUSE, for example).

First, SSH to your VM. The following example connects to the VM named _myvm.westus.cloudapp.azure.com_ with the username of _azureuser_. Use your own values:

```bash
<span>ssh azureuser@myvm.westus.cloudapp.azure.com
</span>
```

If you're using Windows and need more information on using SSH, see [How to use SSH keys with Windows](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.htmlssh-from-windows).

Next, install xfce using `apt` :

```bash
<span>sudo apt-get update
sudo DEBIAN_FRONTEND=noninteractive apt-get -y install xfce4
sudo apt install xfce4-session
</span>
```

## Install and configure a remote desktop server

Now that you have a desktop environment installed, configure a remote desktop service to listen for incoming remote access connections. [xrdp](http://www.xrdp.org/) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions and works well with xfce. Install xrdp on your Ubuntu VM as follows:

```bash
<span>sudo apt-get -y install xrdp
sudo systemctl <span class="hljs-built_in">enable</span> xrdp
</span>
```

On Ubuntu 20, you need to give certificate access to an xrdp user:

```bash
<span>sudo adduser xrdp ssl-cert
</span>
```

Tell xrdp what desktop environment to use when you start your session. Configure xrdp to use xfce as your desktop environment as follows:

```bash
<span><span class="hljs-built_in">echo</span> xfce4-session &gt;~/.xsession
</span>
```

Restart the xrdp service for the changes to take effect as follows:

```bash
<span>sudo service xrdp restart
</span>
```

## Set a local user account password

If you created a password for your user account when you created your VM, skip this step. If you only use SSH key authentication and don't have a local account password set, specify a password before you use xrdp to log in to your VM. xrdp can't accept SSH keys for authentication. The following example specifies a password for the user account _azureuser_:

```bash
<span>sudo passwd azureuser
</span>
```

> **Note**
>
> Specifying a password does not update your SSHD configuration to permit password logins if it currently does not. From a security perspective, you may wish to connect to your VM with an SSH tunnel using key-based authentication and then connect to xrdp. If so, skip the following step on creating a network security group rule to allow remote desktop traffic.
> 
## Create a Network Security Group rule for Remote Desktop traffic

To allow Remote Desktop traffic to reach your Linux VM, a network security group rule needs to be created that allows TCP on port 3389 to reach your VM. For more information about network security group rules, see [What is a network security group?](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html../../virtual-network/network-security-groups-overview) You can also [use the Azure portal to create a network security group rule](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html../windows/nsg-quickstart-portal).

-   [Azure CLI](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#tabpanel_1_azure-cli)
-   [Azure PowerShell](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#tabpanel_1_azure-powershell)

The following example creates a network security group rule with [az vm open-port](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/en-us/cli/azure/vm#az-vm-open-port) on port _3389_. From the Azure CLI, not the SSH session to your VM, open the following network security group rule:

Azure CLI Copy

```
<span><span class="hljs-keyword">az vm open-port </span><span class="hljs-parameter">--resource-group</span> myResourceGroup <span class="hljs-parameter">--name</span> myVM <span class="hljs-parameter">--port</span> <span class="hljs-number">3389</span>
</span>
```

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#connect-your-linux-vm-with-a-remote-desktop-client)

## Connect your Linux VM with a Remote Desktop client

Open your local remote desktop client and connect to the IP address or DNS name of your Linux VM.

![Screenshot of the remote desktop client.](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.htmlmedia/use-remote-desktop/remote-desktop.png)

Enter the username and password for the user account on your VM as follows:

![Screenshot of the xrdp log in screen.](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.htmlmedia/use-remote-desktop/xrdp-login.png)

After authenticating, the xfce desktop environment will load and look similar to the following example:

![xfce desktop environment through xrdp](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.htmlmedia/use-remote-desktop/xfce-desktop-environment.png)

If your local RDP client uses network level authentication (NLA), you may need to disable that connection setting. XRDP does not currently support NLA. You can also look at alternative RDP solutions that do support NLA, such as [FreeRDP](https://www.freerdp.com).

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#troubleshoot)

## Troubleshoot

If you can't connect to your Linux VM using a Remote Desktop client, use `netstat` on your Linux VM to verify that your VM is listening for RDP connections as follows:

Bash Copy

```
<span>sudo netstat -plnt | grep rdp
</span>
```

The following example shows the VM listening on TCP port 3389 as expected:

Bash Copy

```
<span>tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
</span>
```

If the _xrdp-sesman_ service isn't listening, on an Ubuntu VM restart the service as follows:

Bash Copy

```
<span>sudo service xrdp restart
</span>
```

Review logs in _/var/log_ on your Ubuntu VM for indications as to why the service may not be responding. You can also monitor the syslog during a remote desktop connection attempt to view any errors:

Bash Copy

```
<span>tail -f /var/<span class="hljs-built_in">log</span>/syslog
</span>
```

Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways to restart services and alternate log file locations to review.

If you don't receive any response in your remote desktop client and don't see any events in the system log, this behavior indicates that remote desktop traffic can't reach the VM. Review your network security group rules to ensure that you have a rule to permit TCP on port 3389. For more information, see [Troubleshoot application connectivity issues](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/en-us/troubleshoot/azure/virtual-machines/troubleshoot-app-connection).

[](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.html#next-steps)

## Next steps

For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.htmlmac-create-ssh-keys).

For information on using SSH from Windows, see [How to use SSH keys with Windows](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/_generated_background_page.htmlssh-from-windows).

## Feedback

Coming soon: Throughout 2024 we will be phasing out GitHub Issues as the feedback mechanism for content and replacing it with a new feedback system. For more information see: [https://aka.ms/ContentUserFeedback](https://aka.ms/ContentUserFeedback).

Submit and view feedback for

[This product](https://feedback.azure.com/d365community/forum/ec2f1827-be25-ec11-b6e6-000d3a4f0f1c) [This page](https://github.com/MicrosoftDocs/azure-docs/issues/new?title=&body=%0A%0A%5BEnter%20feedback%20here%5D%0A%0A%0A---%0A%23%23%23%23%20Document%20Details%0A%0A%E2%9A%A0%20*Do%20not%20edit%20this%20section.%20It%20is%20required%20for%20learn.microsoft.com%20%E2%9E%9F%20GitHub%20issue%20linking.*%0A%0A*%20ID%3A%20077ee673-528a-d893-5832-7656b91dbec8%0A*%20Version%20Independent%20ID%3A%202180e845-1ead-3b47-03be-c26aee00c6f7%0A*%20Content%3A%20%5BUse%20xrdp%20with%20Linux%20-%20Azure%20Virtual%20Machines%5D(https%3A%2F%2Flearn.microsoft.com%2Fen-us%2Fazure%2Fvirtual-machines%2Flinux%2Fuse-remote-desktop%3Fsource%3Drecommendations%26tabs%3Dazure-cli)%0A*%20Content%20Source%3A%20%5Barticles%2Fvirtual-machines%2Flinux%2Fuse-remote-desktop.md%5D(https%3A%2F%2Fgithub.com%2FMicrosoftDocs%2Fazure-docs%2Fblob%2Fmain%2Farticles%2Fvirtual-machines%2Flinux%2Fuse-remote-desktop.md)%0A*%20Service%3A%20**virtual-machines**%0A*%20GitHub%20Login%3A%20%40mattmcinnes%0A*%20Microsoft%20Alias%3A%20**mattmcinnes**)

[View all page feedback](https://github.com/MicrosoftDocs/azure-docs/issues?utf8=%E2%9C%93&q=%222180e845-1ead-3b47-03be-c26aee00c6f7%22&in=body)

## Additional resources

___

Training

Learning path

[Deliver remote desktops and apps with Azure Virtual Desktop - Training](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/en-us/training/paths/m365-wvd/?source=recommendations)

Azure Virtual Desktop on Microsoft Azure is a desktop and app virtualization service that runs on the cloud. Azure Virtual Desktop works across devices – including Windows, Mac, iOS, and Android – with full-featured apps that you can use to access remote desktops and apps.

___

Documentation

-   [Use SSH keys to connect to Linux VMs - Azure Virtual Machines](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/en-us/azure/virtual-machines/linux/ssh-from-windows?source=recommendations)
    
    Learn how to generate and use SSH keys from a Windows computer to connect to a Linux virtual machine on Azure.
    
-   [Connect to a Linux VM - Azure Virtual Machines](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/en-us/azure/virtual-machines/linux-vm-connect?source=recommendations)
    
    Learn how to connect to a Linux VM in Azure.
    
-   [Enable graphical remote desktop for Linux labs - Azure Lab Services](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/en-us/azure/lab-services/how-to-enable-remote-desktop-linux?source=recommendations)
    
    Learn how to enable remote desktop for Linux virtual machines in a lab in Azure Lab Services, and about options for best performance.
    

Show 4 more

[English (United States)](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/en-us/locale?target=https%3A%2F%2Flearn.microsoft.com%2Fen-us%2Fazure%2Fvirtual-machines%2Flinux%2Fuse-remote-desktop%3Fsource%3Drecommendations)

[Your Privacy Choices](https://aka.ms/yourcaliforniaprivacychoices)

Theme

-   [Previous Versions](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/en-us/previous-versions/)
-   [Blog](https://techcommunity.microsoft.com/t5/microsoft-learn-blog/bg-p/MicrosoftLearnBlog)
-   [Contribute](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/en-us/contribute/)
-   [Privacy](https://go.microsoft.com/fwlink/?LinkId=521839)
-   [Terms of Use](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/en-us/legal/termsofuse)
-   [Trademarks](https://www.microsoft.com/legal/intellectualproperty/Trademarks/)
-   © Microsoft 2024