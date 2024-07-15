https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=upgrading-storage-fusion



Upgrading IBM Storage Fusion

Procedure to upgrade IBM Storage Fusion to 2.8. 
Before you begin


For 2.8, you must be on IBM Storage Fusion version 2.7.2. 
If you installed IBM Storage Fusion version 2.7.2 by
using online or your enterprise registry installation mode, then ensure that you do not change the
mode during the upgrade to 2.8 version.
To change the installation mode, reinstall IBM Storage Fusion.
Ensure all compute nodes are in ready state on OpenShift® user interface.
Download the logs that you collected by using IBM Storage Fusion. The Collect logs user interface page gets
deleted after the upgrade process completes so download the needed logs before you begin the
upgrade. 
If you installed the earlier version of IBM Storage Fusion by using your enterprise registry, then do these additional mirroring prerequisites steps. See
Prerequisites for enterprise registry upgrade.



Procedure
Log in to the OpenShift Container Platform management console as
the cluster administrator.
Upgrade IBM Storage Fusion: 

From the navigation menu, click
Operators > Installed
Operators.
From the Installed Operators list, click IBM Storage
Fusion operator. The Details tab opens by
default. 
Go to Subscription tab.
View the Subscription details section for the upgrade status.  
Note: If this is an offline setup, then update the image path in IBM Storage Fusion catalog source with new catalog source
image.

If an upgrade is available for the operator, then click Approve
to manually initiate the upgrade. If you do not agree to the upgrade, click
Deny.  If no new upgrade is available, then Upgrade
status displays Up to date. Note: By default, the upgrade of the
IBM Storage Fusion is Automatic. However, you can change
it to Manual.

After the upgrade is successful, refresh your browser and clear your
cache.
Verify whether the IBM Storage Fusion is in
succeeded state and the version is 2.8.0.
Also, in the Subscription tab, ensure that the upgrade status displays
Up to date.


Upgrade IBM Storage Fusion services.
 For the steps to upgrade services, see Upgrading IBM Storage Fusion services.
Upgrade Red Hat® OpenShift Container Platform from Red Hat OpenShift Container Platform console.  
Note: The Red Hat OpenShift Container Platform version must be
upgraded only to the version supported by IBM Storage Fusion. Do not upgrade or rollback your Red Hat OpenShift Container Platform version manually until
the support is included in IBM Storage Fusion. 
For the upgrade procedure, Red Hat OpenShift Container Platform, see Understanding OpenShift Container Platform
updates.




Prerequisites for enterprise registry upgrade
If you installed the earlier version of IBM Storage Fusion by using your enterprise registry, then mirror the 2.8.0 images to your enterprise registry.
Upgrading IBM Storage Fusion services
From the IBM Storage Fusion user interface, upgrade the IBM Storage Fusion services, namely Data Foundation, Global Data Platform, Backup & Restore, and Data Cataloging.
Upgrading Red Hat OpenShift Data Foundation 4.12 to IBM Storage Fusion Data Foundation 4.12 or higher
Steps to upgrade Red Hat Data Foundation 4.12 to IBM Storage Fusion Data Foundation 4.12 or higher.






