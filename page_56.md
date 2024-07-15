https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=glossary



Glossary

This glossary provides terms and definitions for the #REPLACE_ME_PRODUCTS# software and products.

The following cross-references are used in this glossary: 
See refers you from a nonpreferred term to the preferred term or from an abbreviation to the spelled-out form.
See also refers you to a related or contrasting term.




A
B
C
D
E
F
G
H
I
K
L
M
N
O
P
R
S
T
U
V
W
Z



A


activation key
See license key.
advisory lock
A type of lock that a process holds on a region of a file that signals any other process to not use or lock the region or an overlapping region. Other processes are not forced to comply.
allocatable extent limit
A maximum total capacity for the system. The allocatable extent limit is calculated from pool extent sizes.
application key
See license key.
array
An ordered collection, or group, of physical devices (disk drive modules) that are used to define logical volumes or devices. An array is a group of drives designated to be managed with a Redundant Array of Independent Disks (RAID).
asynchronous replication
A type of replication in which control is given back to the application as soon as the write operation is made to the source volume. Some time later, the write operation is made to the target volume. See also synchronous replication.
audit log
An unalterable record of all commands or user interactions that are issued to the system.
authenticated user
A user who has logged in to the system with a valid account (user ID and password).
authentication
The mechanism by which a system determines what permissions a particular authenticated user has to access specific resources or actions. See also authorization.
authorization
The mechanism by which a system determines what permissions a particular authenticated user has to access specific resources or actions. See also authentication.
authorization code
An alphanumeric code generated for administrative functions, such as password resets or two-factor authentication bypass.
available capacity
The amount of usable capacity that is not yet used in a system, pool, array, or MDisk.





B


block storage
A unit of data storage on a device.





C


cache
Storage or memory that is used to improve access times to instructions, data, or both. For example, data that resides in cache memory is normally a copy of data that resides elsewhere in slower, less expensive storage, such as on a disk or on another network node.
cache eviction
A process by which data associated with a file is removed from the cache system. The data is removed either by using a Least Recently Used (LRU) algorithm when configured General Parallel File System (GPFS) hard or soft quota limits are exceeded or by issuing a command.  When referenced again in the cache system, the data that is associated with the file is retrieved from the home system.
caching I/O group
The I/O group in the system that performs the cache function for a volume.
call home
A communication link established between a product and a service provider. The product can use this link to place a call to a service provider when it requires service. With access to the machine, service personnel can perform service tasks, such as viewing error and problem logs or initiating trace and dump retrievals.
capacity
The amount of data that can be contained on a storage medium.
capacity recycling
The amount of provisioned capacity that can be recovered without causing stress or performance degradation. This capacity identifies the amount of resources that can be reclaimed and provisioned to other objects in an environment.
capacity threshold
The percent of total usable physical capacity that used capacity must exceed before a notification is sent. See also total usable physical capacity.
certificate
A digital document that binds a public key to the identity of the certificate owner, thereby enabling the certificate owner to be authenticated. A certificate is issued by a certificate authority and is digitally signed by that authority.
change volume
A volume that is used in Global Mirror that holds earlier consistent revisions of data when changes are made.
child pool
A user-defined capacity that is formed from capacity that is defined either in another pool or a system. See also parent pool.
CIFS
See Common Internet File System.
CIM
See Common Information Model.
CIM object manager (CIMOM)
The common conceptual framework for data management that receives, validates, and authenticates the CIM requests from the client application. It then directs the requests to the appropriate component or service provider.
CIMOM
See CIM object manager.
CKD
See count key data.
CLI
See command-line interface.
client
A software program or computer that requests services from a server. See also host, server.
cloud account
An agreement with a cloud service provider to use storage or other services at that service provider.  Access to the cloud account is granted by presenting valid credentials.
cluster
A group of computers and other resources that operate together as a single system.
command-line interface (CLI)
A computer interface in which the input and output are text based.
Common Information Model (CIM)
An implementation-neutral, object-oriented schema for describing network management or systems management information. The Distributed Management Task Force (DMTF) develops and maintains CIM specifications.
Common Internet File System (CIFS)
A protocol that manages shared, remote file access for applications to files, printers, serial ports, and so on over a TCP/IP network.
compression
A function that removes repetitive characters, spaces, strings of characters, or binary data from the data being processed and replaces characters with control characters. Compression reduces the amount of storage space that is required for data.
compute node
An independent machine that contains one or more microprocessors, memory, storage, and network controllers and runs its own operating system and applications.
concurrent copy
A function of the DFSMSdss component that is used to back up any collection of data at a point in time with minimum down time for the database or application that uses the collection of data.
copyback
A process that moves data back to its expected or preferred location to maintain an array in a more efficient configuration after a failed drive is replaced.
count-key-data record
See data record.
count key data (CKD)
An architecture for a direct access storage device (DASD) device or logical device that specifies the access mechanisms for the logical data units on the device through a specific set of supported channel commands.  Extensions to the CKD command set form the basis of Extended CKD.
A data recording format that uses self-defining record formats in which each record on a volume is represented by up to three fields: a count field identifying the record and specifying its format, an optional key field that can be used to identify the data area contents, and an optional data field that typically contains the user data. See also data record, storage architecture type.


CRU
See customer-replaceable unit.
customer-replaceable unit (CRU)
An assembly or part that can be replaced in its entirety by a user when any one of its components fails.
cylinder
A unit of storage on a count-key-data (CKD) device with a fixed number of tracks.





D


data consistency
A characteristic of the data at the target site where dependent write order is maintained to guarantee the recoverability of applications.
data record
A basic unit of data recording format. See also count key data, fixed-block architecture.
data reduction
A set of techniques that can be used to reduce the amount of usable capacity that is required to store data. Examples of data reduction include data deduplication and compression. See also data reduction savings, stored capacity.
data reduction savings
The total amount of usable capacity that is saved in a system, pool, or volume through the application of an algorithm such as compression or deduplication on the written data. This saved capacity is the difference between the written capacity and the used capacity. See also data reduction.
destage
To move data from cache to a nonvolatile storage medium.
distributed RAID
An alternative RAID scheme where the number of drives that are used to store the array can be greater than the equivalent, typical RAID scheme. The same data stripes are distributed across a greater number of drives, which increases the opportunity for parallel I/O and hence improves overall array performance. See also rebuild area.
DNS
See Domain Name System.
Domain Name System (DNS)
The distributed database system that maps domain names to IP addresses.
drive
A data storage device. A drive can be either a magnetic disk drive or a solid-state drive (SSD).
drive class
A combination of drive technology and speed, which uniquely defines a class of drives that have approximately the same performance characteristics.
drive technology
A category of a drive that pertains to the method and reliability of the data storage techniques being used on the drive. Possible values include enterprise (ENT) drive, nearline  (NL) drive, or solid-state drive (SSD).





E


ECKD
See extended count key data.
effective capacity
The amount of provisioned capacity that can be created in a system or pool without running out of usable capacity given the current data reduction savings being achieved. This capacity equals the usable capacity divided by the data reduction savings percentage.
enclosure
The metal structure in which various electronic components are mounted.
encryption deadlock
The inability to access encryption keys to decrypt data. See also encryption recovery key.
encryption key label
The list of encryption key labels used by the storage system to identify keys that will be used on the key server.
encryption key manager
See encryption key server.
encryption key server
An internal or external system that runs a key manager that receives and then serves existing encryption keys or certificates to a storage system.
encryption recovery key
An encryption key that allows a method to recover from an encryption deadlock situation where the normal encryption key servers are not available. See also encryption deadlock.
enterprise
Pertaining to a type of data storage device that has higher error recovery limits, vibration tolerance, and end-to-end error detection than standard desktop hard drives.
extended count key data (ECKD)
An extension of the count-key-data (CKD) architecture. It includes additional commands that can be used to improve performance.
extent type
See storage architecture type.





F


failback
The restoration of an appliance to its initial configuration after detection and repair of a failed network or component.
failover
An automatic operation that switches to a redundant or standby system or node in the event of a software, hardware, or network interruption.
FBA
See fixed-block architecture.
FC
See Fibre Channel.
FC-AL
See Fibre Channel Arbitrated Loop.
FCIP
See Fibre Channel over IP.
FCP
See Fibre Channel Protocol.
feature activation code
See license key.
Fibre Channel (FC)
A technology for transmitting data between computer devices. It is especially suited for attaching computer servers to shared storage devices and for interconnecting storage controllers and drives. See also zoning.
Fibre Channel Arbitrated Loop (FC-AL)
An implementation of the Fibre Channel standards that uses a ring topology for the communication fabric; refer to American National Standards Institute (ANSI) INCITS 272-1996, (R2001). In this topology, two or more Fibre Channel end points are interconnected through a looped interface.
Fibre Channel connection (FICON)
A Fibre Channel communication protocol designed for IBM mainframe computers and peripherals.
Fibre Channel extender
A device used to extend a Fibre Channel link over a greater distance than is supported by the standard, usually a number of miles or kilometers. Devices must be deployed in pairs at each end of a link.
Fibre Channel over IP (FCIP)
A network storage technology that combines the features of the Fibre Channel Protocol and the Internet Protocol (IP) to connect distributed SANs over large distances.
Fibre Channel Protocol (FCP)
The serial SCSI command protocol used on Fibre Channel networks. See also open system.
FICON
See Fibre Channel connection.
field-replaceable unit (FRU)
An assembly that is replaced in its entirety when any one of its components fails.
file module
A component that provides file systems to network users. A file module must be provided with storage for the file systems.
file system (FS)
A collection of files and certain attributes associated with those files.
file system storage
Data storage that is organized into files and directories.
fixed-block architecture (FBA)
An architecture for a virtual device that specifies the format of and access mechanisms for the virtual data units on the device. The virtual data unit is a block. All blocks on the device are the same size (fixed size). The system can access them independently. See also data record, storage architecture type.
fixed block
See fixed-block architecture.
FlashCopy
Pertaining to a point-in-time copy where a virtual copy of a volume is created. The target volume maintains the contents of the volume at the point in time when the copy was established. Any subsequent write operations to the source volume are not reflected on the target volume.
flash drive
A data storage device, which is typically removable and rewritable, that uses solid-state memory to store persistent data. See also flash module.
flash module
A modular hardware unit containing flash memory, one or more flash controllers, and associated electronics. See also flash drive.
flush-through mode
See write-through mode.
form factor
The industry-standard physical dimensions of a storage system drive enclosure. Possible values include “3.5 inch”, “2.5 inch”, and “1.8 inch.”
frame
The hardware support structure, covers, and all electrical parts mounted therein that are packaged as one entity for shipping.
FRU
See field-replaceable unit.
FS
See file system.
full restore operation
A copy operation where a local volume is created by reading an entire a volume snapshot from cloud storage.
full snapshot
A type of volume snapshot that contains all the volume data. When a full snapshot is created, an entire copy of the volume data is transmitted to the cloud. 





G


General Parallel File System (GPFS)
A high-performance shared-disk file system that can provide data access from nodes in a clustered system environment.
Global Mirror
A method of an asynchronous replication that maintains data consistency across multiple volumes within or across multiple systems. Global Mirror is generally used where distances between the source site and target site cause increased latency beyond what the application can accept.
GPFS
See General Parallel File System.





H


Hardware Management Console (HMC)
A system that controls managed systems, including the management of logical partitions and use of Capacity Upgrade on Demand. Using service applications, the HMC communicates with managed systems to detect and consolidate information, which can then be sent for analysis.
HMC
See Hardware Management Console.
host
A physical or virtual computer system that hosts computer applications, with the host and the applications using storage. See also client, host, server.
host cluster
A configured set of physical or virtual hosts that share one or more storage volumes in order to increase scalability or availability of computer applications.
host interface card
See interface card.
host object
A logical representation of a host within a storage system that is used to represent the host for configuration tasks.
hot-spare
Pertaining to redundant hardware (such as an adapter, a disk, a drive, or a server) that is installed and available in the event of a hardware failure.
HyperSwap
Pertaining to a function that provides continuous, transparent availability against storage errors and site failures, and is based on synchronous replication.





I


I/O
See input/output.
I/O enclosure
A hardware unit in a storage system where data is transferred into and out of the system.
incremental restore operation
A copy operation where a local volume is modified to match a volume snapshot by reading from cloud storage only the parts of the volume snapshot that differ from the local volume.
incremental snapshot
A type of volume snapshot where the changes to a local volume relative to the volume's previous snapshot are stored on cloud storage.
input/output (I/O)
Pertaining to a device, process, channel, or communication path involved in data input, data output, or both.
interface card
An optional part of a node canister that provides the system with additional host and storage connectivity options.
interface node
A node that connects a system to an Internet Protocol (IP) network for file-serving capabilities by using service protocols.
Internet Small Computer System Interface (iSCSI)
An IP-based standard for linking data storage devices over a network and transferring data by carrying SCSI commands over IP networks. See also Small Computer System Interface.
iSCSI
See Internet Small Computer System Interface.





K


key server
A server that negotiates the values that determine the characteristics of a dynamic virtual private network (VPN) connection that is established between two endpoints.







L


licensed capacity
The amount of capacity on a storage system that a user is entitled to configure.
license key
An alphanumeric code that activates a licensed function on a product.
license key file
A file that contains one or more licensed keys.





M


machine signature
A string of characters that identifies a system. A machine signature might be required to obtain a license key.
management node
A node that is used for configuring, administering, and monitoring a system.
maximum replication delay
The number of seconds that Metro Mirror or Global Mirror replication can delay a write operation to a volume.
Metro Global Mirror
A cascaded solution where Metro Mirror synchronously copies data to the target site. This Metro Mirror target is the source volume for Global Mirror that asynchronously copies data to a third site. This solution has the potential to provide a disaster recovery with no data loss at Global Mirror distances when the intermediate site does not participate in the disaster that occurs at the production site.
Metro Mirror
A method of synchronous replication that maintains data consistency across multiple volumes within the system. Metro Mirror is generally used when the write latency caused by the distance between the source site and target site is acceptable to application performance.





N


nearline
Pertaining to a type of storage in which data is available in a short amount of time, but not instantly.
nearline SAS drive
A drive that combines the high capacity data storage technology of a Serial Advanced Technology Attachment (SATA) drive with the benefits of a serial-attached SCSI (SAS) interface for improved connectivity.
node
A single processing unit within a system. For redundancy, multiple nodes are typically deployed to make up a system.





O


open system
A system that complies with industry-defined interoperability standards. An open system can be connected to other systems complying with the same standards. See also Small Computer System Interface, Fibre Channel Protocol.
order confirmation code
See authorization code.
overhead capacity
An amount of usable capacity that is occupied by metadata in a system or pool and other data that is used for system operations.
overprovisioned ratio
The ratio of provisioned capacity to usable capacity in a system or pool.
overprovisioning
The result of creating more provisioned capacity in a storage system or pool than there is usable capacity. Overprovisioning occurs when thin provisioning or data reduction techniques ensure that the used capacity of the provisioned volumes is less than their provisioned capacity.





P


parent pool
A storage pool that receives its capacity from MDisks and has, or will have, some of its capacity allocated to child pools. See also child pool.
performance group
A collection of volumes that is assigned the same performance characteristics. See also performance policy.
performance policy
A policy that specifies performance characteristics, for example quality of service (QoS). See also performance group.
PFC
See priority flow control.
pool
See storage pool.
pool pair
Two storage pools that are required to balance workload. Each storage pool is controlled by a separate node.
port
The physical entity within a host, system, or storage system that performs the data communication (transmitting and receiving) over the Fibre Channel.
priority flow control (PFC)
A link-level flow control mechanism, IEEE standard 802.1Qbb. PFC operates on individual priorities. Instead of pausing all traffic on a link, PFC is used to selectively pause traffic according to its class.
projected capacity
The estimated volume capacity that is available for volume creation, given the current average performance of any data compression, excluding thin-provisioning savings. See also thin-provisioning savings.
protocol
A set of rules controlling the communication and transfer of data between two or more devices or systems in a communication network.
provisioned capacity
The total capacity of all volumes and volume copies in a system or pool.





R


rack
A free-standing structure that can hold multiple servers, storage systems, chassis, switches, and other devices.
RAID
See Redundant Array of Independent Disks.
RAID 0
A data striping technique, which is commonly called RAID Level 0 or RAID 0 because of its similarity to common, RAID, data-mapping techniques. It includes no data protection, however, so, strictly speaking, the appellation RAID is a misnomer. RAID 0 is also known as data striping.
RAID 1
A form of storage array in which two or more identical copies of data are maintained on separate media.
RAID 10
A collection of two or more physical drives that present to the host an image of one or more drives. In the event of a physical device failure, the data can be read or regenerated from the other drives in the RAID due to data redundancy.
RAID 5
A form of parity RAID in which the disks operate independently, the data stripe size is no smaller than the exported block size, and parity check data is distributed across the array's disks.
RAID 6
A form of RAID that can continue to process read and write requests to all of an array's virtual disks in the presence of two concurrent disk failures.
RAID level
The level of protection provided by the specific techniques of striping, mirroring, or parity used by a Redundant Array of Independent Disks (RAID).
RAID type
See RAID level.
raw capacity
The reported capacity of the drives in the system before formatting or RAID (Redundant Array of Independent Disks) is applied.
rebuild area
Reserved capacity that is distributed across all drives in a redundant array of drives. If a drive in the array fails, the lost array data is systematically restored into the reserved capacity, returning redundancy to the array. The duration of the restoration process is minimized because all drive members simultaneously participate in restoring the data. See also distributed RAID.
reclaimable capacity
The amount of provisioned capacity that can be recovered without causing stress or performance degradation. This capacity identifies the amount of resources that can be reclaimed and provisioned to other objects in an environment.
reclaimed capacity
See reclaimable capacity.
recovery key
See encryption recovery key.
Redundant Array of Independent Disks (RAID)
A collection of two or more physical disk drives that present to the host an image of one or more logical disk drives. In the event of a physical device failure, the data can be read or regenerated from the other disk drives in the array due to data redundancy.
repo
See repository.
repository (repo)
A persistent storage area for data and other application resources.
reserved capacity
The amount of used capacity that is made up of capacity reserved for system use. See also total usable physical capacity.





S


SCSI
See Small Computer System Interface.
SCSI-FCP
See SCSI Fibre Channel Protocol.
SCSI device
A product, such as a drive or adapter, connected to a host through an I/O interface using the Small Computer System Interface (SCSI) protocol. A SCSI device is either an initiator,target, or both. See also Small Computer System Interface.
SCSI Fibre Channel Protocol (SCSI-FCP)
A standard that defines the protocol used to transfer Small Computer System Interface (SCSI) commands over the transport physical layer of the Fibre-Channel interface. This standard is published by ANSI as X3.269-1996.
SCSI initiator
The system component that initiates communications with attached targets.
SCSI target
A device that acts as a subordinate to a SCSI initiator and consists of a set of one or more logical units (LUs), each with an assigned logical unit number (LUN). The LUs on the SCSI target are typically I/O devices.
server
A computer program or a device that provides functions for other programs or devices, called clients. See also client, host.
Server Message Block (SMB)
A protocol that manages requests and responses in a client/server environment so that clients on a network can share files, directories, and devices.
Small Computer System Interface (SCSI)
An ANSI-standard electronic interface that allows personal computers to communicate with peripheral hardware, such as disk drives, tape drives, CD-ROM drives, printers, and scanners faster and more flexibly than previous interfaces. See also open system, Internet Small Computer System Interface, SCSI device.
SMB
See Server Message Block.
solid-state drive (SSD)
A storage device that contains nonvolatile flash memory. A solid-state drive (SSD) has no moving mechanical components.


space
See capacity.
space efficient
See thin provisioning.
spare drive
A drive reserved in an array for rebuilding a failed drive in a RAID.  Should a drive fail in a RAID, a spare drive from within that device adapter (DA) pair will be selected to rebuild it.
SSD
See solid-state drive.
standard-provisioned volume
A volume that completely uses storage at creation.
standard provisioning
The ability to completely use a volume's capacity for that specific volume.
storage architecture type (storage type)
The type of storage architecture, either count key data (CKD) or fixed block (FB), for which an array, pool, or volume is provisioned. See also count key data, fixed-block architecture.
storage enclosure
A specialized chassis that is designed to hold and power drives while providing a mechanism to allow them to communicate to one or more separate computers.
storage node
A component of a storage system that provides internal storage or a connection to one or more external storage systems.
storage pod
A subcomponent of a network-attached storage (NAS) system that consists of two or more storage nodes and one or more supported storage systems.
storage pool (pool)
A collection of storage that identifies an underlying set of resources. These resources provide the capacity and management requirements for a volume or set of volumes.
storage system
A system that provides persistent storage within a network. A storage system can include facilities for host attachment, user role authentication, a command-line interface (CLI), a graphical user interface (GUI), and storage devices that most often include Redundant Array of Independent Disks (RAID) controllers. It might also include agents for enabling third-party management software to monitor or manage the storage devices.
storage type
See storage architecture type.
stored capacity
The amount of capacity that is used to store data that is written by a host after data reduction See also data reduction, total usable physical capacity.
support assistance
A function that is used to provide support personnel access to the system to complete troubleshooting and maintenance tasks.
synchronous replication
A type of replication in which the application write operation is made to both the source volume and target volume before control is given back to the application. See also asynchronous replication.
syslog
A standard for transmitting and storing log messages from many sources to a centralized location to enhance system management.





T


thin-provisioned volume
A volume that allocates storage when data is written to it.
thin-provisioning savings
The total amount of usable capacity that is saved in a system, pool, or volume by consuming usable capacity only when needed as a result of write operations.  The capacity that is saved is the difference between the provisioned capacity minus the written capacity. See also volume capacity, projected capacity, written capacity.
thin provisioning
The ability to defer capacity allocation on a storage resource until data is actually written to it.
total capacity savings
The total amount of usable capacity that is saved in a system, pool, or volume through thin provisioning and data reduction techniques. This saved capacity is the difference between the used usable capacity and the provisioned capacity.
total usable physical capacity
The amount of physical configured storage space that is available for stored capacity or reserved capacity.  This capacity can consist of both internal storage through arrays and external storage through MDisks. See also reserved capacity, capacity threshold, stored capacity.
transparent cloud tiering
The functions that use cloud storage as an extension of on-premises storage.
trial license
A temporary entitlement to use a licensed function.
TSE for FlashCopy
A thin-provisioning method in which storage space is allocated from a TSE repository on an as needed basis. See also TSE repository.
TSE repository
The amount of capacity in a storage pool reserved for volumes that use a thin-provisioning method of TSE for FlashCopy. See also TSE for FlashCopy.





U


unmapped volume capacity
The amount of volume capacity that is not mapped to a host. See also volume capacity.
update
Software maintenance such as a manufacturing refresh, refresh pack, or fix pack that changes the modification level of a product.
To modify a file or data set with current information.
To apply fixes to a system.


upgrade
Any hardware or software change to a later release, or any hardware addition or software addition.
To install a new version or release of a product to replace an earlier version or release of the same product.


usable capacity
The amount of capacity that is provided for storing data on a system, pool, array, or MDisk after formatting and RAID techniques are applied.
used capacity
The amount of usable capacity that is taken up by data or overhead capacity in a system, pool, array, or MDisk after data reduction techniques have been applied.
user role
An identifier that is assigned to a user that defines the set of permissions that are granted to that user.





V


virtual capacity
See provisioned capacity.
virtualized capacity
The amount of capacity that is contributed to a storage pool by a given provisioning group.
virtual machine (VM)
An emulation of a particular computer system. Virtual machines operate based on the computer architecture and functions of a real or hypothetical computer. Their implementations might involve specialized hardware, software, or a combination of both.
VM
See virtual machine.
volume
A fixed amount of physical or virtual storage on a data storage medium.
volume access set
The set of I/O groups that allows host access to a volume. This set can optionally include the caching I/O group.
volume capacity
The total capacity for all volumes in a system or storage pool. Volume capacity is defined by the client when a volume is created and surfaced to the host. See also thin-provisioning savings, unmapped volume capacity.
volume snapshot
A collection of objects on a cloud storage account that represents the data of a volume at a particular time.





W


worldwide ID (WWID)
A name identifier that is unique worldwide and that is represented by a 64-bit value that includes the IEEE-assigned organizationally unique identifier (OUI).
worldwide name (WWN)
A 64-bit, unsigned name identifier that is unique.
worldwide node name (WWNN)
A unique 64-bit identifier for a host containing a Fibre Channel port. See also worldwide port name.
worldwide port name (WWPN)
A unique 64-bit identifier associated with a Fibre Channel adapter port. The WWPN is assigned in an implementation-independent and protocol-independent manner. See also worldwide node name.
write-through mode
A process in which data is written to a storage device at the same time as the data is cached.
written capacity
The amount of usable capacity that would have been used to store written data in a system or pool if data reduction was not applied. See also thin-provisioning savings.
written capacity limit
The largest amount of capacity that can be written to a drive, array, or MDisk. The limit can be reached even when usable capacity is still available.
WWID
See worldwide ID.
WWN
See worldwide name.
WWNN
See worldwide node name.
WWPN
See worldwide port name.





Z


z Global Mirror
A method of an asynchronous replication function that maintains data consistency across multiple volumes that are attached to a z/OS system. Time-based data consistency is maintained through the Data Facility Storage Management Subsystem (DFSMS) system data mover (SDM) component.
zoning
The grouping of multiple ports to form a virtual, private, storage network. Ports that are members of a zone can communicate with each other, but are isolated from ports in other zones. See also Fibre Channel.









