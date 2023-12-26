# ARP-spoofing 

> Python script to perform ARP spoofing on a network

This python script allows you to perform ARP spoofing, which can be used to perform attacks such as denial of service, man in the middle, or session hijacking.

# Requirements

We need these tools before starting attack.
```
* Python3
* Scapy 
* Wireshark
* python script
```

# Requirement details

Python comes installed on linux by default. 

You can download Scapy from terminal 

![](https://github.com/V3ENIOM/ARP-Spoofing/blob/main/Snaps/install-scapy.png)




# Installation

You can download this python script by running the following command in the terminal:
```
$ wget "https://github.com/V3ENIOM/ARP-Spoofing/blob/main/src/ARP.py"
```

# Setting up IP Forwarding

We will be using this script to perform man in the middle attack. Which means we will use this to get the data from another device connected to the same network.

The first step you have to do it turn on the ip forwarding. This step is required so that the connection on the victim's device does not get interrupted. 

To turn on IP forwarding, open terminal and type:
```
$ echo 1 > /proc/sys/net/ipv4/ip_forward

```
This will set value in ip_forward file to be 1 instead of 0


Now that we have that sorted, we need to get the MAC address and the IP address of the victim we want to attack on our network. To do that, you first need to see what IP address the router has given you. 

On linux you can get these details by using Nmap or just use this command line
```
$ sudo arp -a

```
![](https://github.com/V3ENIOM/ARP-Spoofing/blob/main/Snaps/sudo%20arp%20-a.png)

# Gathering MAC and IP addresses

According to this we are connected on IP Address: `192.168.1.3` and the Route IP is: `192.168.1.1`

You should see something like this after it is done scanning your network:
![](arp)

# Performing the attack

Now that you have gotten the IP address and the MAC address of the victim, all you need to do is launch the actual attack. To do that fire up the script you downloaded.
```
$ sudo python3 '/home/"{path}"/mmattack.py'
```

Now all you need to do is enter the details it asks. Here is an example of what it should look like:
![](https://github.com/V3ENIOM/ARP-Spoofing/blob/main/Snaps/dataforattack.png)

If everything goes well, you should be able to start sending packets.
![](https://github.com/V3ENIOM/ARP-Spoofing/blob/main/Snaps/packets.png)

Now while this ARP request is being spammed, we need to open wireshark
![](https://github.com/V3ENIOM/ARP-Spoofing/blob/main/Snaps/wiresharkstart.png)

Select the proper interface you are connected to. If you are not sure, select the `any` option and click start.

You should see a screen like this now:
![](https://github.com/V3ENIOM/ARP-Spoofing/blob/main/Snaps/wireshark2.png)

With the `ARP` protocol requests getting spammed. If you don't see this, you have done something wrong. 

Now to see victim's packets we should use this filter:
```
ip.addr=={ipaddress_of_the_victim} 
``` 
```
ip.addr==192.168.1.4 
```

and press enter.

![](https://github.com/V3ENIOM/ARP-Spoofing/blob/main/Snaps/wireshark.png)

