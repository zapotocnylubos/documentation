---
title: "Installing TrueCommand on Windows"
description: "Running TrueCommand in Docker Desktop for Windows"
---

{{% pageinfo %}}
For even easier deployment, iXsystems now offers TrueCommand as a cloud service!
See the [TrueCommand information page]({{< relref "tcwhatis.md" >}}) for more details.
{{% /pageinfo %}}

## Prerequisites

The requirements to run TrueCommand in Docker Desktop for Windows are:

 + Windows 10 Enterprise, Pro, or Education editions.
 + 64-bit Processor with Second Level Address Translation (SLAT).
 + CPU support for VM Monitor Mode Extension (VT-c on Intel CPUs).
 + Hyper-V is enabled in Windows 10.
 + 4 GB memory at minimum.
 + [Docker Desktop](https://www.docker.com/products/docker-desktop) needs to be installed in Windows.

### Enable Hyper-V

To enable Hyper-V, click on the Windows Start button and select or search for *Apps & Features*. Select *Programs and Features* under **Related settings** and *Turn Windows Features on or off* (Administrator action). Set the Hyper-V option and click **Ok**. You will need to restart your restart your computer for the change to take effect.

<img src="/images/EnableHyperV.png">
<br><br>

Alternatively, Hyper-V can be enabled with the Powershell. To do this, run Powershell as a Windows Administrator and enter `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All`. If an error is returned that says the command could not be found, verify that you are running PowerShell as the Administrator. After the command successfully runs, reboot the computer.

<img src="/images/PowershellHyperV1.png">
<br><br>
<img src="/images/PowershellHyperV2.png">
<br><br>

### Install Docker Desktop

Open Docker Hub and click the *Get Docker* button to download the [Docker Desktop from Docker Hub](https://hub.docker.com/editions/community/docker-ce-desktop-windows/).

<img src="/images/DownloadDockerDesktop.png">
<br><br>

Run the installer after the download completes. When the installer is finished, reboot the system.

If the admin account is different from your Windows user account, the user must be added to the `docker-users` group. Run *Computer Management* as an administrator and go to **Local Users and Groups > Groups > docker-users** to add the user to the group. You will need to log out and back in for the changes to take effect.

If this error message appears after rebooting, install the Linux Kernel Update Package:

<img src="/images/DockerDesktop4Error.png">
<br><br>

The update package can be downloaded from a [Windows storage location](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi).

<img src="/images/DockerDesktop5.png">
<br><br>

Microsoft has additional documentation available for assistance with [downloading the Linux kernel update](https://docs.microsoft.com/en-us/windows/wsl/install-win10#step-4---download-the-linux-kernel-update-package).

After installing the kernel update, set the WSL default version to `version 2` by opening the Powershell and entering `wsl --set-default-version 2`.

<img src="/images/DockerDesktop6.png">
<br><br>

The system must be rebooted after changing the default version.

## Installing the TrueCommand Docker Container

Open the [Docker Hub](https://hub.docker.com) in a browser and search for `ixsystems/truecommand`.

<img src="/images/DockerHub1.png">
<br><br>

<img src="/images/DockerHub2.png">
<br><br>

Verify the pull command required and run it from a command line. Example: `docker pull ixsystems/truecommand:latest`.

<img src="/images/DockerHub3.png">
<br><br>

When the container is downloaded, open the Docker Desktop and select *Images*.
Hover over the *ixsystems/truecommand* entry to show the **Run** button, then click it.

<img src="/images/DockerDesktop7.png">
<br><br>

Open the *Optional Settings* drop down menu, name the container, and set the following port values.
Investigate your network environment or check with your IT department to ensure that these ports will not conflict with any other running services.

+ Local Host Port: `9005`
+ Container Port `443`

Click the `+` sign to add a second set of ports.

+ Local Host Port `9004`
+ Container Port `80/tcp`

<img src="/images/DockerDesktop8.png">
<br><br>

Setting the *Volume* is not usually required for TrueCommand.
Click **RUN** after configuring the settings.

When Docker Desktop shows the container status as **RUNNING**, open a new browser tab and go to `https://127.0.0.1:9005`.

<img src="/images/DockerDesktop9.png">
<br><br>

Because TrueCommand uses a self-signed certificate, the certificate must be manually authorized before the TrueCommand web interface can be accessed:

<img src="/images/DockerBrowser1.png">
<br><br>

The initial TrueCommand screen requires creating an administrator account before logging in.  
<img src="/images/DockerBrowser2.png">
<br><br>
<!-- markdown-link-check-disable-next-line -->
After creating the account the login screen refreshes and you can log in with the account credentials that were just created.
TrueCommand can now be configured and begin to be used.
See the remaining [TrueCommand Administration articles]({{< relref "/truecommand/admins/_index.md" >}}) for specific usage guides.

## Support

The [TrueNAS Community](https://www.truenas.com/community/) is an active online resource for asking questions, troubleshooting issues, and sharing information with other TrueNAS or TrueCommand users. [Registering](https://www.truenas.com/community/register/) is required for posting. New users are encouraged to briefly [introduce](https://www.truenas.com/community/forums/introductions.25/) themselves and review the [forum rules](https://www.truenas.com/community/threads/forum-rules.45124/) before posting.

iXsystems also offers different Support packages for TrueCommand customers. To find more details about the different Warranty and Service Level Agreement (SLA) options available, see the [iXsystems Support overview](https://www.ixsystems.com/support/), **TrueCommand** tab.
