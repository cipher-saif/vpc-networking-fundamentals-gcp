```

██╗░░░██╗██╗██████╗░████████╗██╗░░░██╗░█████╗░██╗░░░░░  
██║░░░██║██║██╔══██╗╚══██╔══╝██║░░░██║██╔══██╗██║░░░░░  
╚██╗░██╔╝██║██████╔╝░░░██║░░░██║░░░██║███████║██║░░░░░  
░╚████╔╝░██║██╔══██╗░░░██║░░░██║░░░██║██╔══██║██║░░░░░  
░░╚██╔╝░░██║██║░░██║░░░██║░░░╚██████╔╝██║░░██║███████╗  
░░░╚═╝░░░╚═╝╚═╝░░╚═╝░░░╚═╝░░░░╚═════╝░╚═╝░░╚═╝╚══════╝  

██████╗░██████╗░██╗██╗░░░██╗░█████╗░████████╗███████╗  ░█████╗░██╗░░░░░░█████╗░██╗░░░██╗██████╗░░░░
██╔══██╗██╔══██╗██║██║░░░██║██╔══██╗╚══██╔══╝██╔════╝  ██╔══██╗██║░░░░░██╔══██╗██║░░░██║██╔══██╗░░░
██████╔╝██████╔╝██║╚██╗░██╔╝███████║░░░██║░░░█████╗░░  ██║░░╚═╝██║░░░░░██║░░██║██║░░░██║██║░░██║░░░
██╔═══╝░██╔══██╗██║░╚████╔╝░██╔══██║░░░██║░░░██╔══╝░░  ██║░░██╗██║░░░░░██║░░██║██║░░░██║██║░░██║░░░
██║░░░░░██║░░██║██║░░╚██╔╝░░██║░░██║░░░██║░░░███████╗  ╚█████╔╝███████╗╚█████╔╝╚██████╔╝██████╔╝██╗
╚═╝░░░░░╚═╝░░╚═╝╚═╝░░░╚═╝░░░╚═╝░░╚═╝░░░╚═╝░░░╚══════╝  ░╚════╝░╚══════╝░╚════╝░░╚═════╝░╚═════╝░╚═╝
```

<div align="center">

# VPC Networking Fundamentals — Cloud Network Security & Traffic Analysis

*Virtual private cloud design, firewall rule analysis, and internal vs external traffic testing on GCP*

</div>

---

&nbsp;

```
═══════════════════════════════════════════════════════
𝐎𝐕𝐄𝐑𝐕𝐈𝐄𝐖
═══════════════════════════════════════════════════════
```

This project demonstrates the design and analysis of a Virtual Private Cloud (VPC) on Google Cloud Platform. Two virtual machine instances were deployed within the same network to examine how cloud firewall rules govern traffic, how internal and external communication behaves, and how secure network design principles apply in a real cloud environment.

The work covers east–west traffic (internal VM-to-VM), north–south traffic (external public access), firewall rule evaluation, and subnet architecture — building a practical foundation in cloud network security.

&nbsp;

---

```
═══════════════════════════════════════════════════════
𝐎𝐁𝐉𝐄𝐂𝐓𝐈𝐕𝐄𝐒
═══════════════════════════════════════════════════════
```

- Design and configure a cloud-based Virtual Private Cloud (VPC) on GCP
- Deploy and manage virtual machine instances within the network
- Analyze and understand cloud firewall rules and ingress traffic control
- Test and compare internal (east–west) and external (north–south) network traffic
- Validate firewall rule enforcement and stateful traffic behavior
- Build foundational skills in cloud networking and security-first design

&nbsp;

---

```
═══════════════════════════════════════════════════════
𝐓𝐎𝐎𝐋𝐒  &  𝐓𝐄𝐂𝐇𝐍𝐎𝐋𝐎𝐆𝐈𝐄𝐒
═══════════════════════════════════════════════════════
```

![GCP](https://img.shields.io/badge/Google_Cloud_Platform-4285F4?style=flat&logo=googlecloud&logoColor=white)
![VPC](https://img.shields.io/badge/VPC_Networks-34A853?style=flat&logo=googlecloud&logoColor=white)
![Compute](https://img.shields.io/badge/Compute_Engine-EA4335?style=flat&logo=googlecloud&logoColor=white)
![Firewall](https://img.shields.io/badge/Firewall_Rules-black?style=flat)
![Linux](https://img.shields.io/badge/Linux_CLI-FCC624?style=flat&logo=linux&logoColor=black)

&nbsp;

---

```
═══════════════════════════════════════════════════════
𝐏𝐑𝐎𝐉𝐄𝐂𝐓  𝐒𝐓𝐑𝐔𝐂𝐓𝐔𝐑𝐄
═══════════════════════════════════════════════════════
```

```
vpc-networking-fundamentals-gcp/
│── README.md
│── Report/
│   └── VPC_Networking_Fundamentals___Cloud_Network_Security___Traffic_Analysis.pdf
│── Screenshots/
│   ├── firewall-rules.jfif
│   ├── subnets.jfif
│   ├── vm1-external-ip-ping-vm2.jfif
│   ├── vm1-internal-ip-ping-vm2.jfif
│   ├── vm1-ipaddr.jfif
│   ├── vm2-internal-ip-ping-vm1.jfif
│   ├── vm2-ipaddr.jfif
│   ├── vm-instances-internal-and-external-ip-addr.jfif
│   ├── vm-instances.jfif
│   └── vm-metrics.jfif
```

&nbsp;

---

```
═══════════════════════════════════════════════════════
𝐏𝐑𝐎𝐉𝐄𝐂𝐓  𝐀𝐑𝐂𝐇𝐈𝐓𝐄𝐂𝐓𝐔𝐑𝐄
═══════════════════════════════════════════════════════
```

The network environment was constructed as follows:

```
Default VPC Network (Auto-Mode)
│
├── Subnets — auto-provisioned per region with private IP ranges
│
├── vm-1  →  Internal IP: 10.142.0.2  |  External IP: 35.185.14.163
└── vm-2  →  Internal IP: 10.142.0.3  |  External IP: 34.23.165.49

Firewall Rules Applied:
├── default-allow-icmp      →  Allow ICMP (ping)          Priority: 65534
├── default-allow-ssh       →  Allow TCP:22 (SSH)          Priority: 65534
├── default-allow-rdp       →  Allow TCP:3389 (RDP)        Priority: 65534
└── default-allow-internal  →  Allow all internal traffic  Priority: 65534
```

&nbsp;

---

```
═══════════════════════════════════════════════════════
𝐌𝐄𝐓𝐇𝐎𝐃𝐎𝐋𝐎𝐆𝐘
═══════════════════════════════════════════════════════
```

&nbsp;

### Step 1 — VPC Network Creation

An auto-mode VPC network was created to provision subnets automatically across all GCP regions. Each subnet received a private IPv4 range and inherited default firewall rules at the network level, establishing a secure baseline for all connected resources.

&nbsp;

### Step 2 — Virtual Machine Deployment

Two Compute Engine instances were deployed within the same VPC network in the `us-east1-c` zone. Each VM was assigned both an internal IP for private intra-network communication and an external IP for public access and traffic testing.

&nbsp;

### Step 3 — Firewall Rules Analysis

Default ingress firewall rules were examined across the VPC. Rules are stateful, evaluated by priority, and enforced at the network level. The following were analyzed:

| Rule | Protocol | Port | Action | Priority |
|---|---|---|---|---|
| default-allow-icmp | ICMP | — | Allow | 65534 |
| default-allow-ssh | TCP | 22 | Allow | 65534 |
| default-allow-rdp | TCP | 3389 | Allow | 65534 |
| default-allow-internal | TCP/UDP/ICMP | All | Allow | 65534 |

&nbsp;

### Step 4 — Internal Traffic Testing (East–West)

VM-to-VM communication was tested using the internal IP address of each instance. Traffic remained entirely within the private VPC — no public internet routing was involved.

```bash
ping <internal-ip>
```

Both VMs successfully responded to ICMP requests via their internal addresses, confirming correct east–west traffic behavior within the VPC.

&nbsp;

### Step 5 — External Traffic Testing (North–South)

Connectivity was tested using the external IP address of the second VM to simulate north–south traffic — traffic entering or leaving the cloud network boundary.

```bash
ping <external-ip>
```

The test confirmed that external access is dependent on firewall rules permitting ICMP ingress, and that public-facing resources carry a higher exposure surface than internal-only instances.

&nbsp;

### Step 6 — Security Observations & Analysis

Key security findings from the testing and analysis:

- Internal traffic is faster, more efficient, and inherently more secure than external traffic
- GCP firewall rules are stateful — return traffic is automatically permitted
- Firewall rules are applied at the VPC level and affect all instances within the network
- Public-facing resources should be minimized in line with least-privilege networking principles
- Default rules provide a functional baseline but should be reviewed and tightened for production environments

&nbsp;

---

```
═══════════════════════════════════════════════════════
𝐑𝐄𝐒𝐔𝐋𝐓𝐒  &  𝐒𝐂𝐑𝐄𝐄𝐍𝐒𝐇𝐎𝐓𝐒
═══════════════════════════════════════════════════════
```

&nbsp;

<div align="center">
<table border="1" cellpadding="16" cellspacing="0">
<tr>
<td align="center">
<img src="Screenshots/vm-instances (internal & external ip addr).jfif" width="780"/>
<br/><br/>
<b>𝗙𝗶𝗴. 𝟭 &nbsp;·&nbsp; VM Instances — Internal & External IP Addresses</b><br/>
<sub>Both virtual machine instances listed with their assigned internal and external IP addresses. vm-1 is assigned <code>10.142.0.2</code> internally and <code>35.185.14.163</code> externally; vm-2 is assigned <code>10.142.0.3</code> and <code>34.23.165.49</code>.</sub>
</td>
</tr>
</table>
</div>

&nbsp;

<div align="center">
<table border="1" cellpadding="16" cellspacing="0">
<tr>
<td align="center">
<img src="Screenshots/vm-instances.jfif" width="780"/>
<br/><br/>
<b>𝗙𝗶𝗴. 𝟮 &nbsp;·&nbsp; VM Instances — Compute Engine Overview</b><br/>
<sub>The Compute Engine VM instances dashboard showing both vm-1 and vm-2 deployed in the <code>us-east1-c</code> zone, each with SSH access enabled and running within the default VPC network.</sub>
</td>
</tr>
</table>
</div>

&nbsp;

<div align="center">
<table border="1" cellpadding="16" cellspacing="0">
<tr>
<td align="center">
<img src="Screenshots/subnets.jfif" width="780"/>
<br/><br/>
<b>𝗙𝗶𝗴. 𝟯 &nbsp;·&nbsp; VPC Subnet Details</b><br/>
<sub>The auto-mode VPC subnet list showing automatically provisioned subnets across multiple GCP regions, each assigned a distinct private IPv4 range under the default network.</sub>
</td>
</tr>
</table>
</div>

&nbsp;

<div align="center">
<table border="1" cellpadding="16" cellspacing="0">
<tr>
<td align="center">
<img src="Screenshots/firewall-rules.jfif" width="780"/>
<br/><br/>
<b>𝗙𝗶𝗴. 𝟰 &nbsp;·&nbsp; Firewall Rules List</b><br/>
<sub>Default ingress firewall rules configured on the VPC, including <code>default-allow-icmp</code>, <code>default-allow-ssh</code>, <code>default-allow-rdp</code>, and <code>default-allow-internal</code>, all at priority 65534.</sub>
</td>
</tr>
</table>
</div>

&nbsp;

<div align="center">
<table border="1" cellpadding="16" cellspacing="0">
<tr>
<td align="center">
<img src="Screenshots/vm1-ipaddr.jfif" width="780"/>
<br/><br/>
<b>𝗙𝗶𝗴. 𝟱 &nbsp;·&nbsp; VM-1 IP Address</b><br/>
<sub>Terminal output from vm-1 confirming its assigned internal IP address via the SSH-in-browser session, used as a reference for subsequent internal traffic testing.</sub>
</td>
</tr>
</table>
</div>

&nbsp;

<div align="center">
<table border="1" cellpadding="16" cellspacing="0">
<tr>
<td align="center">
<img src="Screenshots/vm2-ipaddr.jfif" width="780"/>
<br/><br/>
<b>𝗙𝗶𝗴. 𝟲 &nbsp;·&nbsp; VM-2 IP Address</b><br/>
<sub>Terminal output from vm-2 confirming its assigned internal IP address, used as the target for internal ping tests initiated from vm-1.</sub>
</td>
</tr>
</table>
</div>

&nbsp;

<div align="center">
<table border="1" cellpadding="16" cellspacing="0">
<tr>
<td align="center">
<img src="Screenshots/vm1-internal-ip-ping-vm2.jfif" width="780"/>
<br/><br/>
<b>𝗙𝗶𝗴. 𝟳 &nbsp;·&nbsp; VM-1 — Internal IP Ping to VM-2</b><br/>
<sub>Successful ICMP ping from vm-1 to vm-2 using the internal IP address, confirming east–west traffic behavior within the private VPC network with no public internet routing involved.</sub>
</td>
</tr>
</table>
</div>

&nbsp;

<div align="center">
<table border="1" cellpadding="16" cellspacing="0">
<tr>
<td align="center">
<img src="Screenshots/vm2-internal-ip-ping-vm1.jfif" width="780"/>
<br/><br/>
<b>𝗙𝗶𝗴. 𝟴 &nbsp;·&nbsp; VM-2 — Internal IP Ping to VM-1</b><br/>
<sub>Successful ICMP ping from vm-2 to vm-1 via internal IP, validating bidirectional east–west connectivity within the VPC subnet.</sub>
</td>
</tr>
</table>
</div>

&nbsp;

<div align="center">
<table border="1" cellpadding="16" cellspacing="0">
<tr>
<td align="center">
<img src="Screenshots/vm1-external-ip-ping-vm2.jfif" width="780"/>
<br/><br/>
<b>𝗙𝗶𝗴. 𝟵 &nbsp;·&nbsp; VM-1 — External IP Ping to VM-2</b><br/>
<sub>ICMP ping from vm-1 to vm-2 using the external IP address, demonstrating north–south traffic behavior and confirming that firewall rules permit ICMP ingress from external sources.</sub>
</td>
</tr>
</table>
</div>

&nbsp;

<div align="center">
<table border="1" cellpadding="16" cellspacing="0">
<tr>
<td align="center">
<img src="Screenshots/vm-metrics.jfif" width="780"/>
<br/><br/>
<b>𝗙𝗶𝗴. 𝟭𝟬 &nbsp;·&nbsp; VM Metrics</b><br/>
<sub>Compute Engine metrics dashboard showing resource utilization across both VM instances during the testing period, providing visibility into network and CPU activity generated by the traffic tests.</sub>
</td>
</tr>
</table>
</div>

&nbsp;

---

```
═══════════════════════════════════════════════════════
𝐂𝐎𝐌𝐌𝐀𝐍𝐃𝐒  𝐔𝐒𝐄𝐃
═══════════════════════════════════════════════════════
```

**Internal IP ping (east–west traffic test):**
```bash
ping <internal-ip>
```

**External IP ping (north–south traffic test):**
```bash
ping <external-ip>
```

**Example — VM-1 pinging VM-2 internally:**
```bash
student-00-d0e591c0bece@vm-1:~$ ping vm-2
PING vm-2.us-east1-c.c.qwiklabs-gcp-00-3efabebbe55f.internal (10.142.0.3) 56(84) bytes of data.
64 bytes from vm-2...: icmp_seq=1 ttl=64 time=1.49 ms
```

**Example — VM-1 pinging VM-2 externally:**
```bash
student-00-d0e591c0bece@vm-1:~$ ping 34.23.165.49
PING 34.23.165.49 (34.23.165.49) 56(84) bytes of data.
```

&nbsp;

---

```
═══════════════════════════════════════════════════════
𝐃𝐎𝐂𝐔𝐌𝐄𝐍𝐓𝐀𝐓𝐈𝐎𝐍
═══════════════════════════════════════════════════════
```

[Download Full Report](Report/VPC_Networking_Fundamentals___Cloud_Network_Security___Traffic_Analysis.pdf)

&nbsp;

---

```
═══════════════════════════════════════════════════════
𝐂𝐎𝐍𝐂𝐋𝐔𝐒𝐈𝐎𝐍
═══════════════════════════════════════════════════════
```

This project successfully implemented and analyzed a Virtual Private Cloud environment on Google Cloud Platform, demonstrating core network security concepts through hands-on testing. Internal and external traffic behaviors were validated across two VM instances, firewall rule enforcement was confirmed, and the security implications of east–west versus north–south traffic were documented.

The outcomes reflect real-world cloud network design requirements: isolating resources within private subnets, enforcing least-privilege firewall rules, and minimizing public exposure. These fundamentals form the foundation of secure cloud architecture in enterprise environments.

&nbsp;

---

<div align="center">

Developed as part of a personal cloud security portfolio project

</div>
