# <h1>Important Protocols</h1>

## <u> **IpSec** </u>

### **What is IpSec?**


RFC 6071(IP Security (IPsec) and Internet Key Exchange (IKE) Document Roadmap)

IPsec is a protocol that provides a secure tunnel between two computers. It is used to protect data that is transmitted over the internet. 

IPsec helps mitigation against:

- eavesdropping

- theft

- replay attacks,

- Data corruption.

Ipsec operates in 2 different modes: tunnel mode and transport mode.

In ***tunnel mode***, everything is encapsulated in IPsec datagram. when data is transmitted, the layer 3 devices only use IPsec header to route the packet.

This is used basically in the site-to-site VPN and remote access VPN.

in ***transport mode***, all of the data is protected but the original IP header is not. Payload is protected by IPsec. This is used generally in P2P applications.


### Ipsec building Blocks:

Ipsec Suite either uses **Authentication Header(AH)** or **Encapsulating Security Payload (ESP)**. One difference is that in the former, the data is encrypted.

 ESP and AH both come with options of transport and tunnel.

In the AH transport mode, the payload is encrypted and the original IP header is not protected. In the tunnel mode, the payload is encrypted and the original IP header is protected. A new IP header is appointed to the packet in tunnel mode.

ESP transport and Tunnel modes can be used as it is or with AH.

ESP enapsulates the data so we have both header and trailer in the packet in Transport mode and in Tunnel mode.

in ESP header, different than AH header, there is no next header field and payload length field.


Afther the headers, there is `Security Association (SA)`. 

Security Association in IPsec suite is a `unidirectional connection` that gives devices the capability to use AH or ESP services. for a bidirectional comms, a pair of SA is needed.

<u>In order SA to be established, the following steps are needed:</u>

- **SPI**: Security Parameter Index. It is a unique number that is used to identify the SA.

- **Security Protocol Identifier**: It is a number that identifies the protocol that is used in the SA. (50 for AH or 51 for ESP)

- **Destination IP Address**


For key management, it is either done manually or automated using IKEv1 or IKEv2.

***IKE*** (Internet Key Exchange) is a protocol that is used to establish a key management between two computers. default one is IKEv2.


Next building block is **Crypto Algorithm**. These are used for Encryption , Authentication , Integrity and Pseudorandom Number Generation.


====

for SA estabblishement, there are couple of different protocols that are used.

- <u>ISAKMP</u> (Internet Security Association Key Management Protocol) :  Used for procedures and formats to establish SA. It helps us build the SA.

- <u>OAKLEY</u> (One-Way Authentication Key Exchange Protocol) : gives key-exchange mechanissm. Used to exchange key over insecure connection using Diffie-Hellman.

- <u>SKEME</u> (Security Key Exchange Method) :gives anonimity and reputability through key-exchange techniques.

- <u>IKE</u> (Internet Key Exchange) : Uses combination of ISAKMP, OAKLEY, and SKEME


=========


## **Ipsec in Enterprise**


In enterprise level, there are 2 main uses of IPsec:

- <u>Site-to-Site VPN</u>

connect 2 or more sites together. One type of Site-to-Site VPN is `DMVPN` (Dynamic Multicast VPN).

`logically` connects sites, protects `entire` network, provides corporate resources to other sites.




- <u>Remote Access VPN</u>

`logically` connect endpoint to another network.  IPsec using the OS IP stack. protects `individual` devices.

useful in wifi hotspots.

Bu mesela bir isci evden calisirken isyerinin agina ulassin diye kullanilan vpn. ticari bireysel VPNler de bu tip, hotspotshield, NordVPN gibi.





as for IPsec implementations, there are 2 main types:


- <u>GRE over IPSec</u>


way more commen. 

encapsulates entire packet. 






- <u>IPSec over GRE  </u>

much less common. only the payload is protected via IPsec. routing information stays visible in the GRE portion of the datagram.

















## <u>**MacSec**</u>

## <u>**ArpSec**</u>