# Automotive Ethernet

### General Ethernet :

Ethernet is used for `Bandwith`

In vehicles, low power consumption is important. Also , requirement for ECU(Electronic Control Unit) is to be able to comletely wake up from sleep under 100 miliseconds.

Standard 4 wires ethernet cannot handle this speed currently.

So instead of standard ethernet, we use `Automotive Ethernet` which can take care of these issues.



### Comparing Ethernet to CAN(Controller Area Network) and FLEXRAY

## CAN:

it is a multidrop (bus) technlogy where user can add / remove nodes.

Multidrop or bus technology means every node or every ecu is pysically, electrically connected to the same wires as ever other node.


single twisted pair copper wire. => low cost/ light weight
easy for `plug and play`
`Message` or `Packet` based communication.

Unique for CAN is that **`Non-Destructive Arbitration`** for handling message or packet `collisions`.

This is handled in the arbitration section or the arbitration ID of the can network. So when there is a possible collision risk , the arbitration ID is used to identify the message or packet. and the packet or the message with the smaller ID is sent first, whereas the packet or the message with the larger ID is sent later but *`WITHOUT A NEED FOR RE-TRANSMISSION`*.

so lower ID number transmits first, other one waits, not not getting killed just waits.
And nodes that transmits the higher ID packet also understands the situatuin and also waits.

This has a drawback: nodes that lost the arbitration (the ones sending the higher ID packet) will have to wait. *this maskes CAN not as time-critical and accurate in time*.

This is why FlexRay was developed

## FlexRay:

it is similar to CAN in terms of wiring. it is a *MultiDrop* technology BUT `all nodes must be pre-programmed wit a fixed configuration`

up to 10Mb/s. speed.
also good for plug and play.
message or packet based communication.

==> *Collision avoidance is based on time slots for each node*

Eveyn node in FlexRay is aware of time base so this helps each node to understand when it is allowed to transmit. So basically there is a cycle time, and it is divided into slices and each node has its own time slot where it is allowed to transmit.
So colisions dont happen in flexray.

This helps very accurate in time and security critical.



## Automative Ethernet :

*(100Base-T)/(1000Base-T)*

==> base means this is the speed at the slowest rate

Modern ethernet technologies, be it automotive or not, is NOT a bus technology anymore. Instead, it is *point-to-point technology.* This means that each node is connected to only one other node.
for multiple communication, we need to introduce a `SWITCH`.

Switch distributes the traffic to the nodes within a network based on their `pysicall adress` that.

Today commercially there are 100base and 1000base ethernet, 100 meaning 100Mb/s, 1000 meaning 1Gb/s.

Note that automotive ethenetnet is very cost effective network but not enough for `uncompressed audio and video streaming` since they handle around 10MBits.


![](ss/ss1.png)


In bus technology, all the node load can be used and it is  locked to 100 or 1000 mbits. in ethernet, however, it is not the case, aggregate bandwith can exceed 100 or 1000.

## Networking Topologies :

- Defines how device are connected to each other.
- Defines how the device communicate with each other.
- Determines network characteristics.
- Simple Technologies:
- - Point to Point(port) 
- - Ring (Also Etnernet, used for safety critical technologies)
- - Star (ethernet) like one switch with many ports
- - Bus (chained or attached) like CAN , FLEXRAY
- Complex topologies can combine these(like mesh)


