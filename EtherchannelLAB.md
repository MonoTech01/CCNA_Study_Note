SW1, SW2

int range e0/0-1
sw trunk encap dot1q
sw mode trunk 
sw trunk allowed vlan 1, 2, 22

SW1
int e0/2
sw trunk encap dot1q
sw mode trunk
sw trunk allowed vlan 12, 22

SW1, SW2

int range e0/0-1
channel-group  1 mode active 
no shut
