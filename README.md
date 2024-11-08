# Delegate Controls to Groups and Users

## Description
This project focuses on the creation and management of Organizational Units (OUs) in Active Directory (AD) and demonstrates the process of delegating specific permissions to user groups. It is designed for organizations that need to segment administrative responsibilities and ensure appropriate levels of access and control. The project includes configuring OUs, setting up delegation permissions for specific groups (e.g., helpdesk teams), and verifying those permissions to ensure accurate delegation.

## Tools and Utilities

- **Windows Server (with Active Directory Domain Services)**: Platform for managing OUs and delegation.
- **Active Directory Users and Computers (ADUC)**: Used for creating OUs and managing permissions.
- **Delegation of Control Wizard**: Simplifies the process of assigning delegated permissions to groups.
- **Command Prompt (cmd)**: Used for advanced permission management and verification with `dsacls`.

## Environments

### Server Environment
- **Operating System**: Windows Server configured with AD DS.
- **AD Structure**: Includes custom OUs and delegated groups for specific management scenarios.

### User Groups
- Created specific groups, such as **"Helpdesk"**, which permissions were delegated for targeted control within OUs.

## Program Walkthrough

### Creating Child OUs
1. **Created child OUs** (e.g., **Laptops** and **Desktops**) within the main **Boston OU** to allow for differentiated policy application.

### Setting Up Groups and Delegation
1. **Formed a Helpdesk group** within the **Boston OU**.
2. Delegated control to the Helpdesk group by right-clicking the **Boston OU** and selecting **Delegate Control…**.
3. Used the **Delegation of Control Wizard** to grant the Helpdesk group permissions to reset passwords and manage user accounts.

### Assigning Permissions
1. Chose the **Helpdesk group** for delegation and defined specific permissions (e.g., resetting passwords).
2. Verified the delegation by reviewing the **Properties** of the **Boston OU** under the **Security** tab, confirming that the Helpdesk group had the appropriate permissions.

### Creating a User OU
1. Added a **Users OU** under the **Boston parent OU** for better organization and structured user account management.
2. Applied similar delegation techniques to grant the Helpdesk group necessary permissions within the **Users OU**.

### Advanced Verification
1. Inspected and verified permissions set for the Helpdesk group using **Advanced settings** in the **Security** tab.
2. Utilized the `dsacls` command in **Command Prompt** for further inspection of permissions:
   ```cmd
   dsacls "OU=Boston,DC=DomainName,DC=Local"

# Controls Delegation

## **Scenario**

In Boston there are both laptops/desktops for the org, but they will receive different settings through Group Policy. Suppose there is also a helpdesk in Boston as well. The helpdesk should also have the ability to reset passwords. Any users in the Boston area should also be listed also.

1. Create a **child** OU for both Laptops and Desktops for the Boston OU 
    - Both Laptops/Desktops OU can now be managed independently and policies may vary between the two

2. Create a **group** for Helpdesks under the Boston OU
    - If an individual works Helpdesk in Boston they will automatically be a member of that group

3. In order to reset passwords, right-click the Boston OU and select **Delegate Control…** The delegation wizard will pop up asking a few questions on what needs to be delegated and who needs to be delegated to
    
    
    ![image](https://github.com/user-attachments/assets/1d0c2731-f5f2-45ff-9baa-d36a3110bc1d)

    - Select the users and groups (Helpdesk) that need control of a resource and select Next
    
    ![image 1](https://github.com/user-attachments/assets/557869f4-996e-436c-b640-35dd0c31fe17)

    ![image 2](https://github.com/user-attachments/assets/eef1135f-beda-4798-a28f-6a6e9353bc4e)

    -   Will then be prompted to select the tasks that require delegation for Helpdesk
    

![image 3](https://github.com/user-attachments/assets/fb5c1971-a0cc-4d23-b1b2-79793df76538)

![image 4](https://github.com/user-attachments/assets/e3d8f0d4-fcb6-4d78-84db-46ce49032ef6)

4. Create another OU under Boston and name it Users

![image 5](https://github.com/user-attachments/assets/1d180558-1cd1-461e-bd57-e7fe588cee4f)

![image 6](https://github.com/user-attachments/assets/9195597d-504e-463a-9ca2-b8eca5987e53)

### **Verifying Delegation**

Verifying who has permissions for a container or OU can be important and gives an idea of what users or resources have control or managed within those Containers

1. Right-Click the Boston OU and select **Properties.** Navigate to the **Security** tab and scroll to the **Helpdesk** group. The permissions for Helpdesk will be presented and there is a check box for **Special Permissions** for the Helpdesk

![image 7](https://github.com/user-attachments/assets/716e5a2e-5ebd-4b16-a2e2-e8117855ab55)

![image 8](https://github.com/user-attachments/assets/ff19505b-f89d-492e-a513-ba7b652dac55)

2. To see the actual permissions, select the **Advanced** button. Can then view all permissions the Helpdesk has within the OU and can make modifications to the group 

![image 9](https://github.com/user-attachments/assets/e12a01a1-25fe-4386-bed2-0b55a366bef2)
![image 10](https://github.com/user-attachments/assets/f276879c-2054-4718-a197-a3ceba06aa85)


3. If one were to want to start over on the permissions and provide new delegations or permissions to the group, it can be done by selecting **Restore defaults.** Now only the default assignments will remain for that group

![image 11](https://github.com/user-attachments/assets/0730698a-50d8-4e47-8d3f-6342cc133c21)

4. In **cmd** the following tasks can be done from there as well using the **dsacls** command
    - **dsacls -** Allows for full management of delegations
  
## Summary
This project provides a comprehensive guide for managing Organizational Units in Active Directory with clearly defined permissions and control delegation. It enhances administrative oversight, supports structured resource management, and ensures security through strategic delegation practices
