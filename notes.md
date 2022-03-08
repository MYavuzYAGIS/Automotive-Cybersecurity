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


