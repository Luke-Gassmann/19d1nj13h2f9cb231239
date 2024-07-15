https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=accessing-remote-storage-scale-storage-cluster-in-storage-fusion



Accessing remote IBM Storage Scale storage
cluster in IBM Storage Fusion
You can configure a remote file system mount for IBM Storage Scale and access it. The container native data access is only for IBM Storage Fusion on On-premises, Bare Metal, VMware, and Amazon Web Services deployments. 
Before you begin

For remote filesystem of Amazon Web Services storage
cluster, ensure that you deploy a Amazon Web Services
storage cluster. For more information about the storage, see AWS storage cluster.
For the remotely mounted storage cluster, after its filesystem level is updated to 28.00 (5.1.4)
or later, it is recommended to enable --auto-inode-limit on its filesystem for IBM Storage Fusion. For more information about how to
enable, see mmchfs command.
To access the container native data, you must first add a file system. To add a new remote file
system connection, see Connecting to remote IBM Storage Scale file systems.
To understand the number of file systems and clusters that can be remotely mounted, see IBM Spectrum Scale container native limitations.


About this task
Note: The Global Data Platform remote mount capability is
available only for the following deployment modes: 
Standalone rack with Global Data Platform storage ( newly
installed with IBM Storage Fusion 2.8.0)
Standalone rack with FDF ( upgraded to IBM Storage Fusion 2.8.0 / newly installed with IBM Storage Fusion 2.8.0)


You can run a container workload against an existing data set that is stored on an IBM Storage Scale file system. For example, an IBM Storage Scale file system contains lot of images
and you want to run a container workload that specializes in image processing.

The remote file system mount must be configured. For more information, see Connecting to remote IBM Storage Scale file systems.
When the remote file system mount is created, the IBM Storage Fusion automatically creates a statically
provisioned volume that points to the file system. You must know how to identify this Persistent
Volume.
Optionally, modify the file system path that is specified in the Persistent Volume so that it
points to a specific directory in the file system, rather than the root.
Now a Persistent Volume Claim (PVC) can be made against the Persistent Volume. It can be
accomplished by matching the accessMode and storage request against the specified
in the Persistent Volume.
A workload that uses the Persistent Volume Claim can view the contents of the file system.

Configure the UID/GID to match the one that is used to write the data set on the IBM Storage Scale file system. If you do not
configure, then the container workload cannot access the files, because it does not have the
permission.

Procedure
Click Storage > Remote file
systems menu in the IBM Storage Fusion user interface. 
It lists all existing connections to file systems with their details in a table format.
The details include File System, FS status,
Cluster, Cluster status, and Storage
class. You can enter keywords in Search to search for a
connection. You can also filter records based on the status. 
Click ellipsis of a remote file system record to do the following actions:  
Details - Click to view details about the remote file system
connection.
Edit cluster - Click to change the cluster of a file system
connection.
Remove - Click to delete a file system record. 









