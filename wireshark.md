# MODULE 1 Analyzing Network Protocols With Wireshark 

Packet that Matters:

 Best way to begin capturing network traffic is collecting our analysis on a span mirror port on a switch near the client.

 This will help to keep the traffic flowing and to avoid the traffic being captured by the switch hence making it smaller and easier to analyze.

Another way to create a smaller haystack is to filter the captured traffic to only the traffic that is relevant to the analysis.

We create custom columns, protocols, and custom filters to help us analyze the traffic.

Also saving protocol filterings as button for the quick access to those filters.

## **Core Protocols**

Under the application data there are :

- UDP
- TCP
- IPV4
- IPV6
- ARP
- ICMP
- DNS
- TLS 

### **Custom Profiles**

Right click on down right on profile and select "New" and then create the custom profile.

After creating a new profile: go to edit and preferences to start customizing the profile.

Right of the bat: adding Delta time to the profile as title `delta` and type `Delta time displayed` to show the time difference between the packets.

 Another way is to right click on any value down and click `add as column` to add the value as a column.

#### **Creating and Saving buttons.**

There are some filters that you keep using but you dont want to keep writing them. For example `tcp.flags.syn==1` which is the syn=1 flag where the communication starts.

in order to add it as button, I write this on the filter box and click on `+` to add it as a button.


it is also important to colorize the packets in order to create the visibility. view==>colouring rules, then write the filter you want to filter (like regex) and then do not forget to enable it. Also change the importance level by dragging up and down in the list.

**<h1>PROTOCOLS IN DETAIL</h1>**


**<h2>1- ARP</h2>**


**NOTE THAT** ARP does not resolve IPV6 addresses. Meaning IPv6 does not use ARP.  IPV6 uses NDP(Neighbor Discovery Protocol) to resolve the addresses which replaces ARP.

Address Resolution Protocol (ARP) is a protocol used to resolve the MAC address of a host. meaning, it bridges the gap between layer 2 and layer 3.

ARP ne ise yarar nasil calisir?

Bir packet gonderecegin zaman, header olusturmak icin destination IP ve MAC address ihtiyacin var. sen baslangicta kendi IP ve mac adresini biliyorsun, bir de serverinkini.

Target'in MAC adresini bulmak icin ARP kullanilir. ilk once local arp cache'e bakar. eger varsa direkt cevap verir. eger yoksa `arp request` gonderir. Networke bunu broadcast olarak gonderir.

Bu broadcast domain icindeki devices will take this up, will check the IP address that is being resolved and will build and send a reply with  its own mac address as the source mac address.



Yani aslida soyle:

18 numarali bilet kimde ogrenmek istiyorsun. Elindeki listede varsa zaten sorun yok, yoksa ortaliga bagiriyorsun `18 numarali bilet kimdee` yani `what is the mac address for this IP address`?

Herkes biletine bakip `benimki x`, `benimki Y` diye  cevap veriyor.

Sen de sonunda ogrenmis oluyorsun ve header'i yaratip gonderiyorsun.

==> Arp requests are broadcasted to the network but responses are unicasted to the sender.


You check the ARP protocol if you see:

-   Problems connecting to an application 
-   intermittent connectivity.
-   Unicast flooding.


If the destination is visible (like Apple or Google,) it means that the destionation was on the Arp Cache already so it is not broadcasted but unicasted.


**Hands on Demo**:

**Lets disect a ARP request:
**
```
Address Resolution Protocol (request)
    Hardware type: Ethernet (1)     
    Protocol type: IPv4 (0x0800)
    Hardware size: 6
    Protocol size: 4
    Opcode: request (1)
    Sender MAC address: BelkinIn_9d:02:73 (94:10:3e:9d:02:73)
    Sender IP address: 192.168.10.1
    Target MAC address: 00:00:00_00:00:00 (00:00:00:00:00:00)
    Target IP address: 192.168.10.108
```


- Hardware type = Ethernet

- Protocol type = IPv4  Meaanign trying to resolve a mac address to IP address.

- Opcode = 1  meaning request

- Target MAC address: 00:00:00_00:00:00 (00:00:00:00:00:00)   so this is the information that is missing and being looked for. 00:00:00... means that the target mac address is not known.

- Target IP address: 192.168.10.108 is the IP address that is being looked for.



**Now lets look at the ARP Response to this request:**

```
Address Resolution Protocol (reply)
    Hardware type: Ethernet (1)
    Protocol type: IPv4 (0x0800)
    Hardware size: 6
    Protocol size: 4
    Opcode: reply (2)
    Sender MAC address: Apple_e7:ce:6d (a4:5e:60:e7:ce:6d)
    Sender IP address: 192.168.10.108
    Target MAC address: BelkinIn_9d:02:73 (94:10:3e:9d:02:73)
    Target IP address: 192.168.10.1
```
 
- Opcode = 2  meaning reply

- Sender MAC address: Apple_e7:ce:6d (a4:5e:60:e7:ce:6d)   so this is the mac address of the sender which was missing.

- Sender IP address: 192.168.10.108


As you can see, sender and target IP addresses match, so the ARP reply is valid and MAC address is resolved. 


In some cases we see some weird ARP requests that sends requests for entire network. like couple hundred or maybe more limited or less limited numbers of ARP requests.

This `could be ` and indicator to an attack.

The first thing to do is to check the IP origin of the ARP request. For that end, I will create a ARP profile in the wireshark.

as a new coulumn, I will add the `opcode` field which will filter requests and responds. that would be interesting in this case to see if there is any active subnets and actualy any response.

Here is the filter : `arp.opcode==2` This will show all the packets that responded to the requests.


Another very interesting filter is `arp.isgratuitous` which means that we are looking for arps that are  gratuitous either as requests or replies. Grattuitous means that the sender and target mac addresses are the same. Meaning sending its own IP and Mac address which means advertising itself.


Once we know that all is fine, we can remove any protocol that is not needed in the trace. For a protocol to be removed we use `!{protocolName}` like `!arp`.





**<h2>2- IPv4, IPv6 ve ICMP</h2>**

Unlike ethernet, IP is a end to end protocol not a point to point protocol.

`192.168.1.8` is an IP address, `255.255.255.0` is a subnet. 

IP header holds the information about the packet like version, header length,` DSCP(Differentiated Services Code Point)`, ECN(Explicit Congestion Notification), total length and so forth. Many of the times we will be dealing with `DSCP` part of it to troubleshoot where markings for the packet prioritizing is made.

Another important part is total length whici is the total amount of encapsulated packet including the header itself.

Next is the `identification` field which is used to identify the packet, it is either randomized or sequential which is used to `uniquely id` a packet from a station.

Helps figure out whether a packet is duplicated or not, and also help track application traffic behind a load balancer.

`flags` field helps to understand whether the packet is a fragment or not. or fragmentation is allowed or not.


`Time to Live` layer helps to see how many routers/or layer 3 switches a packet has hopped through on its way to destination.

`Protocol` field shows which protocol is coming next in the data payload. It could be TCP, ICMP, or other.


**IP Fragmentation**

Sometimes there is so much data that it is not possible to send it in a single packet.

Lets assume you are sending a data of 1500 bytes. But VPN tunnel has `MTU` 1400 bytes and rest is reserved for encapsulation. As long as the data is less than MTU, it can be sent in a single packet but if it is greater than that, `flags` field will be checked. If the flags are set to `MF` then it means that the packet is fragmented and needs to be sent in multiple packets(called fragments). Each fragment then holds in their header field on how to reassamble the packet.



Sometimes, like in encrypted traffic, the packet does not want to be intercepted or dissected.


If packet size is big and MTU is lower than that, and also `do not fragment` is set, then router will send an `ICMP` error message to the sender saying it cannot pass the packet.



**TTL**

For example when you ping to someplace, it gives you the TTL number.(like 51)

***TTL is not a function of time, it is a decrementing counter!!.*** As the packet travels through the network, each router decrements the counter by 1. If the number is reduced to 0, meaning the packet has reached the destination, it will be dropped and ICMP error message will be sent back to the sender.

This works in both directions in the same manner. This way, we can estimate how many routers are there in the network.



These days TTL starts either at 255(cisco/solaris), or 128(windows), or 64(linux)

**Understanding IP TTL**

Questions based on a Pcap file(`IP TTL`)

- 1. How many unique IP stations are transmitting in this trace file? 

