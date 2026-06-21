# My Journey to Building My Dream Homelab
> 3 Nodes, Dual-WAN, and trying to figure out where all my money went.

<div align="center">
  <img width="600" alt="image" src="https://github.com/user-attachments/assets/1e53884c-9546-4aa1-9a82-6e7e6bff8647" />
</div>

It all started because I just wanted to host a personal project. I spun it up on a spare mini PC and used a Cloudflare Tunnel to access it since my ISP blocks port forwarding (probably for security reasons, but who knows). I actually gave up on this pretty quickly at first. The power interruptions in my country happen frequently and last so long that even a UPS couldn't keep things alive.

I gave it a second chance once we got solar panels and a battery installed. But then the new problem was unstable internet, which is why I ended up adding a prepaid modem router as a backup WAN.

### The First Server (The Frankenstein and the heat problem)

<div align="center">
  <img width="600" alt="IMG_2799" src="https://github.com/user-attachments/assets/49abb72e-8098-4d90-b2ba-b5f9ee543cd3" />
</div>

I'm always cautious about the electricity bill and the heat components produce—heat is a huge issue where I live and wears parts down fast. So, I bought parts from China to build a low-power server around a Xeon E5-2650L v2. Putting it together the first time, I was sweating bullets because it just wouldn't POST. After reseating RAMs for a while, it finally worked. 

I used this server for my automation tools and another mini PC as a budget NAS running OpenMediaVault with a 4TB Seagate Exos drive I bought years ago. (I couldn't afford a real NAS, and honestly, what an unfortunate year to build a homelab with how expensive components are right now).

### Falling into the Proxmox Rabbit Hole

<div align="center">
  <img width="600" alt="IMG_3953-1" src="https://github.com/user-attachments/assets/e4ab3523-c7c0-4980-9394-c2ed0e840e55" />
</div>

After watching some homelab videos, I discovered Proxmox. I migrated everything over, but having only one node meant I was missing out on the cool stuff like ZFS and High Availability (HA). 

Fast forward a few weeks, I decided to build a cluster. I wanted processors with a good balance of high core count, low power, and affordability. I landed on two barebone Dell Enterprise SFF PCs with i5-8500T processors (35W max TDP). I actually haggled with an eBay seller to get the processors for $40 each.

But RAM and SSDs are scary expensive right now, and I couldn't find any good deals on eBay. I gave up on storage and just cannibalized the SSDs from my old mini PCs. For RAM, my mini PC sticks weren't compatible with the enterprise Dells. But then I remembered Mercari Japan—a marketplace where I used to buy cheap second-hand guitars. I found a very good deal on a second-hand 64GB TeamGroup RAM kit for $250. It took weeks to ship, but hey, patience is a virtue.

Once those two Dells were set up with Proxmox, I had my 3-node quorum. I set up ZFS and HA for critical instances like my Cloudflare Tunnel, because without it I can't access my web apps. Now I can finally clean the dust out of my Xeon server without taking the network down, because I can just move the instances to the other two servers.

### The Network Nightmare
Later on, I wanted to create two virtual networks and a failover WAN, so I bought a mini PC firewall router and an L3 switch. 

Let me tell you, setting up a virtualized pfSense router is a pain in the ass. The whole house was freaking out wondering why there was no internet. I honestly wished I had just bought a plug-and-play Fortinet firewall instead. I had to wait until everyone was asleep so I was the only one using the internet, just tinkering with DNS issues until I finally made it stable.

### The Giant Rack & The Financial Damage
<div align="center">
  <img width="600" alt="IMG_3952" src="https://github.com/user-attachments/assets/99ae3ddc-47f1-46a5-b072-a1af91db2b3e" />
</div>
Fast forward, I bought a 32U open server rack. I totally did not anticipate how big it actually is. Now there are all these empty slots that need to be filled, and it's so tempting to buy more nodes just to make it look good. HAHAHA. 

I'm not worried about single points of failure like having no redundancy for the firewall and switch—it's just a homelab. But my wallet definitely felt this project. Here is the final breakdown of the damage:
| Component | Specs | Cost (USD) |
| :--- | :--- | :--- |
| **Node 1** | Xeon E5-2650L v2, DDR3 48GB RAM, 1TB SSD | $350 |
| **Nodes 2 & 3** | 2x Dell SFF i5-8500T, DDR4 32GB RAM, 512GB SSD | $200 |
| **Networking** | pfSense Router Firewall + L3 Switch | $275 |
| **The Rack** | 32U Open Server Rack | $200 |
| **Misc. & Reused** | Patch cables, old drives, mini PC SSDs | $0 (Repurposed) + ??? |
| **Total Damage** | | **$1025+** |

*(Honestly, the total damage is probably higher once you factor in all the other random components I already owned and just reused to make this work.)*
