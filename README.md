# Home Lab #
*Documentation on my Homelab*

---

## Hardware Requirements ##
*This is just a guide that I will be documenting as we go forward.*

## I'll be updating this list as things go along ##

<details>
      <summary> Required Hardware </summary>
      
- A Laptop, Desktop... your primary computuing device.
- A secondary Computer. This could be an old desktop, A mini PC, or a Raspberry Pi, etc.
- A networking Switch or a way to have multiple connections to ensure that your computer is networked to what will be your proxmox box.
- A Flash drive, I'd suggest something along the lines of 8 GB

</details>

## Somethings to note before you get anything started ##

<details>
      <summary> Just things to consider while building </summary>
      
- So as a practical application of understanding how virtualization works, take a note of what your proxmox Specifications are,
- How many cores can the CPU utilize? What is the amount of RAM the computer has in it. What is the size of the harddrive.
- Additionally what are the speeds of each of those devices?
- While containers do end up being a very effective way to cap the amount of resources a certain application can use
- You might start to see these applications add up very quickly.

</details>

<details>
<summary> Main Sources </summary>
      
- [Proxmox](https://proxmox.com/en/)
- [balenaEtcher](https://etcher.balena.io/)
- [Proxmox Scripts](https://community-scripts.github.io/ProxmoxVE/)
- [Debian](https://www.debian.org/) 
- [Metasploitable2](https://www.vulnhub.com/entry/metasploitable-2,29/)
- [Kali](https://www.kali.org/)     

</details>

--- 

## Proxmox Installation ##
<details>
      <summary> Proxmox Installation </summary>
First go to [Proxmox](https://proxmox.com/en/) and click the downloads icon at the top of the page

![Proxmox dot com](https://github.com/user-attachments/assets/e4a6e957-7370-4755-bd3c-c60b2b572c8c)

the first option is Proxmox VE Installer. It is the one we will be choosing. 
But Keep in mind the Proxmox Backup Server ISO. I think we will be using it later.

![Proxmox Choices](https://github.com/user-attachments/assets/156fc1d8-7735-4673-ad32-3ddab235f6e3)

You can choose direct download or torrent. 

While that starts downloading, lets go to [balenaEtcher](https://etcher.balena.io/)
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

</details>

---

## Opening up Proxmox ##
<details>
      <summary> Opening Proxmox </summary>
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
</details>

---

<details>
      <summary> Setting up a Debian Box </summary>
      
## Starting out with Some OS's ##

I went to [Debian](https://www.debian.org/) 

If you right click on the "Download" button, you can see the option to Copy Link.

![Debian Download](https://github.com/user-attachments/assets/edc58ae4-6442-4f2c-bdd8-a523348fc7de)

Remember that box from before? Now we have a url that we can paste into this box to query for a URL.

![Debian URL Query](https://github.com/user-attachments/assets/0643596c-9eaf-4a1c-babf-8db236dc576b)

Now we can download straight from the source.

</details>

---

## Making Some Containers; Heimdall ##

<details>
      <summary> Heimdall Setup and an Introduction to Proxmox Scripts </summary>
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

</details>

---

## Pi Hole ##

<details>
      <summary> Setting Up Pihole </summary>
Well now here we are, What is the point of having a splash page if we don't have anything to display?
So I started with

[Pi Hole](https://community-scripts.github.io/ProxmoxVE/scripts?id=pihole)

Which luckily, the proxmox VE Helper-scripts already has the script to make a pi hole LXC. Neat.

![Pi Hole](https://github.com/user-attachments/assets/53ab4044-b11f-45ac-b978-37812f78f2f3)

Follow the same steps as we did above and use the shell on the pve node of your proxmox page

![Pi Hole Proxmox](https://github.com/user-attachments/assets/488dccdf-8ac5-430e-a764-0f716d04e669)

After clicking the Shell go ahead and punch in that
            
            bash -c "$(curl -fsSL https://raw.githubusercontent.com/community-scripts/ProxmoxVE/main/ct/pihole.sh)"

This is the [Pi hole list](https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts) list I used
![pihole](https://github.com/user-attachments/assets/9365f449-d2a8-4f14-9a04-578dba1ddb91)
</details>

---

## Metasploitable2 ##
<details>
      <summary> Less Obvious Installations </summary>

I wanted to provide an example of an instance where I had installed a virtual machine that was not from a template or a standard URL.
      
[metasploitable2](https://docs.rapid7.com/metasploit/metasploitable-2) is a box that is intentionally terrible and filled with vulnerabilities, I figured this 
could kill two birds with one stone. One, set up a project that will allow me to have a Security punching bag, and to install
something in a less conventional way.
using this method we will not have to download from a URL, or use a script. Instead we will just be utilizing the proxmox shell to grab and establish everything
we will need.

While in shell the first thing we will need to type in is

      wget https://sourceforge.net/projects/metasploitable/files/Metasploitable2/metasploitable-linux-2.0.0.zip

The Package will start to download and may take a moment or two. The next step will be to unzip the package.

      unzip metasploitable-linux-2.0.0.zip

It's possible especially if you have just been following what I have been doing, You actually don't have "unzip" installed.

      apt-get install unzip

This will obviously help extract the file. After the install, try the unzip command again.
after it has extracted the file,

      cd Metasploitable2-Linux/

will bring us to the Metasploitable2 Directory. Which is where we will need to be to 

      qemu-img convert -O qcow2 Metasploitable.vmdk metasploitable.qcow2

Followed by 

      qm create 300 --memory 2048 --cores 2 --name Metasploitable2 --net0 virtio,bridge=vmbr0 --boot c --bootdisk ide0

 and then finally

       qm importdisk 300 metasploitable.qcow2 local-lvm

You'll notice that after this command, it will begin "transferring" which is another way of saying that it is creating the VM.

and you should see after this, a new VM with the ID 300 named Metasploitable. There are a few things I want to do with this box 
just for fun. But we will get to that later.

</details>

 


- Hardening
- Firewall
- Adblock
- Wireguard
- VPN
- Virtual Machines
