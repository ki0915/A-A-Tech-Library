![post-thumbnail](https://velog.velcdn.com/images/tkops365/post/65c4efa1-7472-4aa0-aa8c-994385b67a25/image.png)

# Active Directory?

![](https://velog.velcdn.com/images/tkops365/post/cf0ba30b-ac69-496e-9b51-a58076dd2d7e/image.jpg)

Active Directory centralizes the management of common components of a computer network in a single repository called Active Directory (AD). To explain it more simply, you can think of it as a database that stores information about company employees' account information (ID, password), computer information, and policies you want to enforce (ex: password is 9 or more characters long). I'm familiar with it because I manage a company server, but it can be a bit confusing when you first hear it. The server running this Active Directory is called a domain controller (DC).

> Advantages

Centralized identity management: Easily control and control all users on your network.  
Security policy management: Configure security policies directly in Active Directory and apply them to users and computers across the network as needed.

There is convenience in being able to impose policies on the network and terminals within the network at will. It is very cumbersome to change settings on each computer, so this method is very convenient.

> Configuration

At the heart of every Windows domain is Active Directory Domain Services (AD DS). This service acts as a catalog that holds information about all "objects" that exist on the network. Objects include users, groups, printers, shares, etc.

### user

Users can be represented by two types of objects:

1. Person: A user generally refers to a person within an organization who accesses the network, such as an employee (company employee).

![](https://velog.velcdn.com/images/tkops365/post/2240c28c-4725-46d9-8986-841d0e3ff4e0/image.png)

2. Services: You can define services to use for services such as IIS or MSSQL. In this case, the user only has the permissions necessary to run the specific service.

![](https://velog.velcdn.com/images/tkops365/post/f500239b-d2d2-4785-91d3-b1bd96611d4e/image.png)

![](https://velog.velcdn.com/images/tkops365/post/8a395244-72fd-4e25-8412-99aee61a8b83/image.png)

### machine

A machine is for any computer that joins an AD domain. Machines are considered security principals and are assigned accounts just like regular users. This account has limited permissions within the domain.

The computer account itself is a local administrator on the computer to which it is assigned and is usually accessible to anyone other than the computer itself, but can be logged in with a password.

Caution!: Your computer account password is automatically rotated and usually consists of 120 random characters.

![](https://velog.velcdn.com/images/tkops365/post/09210179-107a-46f6-b6ef-0ba922829fc4/image.png)

### Security Group

It is literally a user group. You can easily manage users by adding them to groups. The user automatically inherits all privileges attached to the group. Security groups are also considered security principals and therefore have permissions to network resources.  
You can sleep.

Caution!) A group can have both users and computers as members. Other groups may also be included if necessary.

Below is an example of a group.

Domain Group Description

### Security group description

Domain Administrator: Users in this group have administrative rights to the entire domain. By default, they can manage all computers in the domain, including DCs.

Server Administrator: Users in this group can administer domain controllers. Management group membership cannot be changed.

Backup Operator: Users in this group can access all files, ignoring permissions. Used to perform data backups on your computer.

Account Administrator: Users in this group can create or modify other accounts in the domain.

Domain Users: Includes all existing user accounts in the domain.

Domain Computers: Includes all existing computers in the domain.

Domain Controller: Includes all existing DCs in the domain.

#### Organizational Unit (OU)

A container object that allows you to categorize users and systems. It is primarily used to define sets of users with similar policy requirements. For example, employees in the sales department are likely to have a different set of policies in place than employees in the development department. And remember that a user can only belong to one OU at a time.

Automatically created organizational units

### Automatically created organizational units

Embedded: Contains default groups that can be used on any Windows host.

Computer: All computers connected to the network are placed here by default. You can move it if necessary.

Domain Controller: The default OU that contains the DCs in the network.

User: Default users and groups that apply to the domain-wide context.

Managed Service Account: Holds the account used by services in the Windows domain.

**Added) Different policies can be deployed individually for each OU via Group Policy Objects (GPOs). GPOs can contain policies targeting users or computers, allowing you to set criteria for specific computers and identities.**

- Difference between security group and organizational unit

Organizational unit: Mainly used to apply policies  
Security Group: Used to grant permissions to resources

## AD Management

This part is similar for both users and machines. The idea is to separate devices and users based on their purpose. Just as it is good to separate intranet computers, development team personal computers, etc. from each other.

## AD authentication method

If you use Windows Domian, all credentials are stored on the domain controller. The user uses these credentials to authenticate to the service, and the service asks the domain controller to confirm the authentication is correct.  
Two protocols can be used for authentication: These are protocols that I occasionally encountered while studying hacking.

Kerberos: Used in newer versions of Windows. This is the default protocol for recent domains.

NetNTLM: A legacy authentication protocol maintained for compatibility.

Although I've heard that NetNTLM is often deprecated, both protocols live on most networks.

## expansion

As your company grows, your network also grows. It's a natural result. As the number of services increases and the information to be managed increases, the size of the network also increases. We know how it grows. Whether it's an algorithm or a flow chart, it's a structure you'll definitely see.

you're right. It is a tree structure.

![](https://velog.velcdn.com/images/tkops365/post/26ad27f9-1911-450e-be22-017ff2279379/image.png)

Active Directory supports multiple domain integration, allowing you to partition your network into independently manageable units. By making them share the same namespace, you can combine the domains in a tree form.

If your domain is split into two subdomains for UK and US branches, you can build a tree with a root domain and two subdomains called thm.local and thm.local, each with their own AD, computers, and users.

This partitioned structure gives you more control over who can access what in your domain. UK IT staff will have their own DC that manages only UK resources. For example, UK users cannot manage US users. In this way, the domain administrator at each branch has full control of its DCs, but not the DCs of other branch offices. You can also configure policies independently for each domain in the tree.

However, it is also common for companies with different namespaces to merge. What should I do in times like this? you're right. Just as the two Chinese characters for tree and neck come together to form the Chinese character for bush and forest,

the domain can also be a forest. Integrating multiple trees with different namespaces into the same network is called a forest.

By organizing multiple domains into trees and forests, you can have a nicely compartmentalized network in terms of management and resources. However, at some point, THM UK's users may need to access shared files on one of MHT ASIA's servers. To achieve this, domains arranged in

trees and forests are joined by trust relationships.

**Simply put, a trust relationship between domains allows you to grant users from another domain access to resources in another domain. This relationship can be unidirectional or bidirectional.**

This is how I looked into Active Directory. Normally, when managing a server, I only knew the concepts and moved on, but when I reflected on my knowledge properly, my perspective opened up more broadly. I need to gain more security and network knowledge in the future.