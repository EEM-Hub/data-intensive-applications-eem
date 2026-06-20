---
source: https://en.wikipedia.org/wiki/Watermark_(data_synchronization)
fetched: 2026-06-19
---

A **Watermark** for [data synchronization](./Data_synchronization) describes an object of a predefined format which provides a point of reference value for two systems/datasets attempting to establish delta/incremental [synchronization](./Data_synchronization); any object in the queried data source which was created, modified, or deleted after the watermark's value will be qualified as "above watermark" and should be returned to the client requesting data.

 

This approach allows the client to retrieve only the objects which have changed since the latest watermark, and also enables the client to resume its synchronization job from where it left off in the event of some pause or [downtime](./Downtime).

 

## Methodology

 

**Watermark** term is often used in Directory Synchronization software development projects. For example, products such as [Microsoft Exchange Server](./Microsoft_Exchange_Server), [Active Directory](./Active_Directory), [Active Directory Application Mode](./Active_Directory_Application_Mode) (ADAM), and [Microsoft Identity Integration Server](./Microsoft_Identity_Integration_Server) 2003/ Microsoft [Identity Lifecycle Manager Server](./Identity_Lifecycle_Manager_Server?action=edit&redlink=1) 2007, as well as [Cisco Unified Communications Manager](./Cisco_Unified_Communications_Manager?action=edit&redlink=1) or [Sun Microsystems](./Sun_Microsystems) [IPlanet](./IPlanet) and other [LDAP](./Lightweight_Directory_Access_Protocol)-based directory products are using DirSync and consequently will consume "watermark" object to provide efficient synchronization between directories. Watermark object sometimes can be referred as "cookie".
DirSync control implementation can differ from product to product, however concept of watermark will allow any product to read changes in the directory incrementally.

 

The DirSync control is a Lightweight Directory Access Protocol (LDAP) server extension that enables a program to search an Active Directory partition for objects that have changed. When a program performs a DirSync search, the program creates a cookie that identifies the directory state at the time of an earlier DirSync query. With the first search, the program creates an empty cookie and Active Directory returns all objects that satisfy the query. Active Directory also returns an updated cookie that can be passed to the next search to obtain changes that are made since the first search. This process is repeated for each search.

— MSDN, from "How to poll for object attribute changes in Active Directory on Windows 2000 and Windows Server 2003" May 23, 2007

 

## See also

 
- [Watermark (disambiguation)](./Watermark_(disambiguation))
- [Microsoft Active Directory](./Microsoft_Active_Directory)
- [Microsoft Identity Integration Server](./Microsoft_Identity_Integration_Server)
- [High-water mark (computer security)](./High-water_mark_(computer_security))

 

## References

  
- ["LDAP Control for Directory Synchronization"](http://ietfreport.isoc.org/idref/draft-armijo-ldap-dirsync/) Microsoft Corporation

  

## External links

 
- [Understanding run profiles in MIIS 2003](http://support.microsoft.com/kb/827118)
- [Microsoft Publishes Open Directory-Synchronization Interface](http://www.microsoft.com/presspass/press/1999/mar99/dirsynpr.mspx)
- [Understanding the Directory](http://www.cisco.com/en/US/docs/voice_ip_comm/cucm/admin/5_0_1/ccmsys/a04direc.html)
- [LDAP Control for Directory](http://ietfreport.isoc.org/idref/draft-armijo-ldap-dirsync/)