# Ex.No 06 – Transfer Files Between Virtual Machines

## Aim
To find a procedure to transfer files from one virtual machine to another virtual machine.

## Methods Covered
1. Copy and Paste (Drag and Drop)
2. USB Drive
3. Network / Shared Folder

## Procedure

### 1. Copy and Paste Data in VirtualBox
1. With your virtual machine running, go to **Devices → Drag and Drop**.
2. Choose one of: **Host to Guest**, **Guest to Host**, or **Bidirectional** (default is Disabled).
3. For best results, select **Bidirectional**.

### 2. Share Files From a USB Stick in VirtualBox
1. Install the **VirtualBox Extension Pack** (required for USB access) from:
   https://www.virtualbox.org/wiki/Downloads
2. Insert the USB device.
3. Open VirtualBox → **File → Preferences → Extensions → +**.
4. Browse to the downloaded Extension Pack, click **Open**, then **Install** and follow the prompts.
5. Confirm USB is enabled under **Settings → USB**.

### 3. Create a Shared Folder in VirtualBox
1. Install **VirtualBox Guest Additions** via **Devices → Install Guest Additions**, browsing to the appropriate EXE and following the prompts to completion.
2. Open **Devices → Shared Folders → Shared Folders Settings**.
3. Click **+**, then in **Folder Path** click the dropdown → **Other**.
4. Browse the host OS for the folder to share, select it.
5. In the Add Share dialog, give the share a name (recommended to match host and guest names).
6. Check **Auto-mount** and **Make Permanent**, then click **OK**.
7. From the guest OS, the shared folder will appear as a network location (e.g., under Network Locations in Windows Explorer).

## Result
The procedure to transfer files between virtual machines (drag-and-drop, USB, and shared folders) was executed successfully.
