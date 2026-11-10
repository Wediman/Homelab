## 📖 Standard Operating Procedure (SOP) & Installation Guide
This guide breaks down the step-by-step creation of *lab.local* inside Oracle VM VirtualBox. It is written to be clear enough for anyone—even if it's their very first time spinning up a Virtual Machine or configuring Windows Server.

## 🛠️ Prerequisites & Lab Requirements
Before touching VirtualBox, make sure your host machine has the proper hardware and ISO files downloaded.

### System Requirements
- **RAM:** 16 GB recommended (Minimum 8 GB allocated: 4 GB for DC01, 2 GB for USR02Pro, 2 GB for User01Ent).

- **Storage:** ~100 GB free disk space (Solid State Drive preferred).

- **Hypervisor:** Oracle VM VirtualBox (v7.0+).

### Required ISO Downloads
- **Windows Server 2022 ISO** (Evaluation Edition)

- **Windows 11 ISO** (Multi-edition x64)

## 🌐 Phase 1: Virtual Network Setup (VirtualBox)
To keep our lab traffic completely isolated from your physical home network, we need a dedicated Internal Network inside VirtualBox.

- Open **VirtualBox** and navigate to **File** > **Tools** > **Network Manager.**

- Create a new **NAT Network** or ensure all VMs will be assigned to an Internal Network (e.g., named AD-Lab-Net).

- Set network parameters:

  - Network Name: *AD-Lab-Net*

  - Network CIDR: *192.168.10.0/24*

  - Enable DHCP: **Unchecked** (We will let Windows Server handle DNS/IP scope later).

## 🖥️ Phase 2: Deploying the Domain Controller (DC01)
### Step 1: Create the Virtual Machine
- In VirtualBox, click New.

- **Name:** *DC01*

- **Type:** Microsoft Windows | **Version:** Windows 2022 (64-bit)

- Allocate **4096 MB RAM** and **2 CPUs**.

- Attach the **Windows Server 2022 ISO** to the optical drive.

- Under **Network settings**, change Attachment to **NAT Network** (*AD-Lab-Net*)

### Step 2: Install Windows Server 2022
- Power on *DC01* and boot from the ISO.

- Select **Windows Server 2022 Standard Evaluation (Desktop Experience)** *Please select **"Desktop Experience"** or else ill be CLI*

- Complete the **custom installation**, select the primary disk partition, and let it finish.

- Set the Administrator password **(make sure to remember it!)**

## Step 3: Configure Static IP Address
Active Directory Domain Controllers must have static IP addresses.

- Open **Network Connections** *(ncpa.cpl)*.

- Right-click your **Ethernet adapter** > **Properties** > **IPv4 Properties**

- Configure the following static settings:

  - **IP Address:** 192.168.10.10

  - **Subnet Mask:** 255.255.255.0

  - **Default Gateway:** 192.168.10.1

  - **Preferred DNS Server:** 127.0.0.1 (or 192.168.10.10)
 
## Step 4: Promote Server to Domain Controller
- Open **Server Manager** > **Click Add Roles and Features**

- Select **Active Directory Domain Services (AD DS) and DNS Server**

- Proceed through wizard defaults and click Install.

- Once installed, click the yellow warning **flag at the top right of Server Manager** and select **Promote this server to a domain controller**

- Select **Add a new forest**:

  - **Root domain name**: *lab.local*

Set your Directory Services Restore Mode (DSRM) password.

Click **Next** through default prompts and hit **Install** Server will reboot automatically.

## 🏛️ Phase 3: Active Directory Organizational Units (OUs) & GPOs
Once *DC01* restarts, log in as *LAB\Administrator*

### Step 1: Build the OU Hierarchy
- Open **Active Directory Users and Computers** *(dsa.msc)*

- Right-click *lab.local* > **New** > **Organizational Unit**

- Create the following four OUs:

  - 💼 *Sales*

  - 🧮 *Accounting*

  - 👔 *Executive*

  - 🛡️ *IT*
 
  - 🖥️ *Workstation*

### Step 2: Configure Group Policy Objects (GPOs)
- Open **Group Policy Management** *(gpmc.msc)*

Expand *lab.local* > **Right-click Group Policy Objects** > **New**

Create distinct GPOs for **each OU** (e.g., Sales_Security_Policy, IT_Admin_Access).

Link each GPO directly to its respective Organizational Unit.

## 💻 Phase 4: Setting Up Client Workstations (USR02Pro & User01Ent)
*Repeat this process for both Windows 11 client Virtual Machines*

Step 1: Create Client VMs
  - *USR02Pro:* Windows 11 Pro **(2048 MB RAM minimum, 2 CPUs)**

  - *User01Ent:* Windows 11 Enterprise **(2048 MB RAM minimum, 2 CPUs)**

  - Network Settings: **Both attached to NAT Network** *(AD-Lab-Net)*

### Step 2: Set Client IP & DNS Settings
- Boot up the **Windows 11 client** and **Win + R** type *npca.cpl*

- Configure **static network configuration** pointing to *DC01*:

  - **IP Address** *(USR02Pro)*: 192.168.10.20

  - **IP Address** *(User01Ent)*: 192.168.10.30

  - **Subnet Mask**: 255.255.255.0

  - **Preferred DNS Server**: 192.168.10.10 **(Crucial: Must point to DC01 to resolve lab.local)**
 
### Step 3: Join Workstations to lab.local
- Open **Settings** > **System** > **About** (or Win + R, sysdm.cpl).

- Click **Advanced system settings** > **Computer Name tab** > **Change...**

- Select **Domain** and enter: *lab.local*

When prompted, authenticate with domain credentials *(LAB\Administrator)*

Reboot the workstation when prompted!

# 🎉 Congratulations! You Survived the Deployment
If you’ve made it this far without crying into your keyboard or accidentally wiping your home machine’s boot partition: hats off to you!

You are now the absolute ruler of *lab.local* You’ve officially earned the right to:

  - Blame DNS for every network glitch in a 5-mile radius.

  - Lock out imaginary employees in the Sales OU just to feel something.

  - Proudly watch your computer fans spin like a jet engine during take-off every time you boot all three VMs at once.

Go grab a coffee, stretch your legs, and enjoy the calm before we unleash SIEM telemetry, vulnerability scans, and simulated attacks onto this domain!
