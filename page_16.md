https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=prerequisites-system-requirements



System requirements
The system requirements for installing IBM Storage Fusion software.
The IBM Storage Fusion operators and your workloads run
on OpenShift® Container Platform that in turn are installed on amd64:
64-bit Intel, AMD x86, or Linux on IBM zSystems hardware
architecture. The following table lists the system requirements for IBM Storage Fusion software: Note: Though there is no minimum
number of nodes requirement, the following table provides data based on three control nodes and
three compute nodes cluster. However, sizing changes based on the number of nodes for components
with "Per node". IBM Fusion Data Foundation can be deployed
on Infra or worker nodes, whereas all other IBM Storage Fusion services including Base must be deployed on worker nodes.


Component
vCPUs 
Memory
Storage



IBM Storage Fusion Base
Request CPU: 4Limit CPU: 10

Request memory: 4 GiBLimit memory: 13 GiB

Overall storage is a minimum of 500 MB.


IBM Fusion Data Foundation 4.15.x


Internal mode (Local and dynamic) 

Request CPU: 22+2*(total count of Object Storage Daemon )
Limit CPU: 22+2*(total count of Object Storage Daemon)



External mode

Request CPU: 4
Limit CPU: 5



For IBM Power Systems:
Internal mode
48 CPU (logical)



External mode
24 CPU (logical)



Internal mode (Local and dynamic) 

Request memory: 56+5*(total count of Object Storage Daemon) GiB
Limit memory: 56+5*(total count of Object Storage Daemon) GiB



External mode

Request memory:16 GiB
Limit memory: 16 GiB



For IBM Power Systems:
Internal mode
192 GiB memory


External mode
48 GiB memory


Minimum three storage NodesFor more information about IBM Fusion Data Foundation, see Important considerations when deploying Red Hat OpenShift Data
Foundation.

For IBM Power Systems:
Internal
3 storage devices, each with additional 500 GB of disk




Global Data Platform



Per node

Request CPU: 10% (total vCPU of the node)



Cluster

Request CPU: 3
Limit CPU: 12





Per node

Request memory: 10% (total memory of the node)



Cluster

Request memory: 13
Limit memory: 30



For more information about IBM Spectrum Scale Container Native Storage Access, see Hardware requirements for IBM Storage Scale Container Native Storage
Access.


Backup & Restore hub

Request CPU: 5
Limit CPU: 30


Request memory: 17 GiB
Limit memory: 41 GiB

200 GB Minimum


Backup & Restore spoke

Request CPU: 2
Limit CPU: 8


Request Memory: 2 GiB
Limit Memory 7 GiB

10GiB


Data Cataloging

Request CPU: 14
Limit CPU: 77


Request memory: 29 GiB
Limit memory: 162 GiB

500 GB MinimumFor more information about Data Cataloging, see Data Cataloging.




The following table lists the component versions: 
Component
Versions


On-premises VMware
Version 7.0 


On-premises IBM z/OS Container
Extensions (IBM zCX)
All the zCX hypervisor versions on
which OpenShift Container Platform is supported.


Red Hat®
OpenShift Container Platform
4.12, 4.14, 4.15Note:  You can upgrade Red Hat
OpenShift Container Platform to the supported 4.15 version. However,
you cannot enable Data Cataloging service in an upgraded
IBM Storage Fusion 2.8.0 with Red Hat
OpenShift Container Platform 4.15.



Storage
IBM Fusion Data Foundation 4.12, 4.14, and 4.15 



Note: For deployment platforms and supported services, see IBM Storage Fusion Services support matrix.



IBM Storage Scale
Remote mount of IBM Storage Scale storage:
Note:
IBM Storage Fusion 2.8.0 or higher supports IBM Storage Scale 5.2.0.0.

IBM Storage Scale remote storage cluster
release 5.1.3 or higher.
The IBM Storage Fusion cluster accesses the storage
owned by an IBM Storage Scale storage cluster by
using a remote mount.
The
IBM Storage Scale file system version of the
owning storage cluster cannot be newer than version 33.00. 
For more information, see Software requirements.
To determine the version of your IBM Storage Scale cluster, run the mmdiag
--version command on the IBM Storage Scale cluster. To determine the version
of your IBM Storage Scale file system, run the
mmlsfs all -V
command.For
further information, including installation/upgrade instructions for the remote IBM Storage Scale cluster, see IBM Storage Scale
documentation.







Backup & Restore

IBM Storage Fusion supports backup and recovery
operations on Red Hat
OpenShift Container Platform environment on AMD64 with any storage
provider that implemented the Container Storage Interface (CSI) driver and meets the following prerequisites:
The Container Storage Interface driver must be v1 or higher (no support for alpha or
beta versions)
The Container Storage Interface driver must support Volume Snapshot and Restore.
StorageClass must be created with volumeBindingMode: Immediate
(volumeBindingMode: WaitForFirstConsumer is not supported) and
allowVolumeExpansion: true.
PersistentVolume (PV) must be created with volumeMode: Filesystem
(volumeMode: Block is not supported)

Note: It is also recommended that the VolumeSnapshotClass deletion policy is
configured to delete snapshots after the corresponding VolumeSnapshotContent is
deleted (deletionPolicy: Delete).
Note: For backups of PVCs provisioned on
IBM Storage Scale, snapshots are be created only
from independent fileset-based persistent volume claims (PVCs). PVCs that are based on lightweight
directories and dependent file sets are not supported.








Parent topic: Prerequisites






