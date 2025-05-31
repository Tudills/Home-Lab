# Home Lab #
*Documentation on my Homelab*

---

# Hardware Requirements #
## This is just a guide that I will be documenting as we go forward. ##
## I'll be updating this list as things go along ##
- A Laptop, Desktop... your primary computuing device.
- A secondary Computer. This could be an old desktop, A mini PC, or a Raspberry Pi, etc.
- A networking Switch or a way to have multiple connections to ensure that your computer is networked to what will be your proxmox box.
- A Flash drive, I'd suggest something along the lines of 8 GB

## Somethings to note before you get anything started ##
* So as a practical application of understanding how virtualization works, take a note of what your proxmox Specifications are,
* How many cores can the CPU utilize? What is the amount of RAM the computer has in it. What is the size of the harddrive.
* Additionally what are the speeds of each of those devices?
* While containers do end up being a very effective way to cap the amount of resources a certain application can use
* You might start to see these applications add up very quickly.

Main Sources:
[Proxmox](https://proxmox.com/en/)
[balenaEtcher](https://etcher.balena.io/)
[Proxmox Scripts](https://community-scripts.github.io/ProxmoxVE/)
[Debian](https://www.debian.org/) 
[Metasploitable2](https://www.vulnhub.com/entry/metasploitable-2,29/)
[Kali](https://www.kali.org/)

# Proxmox Installation #

First go to 
[Proxmox](https://proxmox.com/en/)
and click the downloads icon at the top of the page

![Proxmox dot com](https://github.com/user-attachments/assets/e4a6e957-7370-4755-bd3c-c60b2b572c8c)

the first option is Proxmox VE Installer. It is the one we will be choosing. 
But Keep in mind the Proxmox Backup Server ISO. I think we will be using it later.

![Proxmox Choices](https://github.com/user-attachments/assets/156fc1d8-7735-4673-ad32-3ddab235f6e3)

You can choose direct download or torrent. 

While that starts downloading, lets go to 
[balenaEtcher](https://etcher.balena.io/)
and there is a link right in the middle of the screen to "Download Etcher"

![balenaEtcher page](https://github.com/user-attachments/assets/c9800da4-784d-461c-bced-2f0a85f7a97c)

Go ahead and download balenaEtcher.
After Proxmox has finished downloading, we can go ahead and install and use balenaEtcher. 
Grab a flash drive that is larger than the ISO file we downloaded (2 Gig or higher most likely)
Balena Etcher will look like this.

![balenaEtcher in action](https://github.com/user-attachments/assets/a9e11632-fe02-4e7b-8491-f5f462817c10)

You'll click "Flash from File" Navigate to the ISO image you just downloaded and select it. 
It will automatically move to the next step of the process where you select the drive
that you will be imaging to. Which is where you will be selecting the Flash drive that is higher
than 2 Gigs. And then we can click "Flash!"

When it is finished, your computer may give you an error that says that the flash drive
is unuasable. Which makes sense. We just made a bootable media. an installation disk if you will.
Eject it from your pc and grab your secondary PC that will be made into the Proxmox box.


## The Process ##
First thing is first. Proxmox does not have a GUI. 
In order for me to have everything be integrated, I used a raspberry pi loaded with NOOBS and installed a regular       
installation of Debian. I installed it on a 8 Gig microSD. The only thing this Pi will be doing, 
is acting as the GUI for Proxmox. The patch panel is directly connected to the switch. 
At some point im probably going to remove the switch from the front of the rack. 
I labeled each of the patch panels to indicate each port of the switch. 1-8. 
I then plugged in my pi into the 12th port so i could use patch ethernet to quickly plug it or unplug it into other devices. 
I did the same thing with my eero, and the proxmox box.

---

## Opening up Proxmox ##

Within the browser view of Proxmox we can see a lot of options. 

![Proxmox Left Side Initial](https://github.com/user-attachments/assets/5c4e49be-9c55-4eb1-a08a-fe861e70a1f1)

for now lets route to the left side of the screen under "Datacenter", Below that we will see, 
"pve" with an option to expand. It's likely that you will see three subjects within the pve category.
"localnetwork (pve)"
"local (pve)"
"local-lvm (pve)"

![localnetwork local local-lvm](https://github.com/user-attachments/assets/8336841e-2799-4ed5-a9d6-c7400011ecfb)
      
If we highlight, "local (pve)" 
here you will see an option called "ISO images". 

![ISO Images](https://github.com/user-attachments/assets/a555702c-b37a-48c5-b14b-74409c780937)

When we click on that we will see an option to "Download from URL"  

![download from URL](https://github.com/user-attachments/assets/83c06d1b-4f09-4f91-831b-677c0390c8c2)

As a decent starting point, we may as well grab a Debian 12 ISO Download

## Starting out with Some OS's ##

I went to [Debian](https://www.debian.org/) 

If you right click on the "Download" button, you can see the option to Copy Link.

![Debian Download](https://github.com/user-attachments/assets/edc58ae4-6442-4f2c-bdd8-a523348fc7de)

Remember that box from before? Now we have a url that we can paste into this box to query for a URL.

![Debian URL Query](https://github.com/user-attachments/assets/0643596c-9eaf-4a1c-babf-8db236dc576b)

Now we can download straight from the source.

---

## Making Some Containers ##

Alright, so this is where things get pretty fun. There is an incredible resource. 

[Proxmox Scripts](https://community-scripts.github.io/ProxmoxVE/)

Click "View Scripts"

![Proxmox VE Scripts](https://github.com/user-attachments/assets/eb7f432f-0dd4-41bd-ab56-c8285039c38c)

We have, so many options here. But, Im going to just walk you through one for now.

[Heimdall](https://community-scripts.github.io/ProxmoxVE/scripts?id=heimdall-dashboard)

![Heimdall](https://github.com/user-attachments/assets/45252864-3ad2-4db7-94ff-a92698b095e8)

Click back into your Proxmox page, and click "pve" you'll see a list of options 
- Search
- Summary
- Notes
- Shell
- System
- Updates
- Firewall
- Disks
- Ceph
- Replication
- Task History
- Subscription

If you hit shell it will open up a terminal.

![Proxmox Terminal](https://github.com/user-attachments/assets/e9d43989-39b4-417e-a544-5106e2f4f175)

and Press Ctrl+Shift+v 
and the script will populate 

![Script Population](https://github.com/user-attachments/assets/2bdbf4c0-4473-4a7d-b649-8730bfeaf46c)

            bash -c "$(curl -fsSL https://raw.githubusercontent.com/community-scripts/ProxmoxVE/main/ct/heimdall-dashboard.sh)"
            
If you slap enter, it will run the script and create a Heimdall instance. And when it starts running, it will provide you with an ip address.

![Heimdall IP](https://github.com/user-attachments/assets/6505c80a-85d8-4fbb-8f95-f6332cb1a44d)

Lets go to that IP Address
It should look like this,

![Heimdall Splash Page](https://github.com/user-attachments/assets/d309c634-f3d4-40c7-b8bb-eacf9700ccef)

---

Well now here we are, What is the point of having a splash page if we don't have anything to display?
So I started with

[Pi Hole](https://community-scripts.github.io/ProxmoxVE/scripts?id=pihole)

Which luckily, the proxmox VE Helper-scripts already has the script to make a pi hole LXC. Neat.

![Pi Hole](https://github.com/user-attachments/assets/53ab4044-b11f-45ac-b978-37812f78f2f3)

Follow the same steps as we did above and use the shell on the pve node of your proxmox page

![Pi Hole Proxmox](https://github.com/user-attachments/assets/488dccdf-8ac5-430e-a764-0f716d04e669)

After clicking the Shell go ahead and punch in that
            
            bash -c "$(curl -fsSL https://raw.githubusercontent.com/community-scripts/ProxmoxVE/main/ct/pihole.sh)"



- Hardening
- Firewall
- Adblock
- Wireguard
- VPN
- Virtual Machines
