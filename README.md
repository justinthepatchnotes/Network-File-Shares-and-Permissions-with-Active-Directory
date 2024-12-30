<p align="center">
<img src="https://i.imgur.com/wUBo4Vj_d.jpeg?maxwidth=520&shape=thumb&fidelity=high" height="40%" width="60%" alt="Logo"/>
</p>

# Network File Shares and Permissions with Active Directory

## Prerequisites and Installation

This tutorial walks you through the process of creating and managing network file shares with Active Directory integration. You'll configure file share permissions for users and groups to allow or deny access based on roles.

## Environments and Technologies Used
- **Microsoft Azure Virtual Machines**
- **Remote Desktop**
- **Active Directory Users and Computers**
- **Network Security Group**
- **Organization Units**

## Operating Systems Used
- **Windows 10**
- **Windows Server 2019**

## List of Prerequisites
- **Active Directory Domain Controller setup**
- **Client machine connected to the same domain**
- **Basic knowledge of Active Directory and file sharing**
- **Remote Desktop access to Azure VMs**


## Installation Steps

### Step 1: Prepare the Environment

1. Create two remote desktop instances: one as a Domain Controller (DC-1) and one as a client machine (Client-1).
2. Log in to the domain controller as an admin and to the client PC as a normal user.

![1](https://i.imgur.com/EakkaxS.png)
**Domain Controller (DC-1)**
![2](https://i.imgur.com/Iaizm3X.png)
**Client machine (Client-1)**
![2](https://i.imgur.com/iAmweu3.png)
<br>

### Step 2: Create File Share Folders on the Domain Controller

1. On DC-1, open **Windows Explorer** and navigate to the **C:\ drive**.
2. Create four folders: **read-access**, **write-access**, **no-access**, and **accounting**.

![1](https://i.imgur.com/lvZIbwg.png)
![2](https://i.imgur.com/UMErmIs.png)
<br>

### Step 3: Configure Sharing Permissions

1. Right-click each folder and go to **Properties** → **Sharing**.
2. Click **Share**, and in the dropdown menu, select **Domain Users**.
3. Set permissions as follows:
   - **read-access**: Read permissions
   - **write-access**: Read/Write permissions
   - **no-access**: Deny access to normal users (assign **Domain Admins** Read/Write access)

![1](https://i.imgur.com/97PbZFV.png)
![2](https://i.imgur.com/zo2t2ya.png)
![3](https://i.imgur.com/T5g1283.png)
<br>

### Step 4: Test Access on Client-1

1. On Client-1, press **Run** → type `\\DC-1` to access the shared folders.
2. Test the following:
   - **read-access**: Open and edit a file (should allow viewing only).
   - **write-access**: Edit and save the file.
   - **no-access**: You should see an error indicating access is denied.

![1](https://i.imgur.com/6dmZfzQ.png)
![2](https://i.imgur.com/BYvlvLX.png)
**Read Only Access (Cannot Create a File)**
![2](https://i.imgur.com/ohBlpf5.png)
**Write Only Access**
![2](https://i.imgur.com/N6mLxLH.png)
**No Access**
![2](https://i.imgur.com/cXdtPNx.png)
<br>

### Step 5: Create and Assign an "ACCOUNTANTS" Security Group

1. On DC-1, open **Active Directory Users and Computers**.
2. Create a new **Organizational Unit** (OU) called **_SECURITY_GROUP**.
3. Create a **Group** named **ACCOUNTANTS** within this OU, selecting **Global** for group scope and **Security** for group type.

![1](https://i.imgur.com/wiCSA2f.png)
![2](https://i.imgur.com/9TRGbhl.png)
<br>

### Step 6: Set Permissions for the "accounting" Folder

1. Go to the **accounting** folder and open its **Properties** → **Sharing**.
2. Add the **ACCOUNTANTS** group and grant **Read/Write** permissions.
3. Share the folder.

![1](https://i.imgur.com/kvwSEWf.png)
<br>

### Step 7: Assign User to the "ACCOUNTANTS" Group

1. In **Active Directory**, add the appropriate user to the **ACCOUNTANTS** group.
2. Right-click the group → **Properties** → **Members** → **Add** → search and add the user.

![1](https://i.imgur.com/BEthIO2.png)
![2](https://i.imgur.com/wRMC5Tc.png)
<br>

### Step 8: Log Off and Log In on Client-1

1. Log off from Client-1, then log back in to apply group membership changes.
2. Open **Windows File Explorer**, navigate to `\\DC-1`, and open the **accounting** folder.
3. Test if you can access, edit, and save the file.

![1](https://i.imgur.com/88NrMUt.png)
<br>

<div style="border-left: 4px solid lightskyblue; padding: 10px; background-color: #F0F8FF;">

You now have successfully set up network file shares and configured permissions using Active Directory. For more details, visit the [Microsoft Support Page](https://support.microsoft.com/en-us).

</div>

## FAQ

**Q: How do I give specific users read-only access?**  
A: Set the folder permissions to "Read" for the specific user or group.

**Q: What if a user can't access a folder?**  
A: Ensure that the user is added to the correct security group and that the share permissions are properly set.

---

## Conclusion
<div style="border-left: 4px solid blueviolet; padding: 10px; background-color: #E6E6FA;">

  🎉 You’ve successfully configured network file shares with Active Directory permissions! 🎉
</div>
