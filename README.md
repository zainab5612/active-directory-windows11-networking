# Windows Server 2022 and Windows 11 Setup

I built this setup in VirtualBox to get more hands-on experience with Windows administration, networking, Active Directory, and troubleshooting.

The environment includes:
- Windows Server 2022
- Windows 11 Pro
- Active Directory
- Remote Desktop
- internal VM networking

The goal was to better understand how Windows domain environments work and how systems communicate inside a business network.

---

## Initial Setup

I started by creating two virtual machines in Oracle VirtualBox:
- Windows Server 2022
- Windows 11 Pro

During installation, I ran into several issues while setting up the virtual machines. One of the first problems was related to boot errors and the VM not properly detecting the Windows ISO file. I spent time troubleshooting storage settings, EFI configuration, and boot options before getting the installations working correctly.

I also installed VirtualBox Guest Additions to improve:
- screen resizing
- clipboard sharing
- shared folders
- overall VM usability

---

## Networking Configuration

Both virtual machines were configured using:
- NAT adapter for internet access
- Internal Network adapter for communication between systems

At first, I thought using NAT alone would allow both virtual machines to communicate directly. After troubleshooting ping failures and connectivity problems, I learned that the internal adapter was necessary for private communication between the systems.

I configured static IP addresses manually for both machines.

| Machine | IP Address | DNS Server |
|---|---|---|
| Windows Server 2022 | 192.168.10.10 | 192.168.10.10 |
| Windows 11 Pro | 192.168.10.20 | 192.168.10.10 |

One issue I spent a while troubleshooting was that the Windows 11 machine could not join the domain. Eventually I realized the DNS server on the Windows 11 machine needed to point to the Domain Controller itself in order for Active Directory communication to work properly.

Once the DNS configuration was corrected, the Windows 11 machine was able to join the domain successfully.

---

## Active Directory Configuration

On the Windows Server machine, I installed Active Directory Domain Services (AD DS) and configured the server as a Domain Controller.

Using Active Directory Users and Computers, I practiced:
- creating domain users
- resetting passwords
- unlocking locked accounts
- disabling and enabling accounts
- modifying user properties

I also tested domain authentication by logging into the Windows 11 machine using user accounts created through Active Directory.

This helped me better understand how centralized user management works in enterprise Windows environments.

---

## Joining Windows 11 to the Domain

After configuring networking and DNS settings correctly, I joined the Windows 11 Pro machine to the Active Directory domain using domain administrator credentials.

Once joined successfully:
- domain users could authenticate on the Windows 11 machine
- communication between both systems improved
- centralized account management became possible

I verified the domain connection by logging into Windows 11 using accounts created inside Active Directory.

---

## Remote Desktop Configuration

After the domain setup was working, I enabled Remote Desktop on the server and connected to it remotely from the Windows 11 machine.

At first I encountered several Remote Desktop issues related to:
- permissions
- existing console sessions
- VM communication problems

One issue that confused me initially was receiving Remote Desktop errors even though both machines could communicate over the network. After troubleshooting, I realized the problem was related to Remote Desktop permissions and authentication rather than networking itself.

After adjusting the settings and testing different accounts, I was able to remotely connect to and manage the server successfully.

---

## Problems I Troubleshot

Some issues I encountered and worked through during this setup included:
- UEFI boot problems during Windows installation
- VM communication failures
- incorrect DNS configuration preventing domain joining
- Remote Desktop authorization errors
- internal network adapter configuration issues
- ping and connectivity problems between systems
- Remote Desktop session conflicts

Working through these problems helped me better understand:
- Windows networking
- DNS communication
- Active Directory authentication
- Remote Desktop configuration
- troubleshooting in virtualized environments

---

## Skills Practiced

- Windows Server administration
- Active Directory management
- User account administration
- DNS configuration
- Remote Desktop configuration
- Virtual machine networking
- Windows troubleshooting
- Enterprise environment setup
- Internal network communication
- VirtualBox configuration

---

## Screenshots

### 1. VirtualBox VM Setup
Created two virtual machines in Oracle VirtualBox for the server and client environment. Both systems were configured with NAT and Internal Network adapters for internet access and internal communication.
<img width="700" height="800" alt="image" src="https://github.com/user-attachments/assets/08c3f2b0-bc5a-405b-a557-4b7e320e20d2" />
<img width="450" height="310" alt="image" src="https://github.com/user-attachments/assets/a64bd002-3a6c-4882-8f9c-f24bfe8ce566" />
<img width="450" height="310" alt="image" src="https://github.com/user-attachments/assets/75db746f-7783-483d-834e-d6e2b4518329" />

---

### 2. Active Directory Users and Computers
Used Active Directory Users and Computers along with the net user /domain command to verify domain account information and practice basic user administration tasks inside the domain environment.
<img width="730" height="506" alt="image" src="https://github.com/user-attachments/assets/b5059a2d-6042-4ae4-8b8b-73ed7cbaeab8" />
<img width="947" height="503" alt="image" src="https://github.com/user-attachments/assets/d11fcbd5-cb21-414d-af5f-68e261d68d29" />

---

### 3. shared folder with VirtualBox guest addition
Configured shared folders using VirtualBox Guest Additions to allow file sharing between the host machine and virtual machines. This improved file transfer and overall usability while working inside the virtual environment.
<img width="597" height="406" alt="image" src="https://github.com/user-attachments/assets/8b159c5f-cf8c-4f47-89d7-c7fb7e02182a" />

---

### 4. Successful Domain Join
Successfully joined the Windows 11 machine to the Active Directory domain using domain administrator credentials after correcting DNS configuration issues.
domain (homelab.com)
<img width="787" height="453" alt="image" src="https://github.com/user-attachments/assets/ab5e92da-4c09-4dfd-a898-12344d143b52" />
---

### 5. Successful Communication Between Virtual Machines
Verified communication between the Windows 11 machine and the server using ping tests after configuring static IP addresses and internal networking.
<img width="800" height="801" alt="image" src="https:/zz/github.com/user-attachments/assets/9a209eff-de1e-4430-8ac0-d0666c2cf974" />
<img width="800" height="801" alt="image" src="https://github.com/user-attachments/assets/ee77b83a-acb4-4bcf-91f7-c45dfc7a64dc" />

---

### 6. Remote Desktop Connection
Successfully connected to the Windows Server machine remotely from the Windows 11 client using Remote Desktop after troubleshooting permission and authentication issues.
<img width="949" height="794" alt="image" src="https://github.com/user-attachments/assets/a48999ce-8444-4a41-96aa-9bdc23a1a322" />

---

### 7. IP Configuration
Configured static IP addresses for both NAT and Internal Network adapters and assigned the Domain Controller as the DNS server to support Active Directory communication and domain joining.
<img width="394" height="455" alt="Screenshot 2026-05-07 171643" src="https://github.com/user-attachments/assets/73142fa4-8f23-4d8e-89eb-2bd350de1aa3" />
<img width="399" height="455" alt="Screenshot 2026-05-07 172005" src="https://github.com/user-attachments/assets/b9c91afa-3b59-4a41-99f7-52df0c3fcdd2" />



