https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=whats-new



What's new
Each release offers new functions and improvements. IBM is constantly updating the
infrastructure, security, and stability of IBM Storage Fusion to improve your experience. Review
this information for a high-level summary of the new features and changes in each
release.
IBM Storage Fusion 2.8.0 includes new features in
the following areas: 
Backup & Restore
Data Cataloging
Service upgrades
Currency support




Backup & Restore

New recipes for Backup & Restore
Real enterprise applications go well beyond a single `Deployment` and one persistent volume. They
may include operators, span multiple namespaces, and require application data consistency across
dozens of persistent volumes. Fusion recipes eliminate the need for multi-page backup run-books by
orchestrating backups of even the most complex applications, and doing it all while the application
is online. This release includes new recipes for applications, including IBM Cloud Pak for AIOps.

Backup & Restore hardening and serviceability
improvements


Improved security by enabling the use of a read-only root file system by pod containers.
More detailed error messages for some common missing prerequisites and configuration errors that
lead to backup and restore failures.



Backup block-mode PVCs (Technical preview)
IBM Storage Fusion adds support for block-mode
persistent volumes. This complements the existing capabilities for backing up file-mode VMs. Now,
you can backup OpenShift® VMs regardless of how
they access storage. Support for backing up block-mode persistent volumes support applies to any
application workload; not just VMs. For more information about block-mode PVCs in IBM Storage Fusion, see Backup & Restore Block PVC Technical preview.




Data Cataloging

Harvesters data ingestion for NFS in Data Cataloging
The 2.8 version introduces harvesters as a new strategy for rapid ingestion of NFS distributed
data sources and data tagging. This novel way to accelerate the data ingestion on distributed NFS
data sources feature allows data cataloging users to take advantage of new entities called
harvesters to perform remote data scans and ingestion out of the cluster.
This new capability is useful in the following scenarios:
The data sources’ link speed from the data source to the cluster is low.
The constrains policies for mounting NFS on the cluster where Data Cataloging service is installed are restrictive

The harvester entity is a software that can be used in a single or multiple distributed
computing boxes and ingest data from it. 


IBM Db2 upgrade in Data Cataloging
The new IBM Db2 11.5.9 version is supported in
Data Cataloging service of IBM Storage Fusion 2.8. This new version provides security fixes,
defects correction, improvements to high availability and performance, and other updates. For more
information about IBM Db2, see What's new
in Db2 11.5.9.

Data Cataloging hardening

Different Data Cataloging security fixes and defect corrections
Supports the new AMQ Streams 2.6 version
Includes log trimmer improvements





Service upgrades

Backup & Restore and Data Cataloging service upgrades just got easier with built in
common pre-checks that automatically validate the health of these services. During upgrade, you can
easily monitor each step, with a clear understanding of what is in progress. If anything gets stuck,
a new guided workflow shows you what needs your attention and guides you with the resolution.



Currency support




Red Hat® OpenShift Container Platform versionIBM Storage Fusion HCI System supports OpenShift Container Platform 4.15.

IBM Storage Fusion service versions
IBM Storage Scale or Global Data Platform service 5.2.0.0
Fusion Data Foundation 4.15
Data Cataloging 2.1.6
Backup & Restore 2.8
For supported IBM Cloud Paks versions, see IBM Cloud Paks support for IBM Storage Fusion.












