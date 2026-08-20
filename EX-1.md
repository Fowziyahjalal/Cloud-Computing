# Ex.No 01 – Virtual Workstation

## Aim
To install VirtualBox/VMware/equivalent open source cloud workstation with different flavours of Linux or Windows OS on top of Windows 8 and above.

## Tools Used
- Oracle VM VirtualBox 7.0.14
- A guest OS ISO image (e.g., Windows 98SE used in this demo)

## Procedure

### Installing VirtualBox on Windows
1. Go to the VirtualBox website: https://www.virtualbox.org/wiki/Downloads
2. Click **Download VirtualBox**.
3. Click the **Windows hosts** link under "VirtualBox 7.0.14 platform packages".
4. Open the downloaded VirtualBox `.exe` file to start the installer.
5. Click **Next** on the Welcome window.
6. Choose the installation folder and click **Next**.
7. Select the features to install and click **Next**.
8. Click **Yes** to allow installation of the network interfaces.
9. Click **Install** to begin installation.
10. Click **Finish** — VirtualBox will open automatically.

### Creating a Virtual Machine
11. Open VirtualBox and click **New**. Fill in:
    - **Name**: any name relevant to the OS you're installing
    - **Installation path**: keep default
    - **ISO Image**: select the ISO of the OS to install
    - **Type**: Linux / Windows / Mac
    - **Version**: appropriate OS version and architecture
12. Click **Next** and allocate resources:
    - Base Memory: 512 MB
    - Processors: 1 CPU
13. In the Virtual Hard Disk wizard, set **Disk size** (e.g., 2.00 GB) and click **Next**, then **Finish**.
14. Select the VM and click **Start** to begin the OS installation wizard.
15. Follow the on-screen steps to complete the OS installation.

## Result
VirtualBox installation on a Windows 10 host machine and installation of a guest operating system were completed successfully.
