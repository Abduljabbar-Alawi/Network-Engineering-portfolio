# 🚨 Incident Report: VLAN 20 Connectivity Loss

## 1. The Incident (Symptom)
While performing verification tests, PC-SALES (VLAN 10) lost connectivity to PC-HR (VLAN 20). PC-SALES ping resulted in `timeout`, and PC-HR could not even reach its default gateway (`host not reachable`).

## 2. Investigation
- Tested connectivity from PC-SALES to PC-HR -> Failed.
- On SW1, executed `show interfaces trunk`.
- **Result:** The output showed `Vlans allowed on trunk: 10`. VLAN 20 was missing from the allowed list.

## 3. Root Cause
The trunk link between SW1 and R1 was manually restricted to only allow VLAN 10. Traffic for VLAN 20 was being dropped at the switch.

## 4. The Fix
Reconfigured the trunk port on SW1 to allow both VLANs:
cisco
interface GigabitEthernet0/0
 switchport trunk allowed vlan 10,20

## 5. Verification

 Re-executed show interfaces trunk -> Confirmed Vlans allowed on trunk: 10,20.
 Ping from PC-SALES to PC-HR -> Success (!!!!!).
 Ping from PC-HR to gateway -> Success.
