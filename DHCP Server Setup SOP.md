# **DHCP Server Setup SOP (Windows Server 2022)**

## **Table of Contents**
1. [Approval Table](#approval-table)
2. [Revision History](#revision-history)
3. [Purpose](#purpose)
4. [Scope](#scope)
5. [Prerequisites](#prerequisites)
6. [IP Address Table](#ip-address-table)
7. [Network Topology Diagram](#network-topology-diagram)
8. [Step-by-Step Guide](#step-by-step-guide)
    1. [Installing the DHCP Role](#step-1-installing-the-dhcp-role)
    2. [Configuring the DHCP Scope](#step-2-configuring-the-dhcp-scope)
    3. [Authorizing the DHCP Server](#step-3-authorizing-the-dhcp-server)
    4. [Configuring DHCP Reservations](#step-4-configuring-dhcp-reservations)
    5. [Securing the DHCP Server](#step-5-securing-the-dhcp-server)
    6. [Verifying and Testing DHCP Configuration](#step-6-verifying-and-testing-dhcp-configuration)
9. [Troubleshooting Common Issues](#troubleshooting-common-issues)
10. [Maintenance and Monitoring](#maintenance-and-monitoring)
11. [Conclusion](#conclusion)

---

## Approval Table

| Approval Level | Name           | Title              | Date       | Comments   |
|----------------|----------------|--------------------|------------|------------|
| Author         | Sejal, Limusi, Milan | System Admin, Network Specialist, IT Technician | 2025-03-29 | Initial Draft |
| Approver       | Felix Liang    | Instructor | 2025-03-31 | Approved |


## Reversion Info

| Version | Date       | Author           | Description                  |
|---------|------------|------------------|------------------------------|
| 1.0     | 2025-03-29 | Sejal, Limusi, Milan | Initial SOP Creation          |
| 1.1     | 2025-03-30 | Sejal, Limusi, Milan | Added Accountability Matrix   |
---

## Accountability Matrix

This section assigns responsibilities for different tasks involved in setting up and maintaining the DHCP server.

| **Task**                     | **Responsible Person/Role**     |
|------------------------------|--------------------------------|
| Approving SOP                | **IT Manager/Instructor**                |
| Installing DHCP Role         | **System Administrator**      |
| Configuring DHCP Scope       | **Network Specialist**          |
| Authorizing DHCP Server      | **IT Technician**    |
| Configuring Reservations     | **Network Specialist**          |
| Securing DHCP Server         | **IT Technician**    |
| Testing DHCP Configuration   | **System Administrator**      |
| Troubleshooting Issues       | **IT Technician**            |

### Responsibilities
- **System Administrator:** Installs and manages DHCP services.
- **Network Specialist :** Ensures proper IP configuration and address management.
- **IT Technician:** Implements security measures for DHCP services.

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

                      +-----------------+
                      |    Internet     |
                      +-----------------+
                             |
                             |
                         +-----------+
                         |   Router  |
                         +-----------+
                             |
              +-----------------------------+
              |                             |
    +------------------+             +------------------+
    |  DHCP Server     |             |     Switch       |
    |  (Static IP)     |             +------------------+
    |  192.168.1.10    |                    |
    +------------------+           +----------------------+
              |                    |                      |
    +-------------------+    +-------------------+   +-------------------+
    |  Static Server 1  |    |   Static Server 2  |   |   Clients (PCs)   |
    |  192.168.1.150    |    |  192.168.1.200     |   |   192.168.1.110     |
    +-------------------+    +-------------------+   +-------------------+

    
---

## **Step-by-Step Guide**

### **Step 1: Installing the DHCP Role**

1. Open **Server Manager**.
2. Click on **Manage** > **Add Roles and Features**.
3. Choose **Role-based or feature-based installation** and click **Next**.
4. Select the target server and click **Next**.
5. Select **DHCP Server** and click **Next**.
6. Click **Install** and wait for the installation to complete.

---

### **Step 2: Configuring the DHCP Scope**

1. Open **DHCP Manager** (`dhcpmgmt.msc`).
2. Right-click on the server name and select **New Scope**.
3. Define the following:
   - **Scope Name**: OfficeLAN
   - **IP Address Range**: From `192.168.1.100` to `192.168.1.200`
   - **Subnet Mask**: `255.255.255.0`
   - **Exclusions**: Any reserved IPs that you do not want to assign.
   - **Lease Duration**: Set as per your network policy.
4. Configure **DHCP Options** (under **Scope Options**):
   - **Router (Default Gateway)**: `192.168.1.1`
   - **DNS Servers**: Set DNS servers for the scope.
   - **WINS Servers** (if applicable).
5. Click **Finish** to activate the scope.

---

### **Step 3: Authorizing the DHCP Server**

1. Open DHCP Manager.
2. Right-click on the DHCP server name and select Authorize.
3. Wait for authorization to complete, then refresh the console.

---

### **Step 4: Configuring DHCP Reservations**

1. Expand the configured scope and select Reservations.
2. Right-click on Reservations and select New Reservation.
3. Enter the following details:
4. Reservation Name: e.g., Printer
  - **IP Address**: 192.168.1.101
  - **MAC Address**: 00-11-22-33-44-55
5. Click Add and then OK.

---

### **Step 5: Securing the DHCP Server**

1. Enable DHCP Audit Logging to track all DHCP-related activities.
2. Configure DHCP Filtering to allow or deny specific MAC addresses.
3. Implement Network Access Protection (NAP) to enforce security policies.
4. Monitor the Event Viewer for DHCP-related logs (Event IDs 1000-1020).

###**Step 6: Verifying and Testing DHCP Configuration**

1. On a client machine, run the following commands to release and renew the IP address:
- **ipconfig /release**
- **ipconfig /renew**
2. Verify that the client machine receives an IP address from the configured scope.
3. Check the Event Viewer for any DHCP-related warnings or errors.

---

## **Troubleshooting Common Issues**

| Issue                         | Solution                                                            |
|-------------------------------|---------------------------------------------------------------------|
| Clients not receiving IPs     | Ensure DHCP scope is active and authorized.                         |
| Duplicate IP addresses assigned| Verify scope exclusions and reservations.                          |
| DHCP server not responding     | Restart DHCP service (`Restart-Service dhcpserver`).               |
| IP conflicts                   | Enable DHCP Conflict Detection (`Set-DhcpServerSetting -ConflictDetectionAttempts 2`). |

---

## **Maintenance and Monitoring**

1. Regularly review DHCP lease allocations.
2. Enable email alerts for DHCP failures.
3. Keep security patches and updates applied.

---

## **Conclusion**

Setting up a DHCP server on Windows Server 2022 ensures efficient IP address management, improves network reliability, and enhances administrative control. Following the outlined steps will help IT administrators deploy a secure and well-structured DHCP service. Regular monitoring and best security practices should be implemented to maintain server integrity.

                






