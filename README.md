# 🖥️ Load Balanced Web Server Setup using VirtualBox, Ubuntu, HAProxy & Nginx

## 📌 About

A simple guide to set up a load-balanced web server system using:

- VirtualBox
- Ubuntu Server 24.04
- HAProxy (Load Balancer)
- Nginx (Web Servers)

Ideal for beginners, students, and home lab learners.

---

## 🧰 Requirements

- VirtualBox installed
- Ubuntu Server ISO
- 20GB+ Disk Space
- 8GB+ RAM

---

##🌍 Live Page:
Visit thsi page to see full articture and for future updates


---

## 🛠️ Setup Overview

1. Create 4 VMs: 1 Load Balancer + 3 Web Servers  
2. Assign static IPs using Netplan  
3. Install Nginx on Web Servers  
4. Install and configure HAProxy on Load Balancer  
5. Test with browser or curl  

---

## 🧱 Static IP Plan

| VM Name       | IP Address       |
|---------------|------------------|
| loadbalancer  | 192.168.56.10    |
| web1          | 192.168.56.11    |
| web2          | 192.168.56.12    |
| web3          | 192.168.56.13    |

---

## 🗺️ VM Structure

                                                    +-------------------+
                                                    |   Load Balancer   |
                                                    |   (HAProxy VM)    |
                                                    |   192.168.56.10   |
                                                    +--------+----------+
                                                             |
                                              +--------------+--------------+
                                              |              |              |
                                    +---------+----+ +-------+------+ +-----+--------+
                                   | Web Server 1  | | Web Server 2 | | Web Server 3  |
                                   |   (Nginx)     | |   (Nginx)    | |    (Nginx)    |
                                   | 192.168.56.11 | | 192.168.56.12| | 192.168.56.13 |
                                    +--------------+ +--------------+ +--------------+

  ---

## 🌐 HAProxy Config Example

```haproxy
frontend http_front
    bind *:80
    default_backend http_back

backend http_back
    balance roundrobin
    server web1 192.168.56.11:80 check
    server web2 192.168.56.12:80 check
    server web3 192.168.56.13:80 check
```
## 🔧 Sample Netplan Configuration
```yaml
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [10.2.2.50/24]
      routes:
        - to: 0.0.0.0/0
          via: 192.X.X.XX
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]

    enp0s8:
      dhcp4: no
      addresses: [192.168.56.11/24]
```
📌 Replace IPs accordingly on each VM.
---
## 🔍 Testing Setup
To test the load balancing:

On a browser or terminal (curl):
```
curl http://192.168.56.10
```
You should get rotating responses from Web Server 1, 2, and 3 (round-robin)

Example HTML content (/var/www/html/index.html):
```html
<h1>Welcome from Web Server 1</h1>
<p>Server IP: 192.168.56.11</p>
```
---
## 🌐 Project Goals

- Simulate real-world load balancing on your local system

- Learn basic networking with VirtualBox (host-only + bridged)

- Deploy static or dynamic content with Nginx

- Route and balance requests using HAProxy

✅ You can also use this guide as a reference to implement the same setup on real hardware (e.g. old PCs, Raspberry Pi, or cloud VMs)


---
## 👨‍💻 Author
Made with ❤️ by [Rishabh Aka Raiplus]

This repo is open-source. Feel free to fork, learn, or contribute!




