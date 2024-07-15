https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=disaster-recovery



Disaster recovery
Metro-DR is a disaster recovery solution supported by IBM Storage Fusion. 


Data Foundation can be configured in two OpenShift® clusters to use a shared stretched Ceph cluster. For information about steps to
configure this solution, see Configuring Data Foundation for Disaster Recovery.
Regional-DR solution is designed to protect your applications against a wide range of large
blast radius failures and disaster scenarios like data center failures. As an IBM Storage Fusion
user, you can use Data Foundation to configure the Regional-DR solution that offers Disaster
Recovery protection with ODF-based asynchronous volume replication for both block and file volumes.
For more information about the solution, see Regional-DR solution for Fusion Data Foundation.


Note: In disaster recovery, two clusters must be connected to failover and failback applications. If
the cluster recovers after the expiry of the client cert, clean and and setup the connection to
rejoin the recovered cluster. For the procedure to rejoin, see Reconnecting OpenShift Container Platform cluster.






