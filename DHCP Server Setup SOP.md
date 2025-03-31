# **DHCP Server Setup SOP (Windows Server 2022)**

## **Approval Table**
| Name       | Role             | Approval Date |
|------------|------------------|---------------|
| Sejal      | Network Admin    | MM/DD/YYYY    |
| Limusi     | IT Manager       | MM/DD/YYYY    |
| Milan      | Security Analyst | MM/DD/YYYY    |

## **Revision History**
| Version | Date       | Description of Changes | Author             | Approver        |
|---------|------------|------------------------|--------------------|-----------------|
| 1.0     | MM/DD/YYYY | Initial SOP Creation    | Sejal, Limusi, Milan | IT Manager      |

---

## **1. Purpose**
This Standard Operating Procedure (SOP) provides step-by-step guidance for setting up and configuring a DHCP server on Windows Server 2022. This ensures proper IP address allocation and management within an enterprise network.

## **2. Scope**
- Applies to IT administrators responsible for network management.
- Covers DHCP role installation, scope configuration, reservations, and security settings.
- Ensures compliance with best practices for security and reliability.

## **3. Prerequisites**
- Windows Server 2022 installed and configured with a static IP.
- Administrative access to the server.
- Active Directory and DNS server properly configured.

## **4. IP Address Table**
This table outlines the IP addresses used in the DHCP configuration, including exclusions and reservations.

| IP Address         | Description         | Status     |
|--------------------|---------------------|------------|
| 192.168.1.1        | Default Gateway     | Static     |
| 192.168.1.100-192.168.1.200 | DHCP Scope Range | Dynamic    |
| 192.168.1.101      | Printer Reservation | Reserved   |
| 192.168.1.150      | Server 1            | Static     |
| 192.168.1.200      | Server 2            | Static     |

## **5. Network Topology Diagram**
The following diagram represents the network topology for the DHCP server setup.

