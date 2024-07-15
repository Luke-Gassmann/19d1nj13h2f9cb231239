https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=fusion-installing-storage-premises-power-systems



Installing IBM Storage Fusion on On-premises
IBM Power Systems
Procedure to install IBM Storage Fusion on OpenShift® Container Platform that runs on On-premises
IBM Power Systems.
Before you begin

If you plan to do an offline installation of IBM Storage Fusion, see Enterprise registry for IBM Storage Fusion
installation.
Ensure you complete all the prerequisites before you proceed with the installation. For the
prerequisites, see Prerequisites.
For more information about deployments and their supported services, see IBM Storage Fusion Services support matrix.


About this task
Support is available for only one instance of IBM Storage Fusion per OpenShift Container Platform.

ProcedureIf you have not configured the IBM Operator Catalog, then configure it. For the procedure
to add IBM Operator catalog, see Adding the IBM operator catalog.  
Note:

IBM Operator Catalog is not specific to a version of IBM Storage Fusion. 
If you already have the IBM Maximo® software
configured in your environment or have plans to configure it, use only the
ibm-operator-catalog of IBM Maximo®
software. 



Log in to Red Hat®
OpenShift Container Platform web management console.
Go to
Operators > OperatorHub.
Under Source, select IBM Operator Catalog.
 It lists all operators that are part of the IBM Operator Catalog including IBM
Storage Fusion. 
Click IBM Storage Fusion. The
Version, Capability level,
Source, and Provider type of IBM Storage Fusion is available.
Click Install.  It opens the Install
Operator page for IBM Storage Fusion operator. 
Select v2.0 in the update channel where the current operator is
published.  
Note: You can also subscribe for updates. The subscription to the channel helps to keep the operator
up to date. 

In the Installation mode, select A specific namespace
on the cluster. The operator will be available in a single Namespace
only.
Select ibm-spectrum-fusion-ns in the Operator recommended
namespace. Alternatively, use the Select a namespace option to
select an existing namespace or create a new namespace. 
Important: Always set Update approval to
Manual as IBM Storage Fusion does not
support Automatic.
In the Update approval
section, you can select either Manual or Automatic
strategy. Always set Update approval to
Manual because the Automatic option automatically
upgrades the operator whenever a new version of the operator is released to the channel. This
automatic upgrade might have an impact on your running workloads.
Click Install.  The installation of the operator
begins. 
Wait for the operator to complete the installation.  After the
successful installation of the operator, the following message gets displayed:
Installed operator - operand required
Generally, it completes in few minutes.
If it takes more time, check whether all pods are up and running.

Note: If
you notice that installation is taking longer than usual or failed, then check the events tab on the
installed-opertor or fusion-operator page. In the events tab, if
you see an error waiting for deployment of serviceability-operator, ignore it and
continue with the installation.

From the Applications menu in the title bar of OpenShift Container Platform, click IBM Storage Fusion.  The License
agreement page gets displayed.
Go through the license agreement, click I have read and accept the
license agreement, and click
Continue. The
Welcome to IBM Storage Fusion dialog box gets displayed.
In the IBM Storage Fusion user
interface, click Install services to install the services right away or click
Maybe later to do it later.

What to do next


For steps to verify the success of the installation, see Validating IBM Storage Fusion installation. 
If you want to enable the services from the IBM Storage Fusion user interface, see the following procedures accordingly:
For Data Cataloging, see Data Cataloging.
For Data Foundation, see Data Foundation.
For Backup & Restore, see Backup & Restore.

If you want to install IBM Storage Fusion services
using OpenShift Container Platform, then see Deploying services from OpenShift Container Platform.Important: To know more about the supported
services for your platform, see IBM Storage Fusion Services support matrix.

To know more about the user interface of IBM Storage Fusion, see Knowing your IBM Storage Fusion user interface.






Parent topic: Deploying IBM Storage Fusion






