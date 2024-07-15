https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=installation-mirroring-your-images-enterprise-registry



Mirroring your images to the enterprise registry
If you are planing a disconnected or offline installation, then you must mirror images to
your enterprise registry.
Before you begin


The registry must have at least one directory path specified. For
example:
https://<enterprise registry host>:<enterprise registry port>/<mandatory root path>
Considerations for your enterprise registry: 
There must not be a huge latency between cluster nodes and your enterprise registry.
You must have a container image registry that supports Docker v2-2 in the location that hosts
the Red Hat®
OpenShift® Container Platform cluster. For more information about
image manifest, see opm CLI reference .Important: Artifactory is the
recommended registry because it supports the following must have capabilities: 
Import and export 
Untagged images


JFrog Artifactory version 7.55.8 is tested on IBM Storage Fusion. The port that is specified in the URL is
used to login and pull the images from the enterprise repository. For a secured enterprise registry,
specify 443. If you do not provide the port value, then no default port is considered in its
absence. The API key is the only supported authentication method.



Ensure that your secure enterprise registry is already setup and ready for use.
Prepare your mirroring host: 
The mirror host must have access to internet and enterprise registry.
Ensure that you install the following tools on your system from where you can connect to Red Hat registry and enterprise registry: 
Install Docker or Podman.
Install opm CLI tool. For more information about installing
opm CLI tool, see Installing the opm CLI.
Install skopeo 1.14 or higher for image
copy operation. For more information to install skopeo, see https://github.com/containers/skopeo.
Install oc command tool from any of the Red Hat
OpenShift Container Platform cluster:
Log in to the system from where you want to run commands.
Log in to OpenShift Container Platform.
Click bell icon and select Command line tools.
Click the appropriate oc download option based on your operating
system.

Alternatively, you can also download the platform based oc client from the
following OpenShift Container Platform link: https://mirror.openshift.com/pub/openshift-v4/clients/ocp/4.10.21/.
For example, use the following link to download oc client
for Linux platform: https://mirror.openshift.com/pub/openshift-v4/clients/ocp/4.10.21/openshift-client-linux-4.10.21.tar.gz.

Download pull-secret.txt.To download pull-secret, see https://console.redhat.com/openshift/install/pull-secret and follow the
instructions.
Edit the downloaded pull-secret with registry
credentials:
Add a new section of key-value pair under auths. For
example,"<Your enterprise registry>:<port>": {
"auth": "<base64 encoded 'user_name:password'>",
email: "<your email>" }See the following sample values:
{ 
"auths": { 
   "cloud.openshift.com": { 
      .... 
   "registryhost.com:443": { 
       "auth": "dXNlcl9uYW1lOnBhc3N3b3Jk",   
        "email": "user_name@ibm.com" 
    }
  }
}

Here, user_name and password are credentials to
connect to enterprise registry.Note: If you want to use multiple repositories, add auth section for
both repositories.






Ensure that you have entitlement key to access IBM Storage Fusion images. 

Note:

Ensure that the  LOCAL_ISF_REPOSITORY path and TARGET_PATH of
the IBM Storage Fusion and IBM Storage Scale images must be same. 
IBM Storage Fusion 2.8.0 or higher supports IBM Storage Scale
5.2.0.

For example, if you use LOCAL_ISF_REPOSITORY=sds/mirror-2.8.0 while mirroring
IBM Storage Fusion images, the same path must be used for
IBM Storage Scale.






About this taskPoints to note about this task: 
Repository and target path must be same for IBM Storage Fusion and IBM Storage Scale.
Run all commands as root user.
In the commands, replace <your enterprise registry> with your enterprise
registry and its corresponding pull-secret.
If you use a non-default port (other than 443), then append a colon and port number after your
enterprise registry value. For example, <Your enterprise registry>:9443. 
You must mirror images to a single repository, a single registry, and a single path.
Depending on which IBM Storage Fusion services you
want to enable you can choose to only mirror images for that service, however you must mirror IBM Storage Fusion images.


ProcedureRun the following steps to mirror IBM Storage Fusion images. For the actual
procedure, see Mirroring IBM Storage Fusion images.
Mirror IBM Storage Scale
images. For the actual procedure, see Mirroring IBM Storage Scale images.

Mirror Data Foundation images deployed on OpenShift Container Platform version 4.12. For the actual
procedure, see Mirroring Data Foundation images deployed on OpenShift Container Platform 4.14 or higher using ImageDigestMirrorSet.
Mirror Backup & Restore images.
 For the actual procedure, see Mirroring Backup & Restore images.
Mirror Data Cataloging images. For
the actual procedure, see Mirroring Data Cataloging images.







