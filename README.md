# Enterprise Network

## 📌 What is this project?
I built a complete, mid-sized company network from scratch using **Cisco Packet Tracer**. 

Instead of just hooking a couple of computers up to a home router, I built a corporate-grade network with a **spiderweb design (Full Mesh)**. This ensures that if any single switch catches fire or a cable gets cut by accident, the network stays online because the data can automatically find another path around the web.
<img width="945" height="370" alt="ntw" src="https://github.com/user-attachments/assets/f9de9ef4-94dc-4acc-b588-25dfd113e7cc" />

---

## 🛠️ The Simple Breakdown of How It Works

### 1. The Spiderweb Layout (Redundancy)
* **What I did:** I used 2 Routers at the top, 2 Layer 3 "Core" Switches (the 3D cubes) in the middle, and 2 standard switches at the bottom. I criss-crossed the cables so everything connects to everything.
* **Why it matters:** If one of the main switches crashes, the backup switch instantly takes over.

### 2. Department Locked Rooms (VLANs)
* **What I did:** I split the network into separate digital rooms. For example, HR is on its own private island away from regular internet traffic.
* **Why it matters:** This is basic cybersecurity. A regular employee shouldn't be able to snoop on HR payroll data.

### 3. Automatic Magic IPs (DHCP)
* **What I did:** I added a physical Server to the network and turned the DHCP service ON. 
* **Why it matters:** In a big company, you can't manually type network settings into 5,000 computers. This server automatically hands out IP addresses to any computer that plugs into the wall.

### 4. Making the Routers Talk (OSPF)
* **What I did:** I turned on a language called OSPF on all the routers and core switches.
* **Why it matters:** This forces the routers to talk to each other, build a live map of the network, and calculate the fastest path to send data.

### 5. The Passport Office (NAT)
* **What I did:** I set up NAT on the edge routers.
* **Why it matters:** Private company IP addresses (like `10.0.x.x`) are legally banned on the public internet. NAT acts like a passport office, translating the private office IPs into a public IP so employees can browse Google.

---

## 🔍 Mistakes I Made & How I Fixed Them (Troubleshooting Logs)

Building this wasn't perfect! Here are the exact roadblocks I ran into and how I solved them:

### ❌ Mistake 1: The OSPF "No Identity" Error
* **The Problem:** When I tried to turn on the router language using `router ospf 1`, the router yelled at me: `OSPF process 1 cannot start. There must be at least one "up" IP interface`.
* **What I learned:** The router was trying to start a conversation but didn't even know its own name yet! 
* **The Fix:** I had to give the router's physical port an IP address first (`10.0.1.1`) and wake it up using the `no shutdown` command. Once it had an identity, OSPF turned on perfectly.

### ❌ Mistake 2: The Guest Mode & Frozen Screen Trap
* **The Problem:** I tried typing setup commands, but the router kept saying `Invalid input detected`. Then, I typed `no shutdown` and the whole screen froze with a message saying `Translating "no"...domain server`.
* **What I learned:** I was trying to change system settings while logged into the "Guest Account" (`Router>`). Because the router didn't understand my command, it thought I was typing a website URL and froze trying to look it up on the internet.
* **The Fix:** First, I pressed **`Ctrl + Shift + 6`** on my keyboard to forcefully unfreeze the screen. Then, I properly climbed up to the Admin Account by typing **`enable`** and **`configure terminal`**. Once the prompt changed to `Router(config)#`, my commands worked flawlessly.
<img width="591" height="200" alt="error" src="https://github.com/user-attachments/assets/6ab0de42-ef69-4298-b14b-e695c10e6731" />
<img width="677" height="649" alt="fix router 0" src="https://github.com/user-attachments/assets/9793a79a-4727-4ba0-9978-0eba1cd296a3" />

### ❌ Mistake 3: The Wrong Blue Cable
* **The Problem:** I initially wired my employee PC to a switch using a light-blue console cable, and it couldn't talk to the network.
* **What I learned:** Light-blue console cables are only for programming a box out of the box. They cannot carry regular internet data.
* **The Fix:** I deleted the blue wire and used a standard solid black **Copper Straight-Through cable** instead.
