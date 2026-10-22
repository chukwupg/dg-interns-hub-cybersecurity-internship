# VM Networking Modes (VMware Workstation)

## Comparison

| Mode | VM - VM | VM - Host | VM - Internet | Internet / LAN - VM | When to use it |
|---|---|---|---|---|---|
| **NAT** | No (each VM is on its own private network) | No (unless port forwarding) | Yes, through the host | No (unless port forwarding) | A single VM that just needs internet access, for updates or browsing. Default mode |
| **NAT Network** | Yes (all VMs on the same virtual network) | No by default (port forwarding needed) | Yes, through the host | No (unless port forwarding) | A multi-VM lab where machines must talk to each other **and** get updates |
| **Host-only** | Yes | Yes | **No** | No | Fully isolated labs, malware analysis, intentionally vulnerable machines |
| **Bridged** | Yes | Yes | Yes | **Yes**, the VM gets an address on the real network | When a VM must behave like a real device on your LAN, such as a test server others need to reach |

## Why vulnerable labs must never be bridged
- In bridged mode, the VM sits on your **real network** like any other device. Everyone else on that network can reach it.
- An **intentionally vulnerable machine** (or one infected with malware) can then be attacked or used as a foothold into real devices such as phones, laptops and smart devices.
- Attack tools in a Kali VM can also hit real devices by accident. That could be **illegal** if you do not have permission.
- If your router forwards ports or the network is public (campus, café, hotel), the exposure can reach the internet.
- Isolated modes (Host-only or NAT Network) contain the lab, so mistakes and malware stay inside.

## Practical tips
- Use **NAT Network** when you need updates and VM-to-VM communication. Use **Host-only** when you want complete isolation.
- A common pattern: update the VMs under NAT Network first, then switch the vulnerable ones to Host-only.
- Take a snapshot before testing anything risky.

## My lab
- **Mode used:** Custom Host-only network (VMnet3).
- **Why:** To create an isolated network for learning without affecting my host machine.
- **Subnet:** 192.168.98.0/24
- **Gateway:** 192.168.98.1

### Lab Network Diagram

![Network Diagram](/Findings/Network%20Map%20and%20Diagram/network-diagram.png)