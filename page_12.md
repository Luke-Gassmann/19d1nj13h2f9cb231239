https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=fusion-prerequisites



Prerequisites
Prerequisite that you need for a successful setup and installation of IBM Storage Fusion.
ProcedureGo through the system requirements and confirm whether you meet all the requirements. For
detailed information about system requirements, see System requirements.
For the prerequisites of individual IBM Storage Fusion services, go through their respective
Before you begin section. For information about the services, see Managing services.

Ensure that you have the infrastructure and Red Hat®
OpenShift® Container Platform 4.12, 4.14, or 4.15.
 Note:

If you want to install Data Foundation 4.14 or 4.15
storage in consumer mode, then OpenShift Container Platform must also
be the same version. 
You can upgrade Red Hat
OpenShift Container Platform to the supported 4.15 version. However,
you cannot enable Data Cataloging service in an upgraded
IBM Storage Fusion 2.8 with Red Hat
OpenShift Container Platform 4.15.


For the supported version of Red Hat OpenShift Container Platform,
see https://www.ibm.com/support/pages/node/7081324.

Obtain IBM Entitlement Registry Key.  For the steps to obtain the key, see
Obtaining entitlement key.
Create a pull secret. For the actual steps to generate, see Creating image pull secret.For actual steps to create a pull secret for installing
IBM Storage Fusion on IBM cloud, see Creating image pull secret for IBM Cloud based installation.
If you plan to deploy IBM Storage Fusion on a
OpenShift Container Platform cluster with a cluster wide proxy
configured, then ensure you add these hosts to your allowlist:  

registry.redhat.io
quay.io
cp.icr.io
icr.io
redhat.com
registry.connect.redhat.com
catalog.redhat.com
access.redhat.com
cloud.redhat.com
cdn02.quay.io
registry.access.redhat.com
dd0.icr.io
dd2.icr.io
dd4.icr.io
dd6.icr.io


Note: This step is applicable only for on-premise deployments.






Obtaining entitlement key
Entitlement keys determine whether IBM Storage Fusion software operator can automatically pull the required container native images. During installation, image pull failures may occur due to an invalid entitlement key or a key belonging to an account that does not have entitlement to IBM Storage Fusion. 
Creating image pull secret
Create an image pull secret to enable the OpenShift cluster to authenticate with the IBM Entitled Registry. The image pull secret provides the credentials for pulling Docker images from the IBM Entitled Registry.
Creating image pull secret for IBM Cloud based installation
With OpenShift Container Platform, you can create a global image pull secret that each worker node in the cluster can use to pull images from a private registry and you can set up your Red Hat OpenShift on IBM Cloud cluster to pull entitled software.
System requirements
The system requirements for installing IBM Storage Fusion software.
SecurityContextConstraints
Red Hat OpenShift SecurityContextConstraints requirement controls pod permissions. These permissions include pod actions and resources that it can access. 


Parent topic: Deploying IBM Storage Fusion






