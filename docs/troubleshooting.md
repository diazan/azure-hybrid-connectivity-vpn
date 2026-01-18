# Troubleshooting Notes – Azure Hybrid VPN

## Netplan and cloud-init Conflict
The on-prem router and test VMs initially did not apply static IP configurations.
This was caused by cloud-init overwriting netplan settings.

**Resolution:**
- Disabled cloud-init network configuration
- Removed `50-cloud-init.yaml`
- Switched netplan renderer to `systemd-networkd`

---

## NetworkManager “Connection Failed” Message
The LAN interface showed a “connection failed” status.
This was expected behavior, as the LAN interface does not have a default gateway or Internet access.

---

## StrongSwan Service Name
On Ubuntu 24.04, the StrongSwan service is managed by `strongswan-starter`, not `strongswan.service`.

---

## Duplicate CHILD_SA Message
When manually bringing up the tunnel, StrongSwan reported duplicate CHILD_SA messages.

**Explanation:**
The tunnel was already established, and StrongSwan correctly prevented duplicate Security Associations.

---

## Validation Strategy
Traffic validation was performed from a test VM in the on-prem LAN to an Azure VM inside the VNet, confirming real encrypted connectivity.
