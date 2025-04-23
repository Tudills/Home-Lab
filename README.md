# Home-Lab
    Documentation on my Homelab

## The Process ##

    First thing is first. Proxmox does not have a GUI. In order for me to have everything be integrated, I used a raspberry pi loaded with NOOBS and installed a regular installation of Debian. I installed it on a 8 Gig microSD. The only thing this Pi will be doing, is acting as the GUI for Proxmox.
    The patch panel is directly connected to the switch. At some point im probably going to remove the switch from the front of the rack. I labeled each of the patch panels to indicate each port of the switch. 1-8. 
    I then plugged in my pi into the 12th port so i could use patch ethernet to quickly  plug it or unplug it into other devices. I did the same thing with my eero, and the proxmox box.

## A Sidebar ##

    This entire project has just been me learning by doing, so im going to let you know some of the fun interesting bits that I encountered.
    Initially, I wanted to set  up my lab isolated from my own network. While this could absolutely be done, 
    there would an immense amount of limitations. For starters, 
    if im not connected to the internet, obviously, I cannot update or upgrade the proxmox server. 
    Additionally, we wouldn't be able to set up any VMs. However, there are some observations worth noting.
    The first setup I had, was the raspberry pi plugged into the router, proxmox plugged into the router, and 
    the switch plugged into the router. When going into the router (cudy.net) I was able to see all of the connections. 
    I could see the switch, I could see the pi, and I could see the proxmox computer. While this is very cool, 
    proxmox seems to drop out every 30 minutes or so. I would re-plug it. and it would show back up on the router connection.
    However, when we introduce the eero, it is a router. But now we have two routers in the mix. gross. 
   
    So, I tore everything down.
    
    I started from scratch. and the first thing I did was reconfigure the cudy router to act just as another switch. 

## Cudy Router Bypass ##

    Because of my current living situation, I cannot set up my lab next to my home modem/router. Instead I have opted to use an eero to connect to the mesh network I have set up in my house.
    If you have access to be right next to your modem and router while doing homelab things, 
    you can skip this part where we make the cudy router, essentially into a switch. 
    Eventually I would like to cut the eero out entirely. This is what AI told one of my friends in regards to this goal.

   ### Disable DHCP Server ###

    Log in to the router’s admin panel (usually http://192.168.0.1/ or http://cudy.net/).
    Navigate to LAN Settings > DHCP Server.
    Disable DHCP (the main router on your network should handle IP assignments).

   ### Assign a Static IP (Optional but Recommended) ###

    Go to LAN Settings > IP Address.
    Assign a static IP outside the main router’s DHCP range (e.g., if your main router uses 192.168.1.100-200, set the Cudy to 192.168.1.2).
    Save settings.

  ### Disable Firewall & VPN Features ###

    Turn off Firewall, VPN, and NAT (if applicable) to prevent interference.

  ### Connect via LAN Ports (Not WAN) ###

    Do not use the WAN/Internet port (it bypasses switching functionality).
    Connect devices to the LAN ports only.
    Connect one LAN port to your main router/network.

  ### Verify Connectivity ###

    Devices connected to the Cudy should now receive IPs from the main router.
    Test connectivity (ping, internet access).


Effectively, now I have two switches, and one eero, acting as my router.

## Patch Panel ##

    There are five ports on the Cudy router, 
    they can all be configured to be Lan ports, save for one port.
    I patched one port to a 8 port switch, and the remaining three ports
    on the Cudy are connected directly to the eero, my Proxmox box, and 
    for some reason, A raspberry pi.

## A Raspberry Pi for some reason ##

    It actually will make sense when I explain it. Part of my idea with this lab was to have
    the entire thing be complete on its own. At some point I want to be able to pick this monster
    up and take it anywhere, plug it in, and be able to jump into it. 

    Proxmox does not have a traditional GUI, it does indeed have one, but it is only accessible via a 
    browser connection from a device on the same network. Which is why I picked a Raspberry Pi 4 that
    I just had lying around. Additionally the racks that I bought came with a neat little PCB adapter 
    that make the Mini HDMI into a full size HDMI, so now I dont have to think about finding any of my 
    Mini HDMI cables. 

## Opening up Proxmox ##

    Within the browser view of Proxmox we can see a lot of options. 

    (Expansion will be here)

    for now lets route to the left side of the screen under "Datacenter" and we will see a sub category, called, "pve". 
    Within that we will see a series of options depending on your network setup. 
    What we want to look at is local (pve) here you will see an option called "ISO images". 
    When we click on that we will see an option to "Download from URL" 
    
    (Expansion will be here)

## Starting out with Some OS's ##

    
    
    

The next step will be...

-Hardening
-Firewall
-Adblock
-Wireguard
-VPN
-Virtual Machines

Within the browser view of Proxmox we can see a lot of options. 

(Expansion will be here)

for now lets route to the left side of the screen under "Datacenter" and we will see a sub category, called, "pve". within that we will see a series of options depending on your network setup. What we want to look at is local (pve) here you will see an option called "ISO images". When we click on that we will see an option to "Download from URL" 


(Expansion will be here)

