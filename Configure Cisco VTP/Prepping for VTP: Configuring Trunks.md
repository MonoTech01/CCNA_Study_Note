LAB

Goal: Establish trunk links between all switches (SW1, SW2, SW3, SW4) in preparation for implementing VTP.

Steps:

Remote Access: Use SSH to access switches remotely, starting with the furthest (SW4) and working backwards to avoid connectivity disruptions.

Verify Connections (CDP): On each switch, use show cdp neighbor to verify physical connections and identify connected interfaces.

Configure Trunks:

SW4:
interface fa 0/8
switchport trunk encapsulation dot1q
switchport mode trunk
SW3:
interface range fa 0/7 - 8 (or interface range fa 0/7 , fa 0/8)
switchport trunk encapsulation dot1q
switchport mode trunk
SW2:
interface range gig 0/1 , fa 0/7
switchport trunk encapsulation dot1q
switchport mode trunk
SW1:
interface gig 0/1
switchport trunk encapsulation dot1q
switchport mode trunk
Key Points:

CDP: Cisco Discovery Protocol helps verify physical connections between Cisco devices.
Interface Range: Use interface range command to configure multiple consecutive interfaces simultaneously.
Trunk Encapsulation: Use .1q for trunking, allowing multiple VLANs to share the same physical link.
Trunk Mode: Set the interface mode to trunk to enable trunking.
Console Connection: Have a console cable and terminal emulator ready as a backup in case remote connectivity is lost.
Note: These configurations ensure all links between the switches are configured as trunks using 802.1Q encapsulation, allowing for VLAN information to be propagated once VTP is configured.


