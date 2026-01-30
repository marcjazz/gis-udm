# Session 5: Virtual Network Modes in Hypervisors

This course introduces virtual machine (VM) networking concepts commonly used in hypervisors such as VirtualBox and VMware. It combines theory, comparisons, hands-on labs, and validation activities.

---

## 1. Theory Lesson: Virtual Network Modes Overview

Virtual machines behave like separate computers, but their network connection depends on how the hypervisor links them to the host and the outside world. Think of the hypervisor as a smart switchboard deciding where VM traffic can go.

### 1.1 NAT (Network Address Translation)

**How it works**
The hypervisor acts like a home router. The VM sits on a private network and shares the host’s IP address to reach the internet.

**Analogy**
A phone using Wi-Fi at home. The phone has a private address, but the router represents it to the internet.

- **Diagram (conceptual)**

```
    [ VM ] --private IP--> [ Hypervisor NAT ] --public IP--> Internet
```

- **Key characteristics**

* VM gets a private IP from the hypervisor
* Outbound internet access works automatically
* External devices cannot directly reach the VM

**Practical use case**
Safely browsing the internet or installing updates inside a VM without exposing it to the local network.

---

### 1.2 Bridged Networking

**How it works**
The VM connects directly to the physical network, appearing as another device on the LAN.

**Analogy**
Plugging an extra laptop into the same switch as your PC.

- **Diagram (conceptual)**

```
[ VM ] --LAN--> [ Switch / Router ] --LAN--> Other devices
```

- **Key characteristics**

* VM receives an IP from the same DHCP server as the host
* Full access to LAN and internet
* Other devices can see and reach the VM

**Practical use case**
Hosting a web or game server that must be reachable by other machines on the network.

---

### 1.3 Host-Only Networking

**How it works**
The VM and host form a private network that does not connect to the internet.

**Analogy**
A private Ethernet cable directly between two computers.

- **Diagram (conceptual)**

```
[ Host ] <----private LAN----> [ VM ]
```

- **Key characteristics**

* Private IP addresses assigned by the hypervisor
* No internet access by default
* VM can communicate with the host

**Practical use case**
Testing software or services that should only be accessed from the host machine.

---

### 1.4 Internal Networking

**How it works**
VMs communicate only with each other on an isolated virtual network.

**Analogy**
A closed lab room where students can talk to each other but not to anyone outside.

- **Diagram (conceptual)**

```
[ VM1 ] <---> [ VM2 ] <---> [ VM3 ]
        (no host, no internet)
```

- **Key characteristics**

* No host or internet connectivity
* Manual or internal DHCP IP assignment
* Completely isolated environment

**Practical use case**
Practicing network attacks and defenses in a safe, isolated lab.

---

### 1.5 Advanced Networking Concepts

#### NAT Network (NAT Service)

Unlike simple NAT where each VM is isolated, a **NAT Network** allows multiple VMs to share the same NAT gateway and communicate with each other while still being hidden from the external LAN.

#### Port Forwarding

Even in NAT mode, you can make a VM service (like a web server on port 80) reachable from the host by mapping a host port (e.g., 8080) to the VM port.

- **Example:** Accessing a VM web server via `http://localhost:8080` from the host's browser.

#### Promiscuous Mode

In Bridged or Internal networks, setting an adapter to **Promiscuous Mode** allows the VM to "see" all traffic on the virtual switch, not just traffic destined for its own MAC address. This is essential for running network sniffers like Wireshark or IDS (Intrusion Detection Systems).

---

## 2. Use Cases and Comparisons

### Comparison Table

| Feature                | NAT             | Bridged       | Host-Only       | Internal                |
| ---------------------- | --------------- | ------------- | --------------- | ----------------------- |
| IP Assignment          | Hypervisor DHCP | LAN DHCP      | Hypervisor DHCP | Manual or internal DHCP |
| Internet Access        | Yes (outbound)  | Yes           | No (by default) | No                      |
| Visible to Host        | Limited         | Yes           | Yes             | No                      |
| VM-to-VM Communication | Limited         | Yes (via LAN) | Yes             | Yes                     |
| Security Level         | High            | Low           | Medium          | Very High               |

**Security notes**

- NAT hides VMs from the LAN, reducing attack surface.
- Bridged mode exposes VMs like real machines and must be secured.
- Host-Only allows controlled testing without outside interference.
- Internal is safest for experiments involving risky configurations.

---

## 3. Lab: VM Network Configuration

### Lab Objective

Configure two virtual machines with different networking modes and observe behavior.

### Requirements

- Two VMs (VM1 and VM2)
- Linux or Windows operating systems
- VirtualBox or VMware

---

### Step 1: Configure VM1 (Host-Only)

1. Power off VM1
2. Open VM settings
3. Go to Network
4. Select **Host-Only Adapter**
5. Save settings and start VM1

**Expected IP range**

- Example: 192.168.56.x

---

### Step 2: Configure VM2 (Bridged)

1. Power off VM2
2. Open VM settings
3. Go to Network
4. Select **Bridged Adapter**
5. Choose active network interface (Ethernet or Wi-Fi)
6. Start VM2

---

### Step 3: Advanced Lab Task - Port Forwarding (NAT)

1. Set VM1 to **NAT** mode.
2. Go to `Advanced > Port Forwarding`.
3. Add a rule: `Name: Web, Protocol: TCP, Host Port: 8080, Guest Port: 80`.
4. Inside the VM, ensure a web server is running.
5. On the host browser, navigate to `http://localhost:8080`.

---

## 4. Network Verification & Troubleshooting

### Verification Commands

**Check IP address**

- Windows: `ipconfig`
- Linux/macOS: `ifconfig` or `ip addr`

**Check connectivity**

- `ping <host IP>`
- `ping <gateway>`

**View routes**

- Windows: `route print`
- Linux: `ip route`

**Identify Listening Ports**

- Linux: `ss -tulpn` or `netstat -plnt`
- Windows: `netstat -ano | findstr LISTENING`

---

## 5. Knowledge Check & Review

### Multiple Choice Questions

1. Which mode hides the VM behind the host’s IP?
   - A. Bridged
   - B. NAT
   - C. Host-Only
   - D. Internal

2. Which mode allows other LAN devices to access the VM?
   - A. NAT
   - B. Internal
   - C. Bridged
   - D. Host-Only

3. Which mode is best for isolated multi-VM labs?
   - A. Bridged
   - B. NAT
   - C. Host-Only
   - D. Internal

4. Which network mode allows VM-to-host communication without internet?
   - A. NAT
   - B. Host-Only
   - C. Bridged
   - D. Internal

5. Which mode has the highest exposure risk?
   - A. Internal
   - B. Host-Only
   - C. NAT
   - D. Bridged
