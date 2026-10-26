🚨 Incident Report: Simulated VLAN 20 Connectivity Loss

1. The Incident (Symptom)
During a verification phase, a simulated human error was introduced: PC-SALES (VLAN 10) lost connectivity to PC-HR (VLAN 20). 
- A ping from PC-SALES to PC-HR resulted in Request Timeout.
- PC-HR could not even reach its default gateway (host not reachable).

2. Investigation
- Tested connectivity from PC-SALES to PC-HR -> Failed.
- On SW1, executed the command: show interfaces trunk.
- Result: The output revealed that the trunk was only allowing VLAN 10. VLAN 20 was missing from the allowed list.

3. Root Cause
The 802.1Q trunk link between SW1 and R1 was manually restricted to only allow VLAN 10. Therefore, all frames tagged with VLAN 20 were being dropped by the switch.

4. The Fix
The trunk port on SW1 was reconfigured to allow both VLANs:
interface GigabitEthernet0/0
 switchport trunk allowed vlan 10,20

5. Verification
- Re-executed show interfaces trunk -> Confirmed Vlans allowed on trunk: 10,20.
- Ping from PC-SALES to PC-HR -> Success (5/5 packets received).
- Ping from PC-HR to its default gateway -> Success.
