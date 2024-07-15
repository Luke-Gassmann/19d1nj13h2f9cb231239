https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=myier-mirroring-data-foundation-images-deployed-openshift-container-platform-414-higher-using-imagedigestmirrorset



Mirroring Data Foundation images deployed on OpenShift Container Platform
4.14 or higher using
ImageDigestMirrorSet
Mirror the Data Foundation images to your
enterprise registry by using ImageDigestMirrorSet.
Before you begin

Ensure that you use OpenShift® Container Platform 4.14.4 or higher in the commands. Use your
specific version number in the commands. 
In 2.8.0, make sure OpenShift Container Platform version is at
least 4.14.4 or higher.

You can migrate the Fusion Data Foundation
ImageContentSourcePolicy to an ImageDigestMirrorSet. For the procedure and why you must migrate, see
Migrating your Data Foundation ImageContentSourcePolicy to ImageDigestMirrorSet.


About this task
The Fusion Data Foundation 4.14 with OpenShift Container Platform 4.14 is used in the procedure as an example.
Replace it with your appropriate supported version. 
For more information about how to plan for this setup in a network restricted Data Foundation, see Disconnected environment.
Note: This procedure is only necessary if you plan to enable the IBM Fusion Data Foundation service.

ProcedureRun the following command to login to Docker registry with your Red
Hat® enterprise credentials: 
docker login registry.redhat.io -u <Red Hat enterprise registry username> -p <Red Hat enterprise registry password>


Log in to the IBM Entitled Container Registry by using the IBM entitlement key:  
docker login cp.icr.io -u cp -p <your entitlement key>
Note: Ensure that your entitlement key for IBM Storage Fusion contains the correct entitlement.
Set the following environment variables: 
export LOCAL_ISF_REGISTRY="<Your enterprise registry host>:<port>" 
export LOCAL_ISF_REPOSITORY="<Your image path>" 
export TARGET_PATH="$LOCAL_ISF_REGISTRY/$LOCAL_ISF_REPOSITORY" 
export OCP_VERSION="<Your ocp version, eg 4.14>" Note: Port is a non-mandatory value
when you set the LOCAL_ISF_REGISTRY variable. If your enterprise registry is
accessible and has a secure connection, then you can ignore it.
Sample value for without
port:export LOCAL_ISF_REGISTRY="registryhost.com"
See the following sample values:
export LOCAL_ISF_REGISTRY="registryhost.com:443"
export LOCAL_ISF_REPOSITORY="fusion-mirror"

LOCAL_ISF_REGISTRY is your entitlement registry.
LOCAL_ISF_REPOSITORY is the image path in which you want to mirror the images.
You can choose your own repository paths. For example, in , the name can be
sds-2.8.0/isf or sds-2.8.0.


Run the command to login to the Docker registry with your enterprise registry
credentials: 
docker login $LOCAL_ISF_REGISTRY -u <your enterprise registry username> -p <your enterprise registry password>


Create the image set configuration for IBM Fusion Data Foundation. See the following image set
configuration:
cat << EOF > imageset-config-fdf.yaml
kind: ImageSetConfiguration
apiVersion: mirror.openshift.io/v1alpha2
storageConfig:
  registry:
    imageURL: "$TARGET_PATH/isf-df-metadata:latest"
    skipTLS: true
mirror:
  operators:
    - catalog: icr.io/cpopen/isf-data-foundation-catalog:v<OCP_VERSION>
      packages:
        - name: "mcg-operator"
        - name: "ocs-operator"
        - name: "odf-csi-addons-operator"
        - name: "odf-multicluster-orchestrator"
        - name: "odf-operator"
        - name: "odr-cluster-operator"
        - name: "odr-hub-operator"
        - name: "ocs-client-operator"
EOF


Run the following oc command to mirror the images: 
oc mirror --config imageset-config-fdf.yaml docker://${TARGET_PATH} --dest-skip-tls --ignore-history


Run the following command to check whether the image got successfully mirrored to the
registry: 

oc mirror list operators --catalog <enterprise registry host:port>/<target-path>/cpopen/isf-data-foundation-catalog:v4.14

WARN[0033] DEPRECATION NOTICE:

Sqlite-based catalogs and their related subcommands are deprecated. Support for them will be removed in a future release. Please migrate your catalog workflows
to the new file-based catalog format.

NAME                               DISPLAY NAME                   DEFAULT                  CHANNEL

mcg-operator                       NooBaa                         Operator                 stable-4.14

ocs-client-operator                OpenShift Data Foundation      Client                   stable-4.14

ocs-operator                       Container                      Storage                  stable-4.14

odf-csi-addons-operator            CSI                            Addons                   stable-4.14

odf-multicluster-orchestrator      Multicluster                   Orchestrator             stable-4.14

odf-operator                       IBM Storage Fusion             Data Foundation          stable-4.14

odr-cluster-operator               DR Cluster                     Operator                 stable-4.14

odr-hub-operator                   DR Hub                         Operator                  stable-4.14


Create the image set configuration for local storage operator. See the
following image set configuration:cat << EOF > imageset-config-lso.yaml
kind: ImageSetConfiguration
apiVersion: mirror.openshift.io/v1alpha2
storageConfig:
  registry:
    imageURL: "$TARGET_PATH/df/odf-lso-metadata:latest"
    skipTLS: true
mirror:
  operators:
    - catalog: registry.redhat.io/redhat/redhat-operator-index:v<OCP_VERSION>
      packages:
        - name: "local-storage-operator"
        - name: "lvms-operator"
EOF
Run the following OC command to mirror the
images:oc mirror --config imageset-config-lso.yaml docker://${TARGET_PATH} --dest-skip-tls --ignore-history
Note: If Red Hat® operator catalog is
running on your cluster, prune and push all earlier packages, including the
local-storage-operator and lvms-operator. Otherwise, old packages
get lost from the Red Hat operator index image.


Add ImageDigestMirrorSet for IBM Fusion Data Foundation.  
Note: The ImageDigestMirrorSet contains a list of repositories, copy digests for
the IBM Fusion Data Foundation.
See the following ImageDigestMirrorSet:
Note: Replace the variable $TARGET_PATH with your registry details where images are
mirrored. 


apiVersion: config.openshift.io/v1
kind: ImageDigestMirrorSet
metadata:
labels:
operators.openshift.org/catalog: "true"
name: isf-fdf-idsp
spec:
imageDigestMirrors:
- mirrors:
  - <enterprise registry host:port>/<target-path>/openshift4
  source: registry.redhat.io/openshift4
- mirrors:
  - <enterprise registry host:port>/<target-path>/redhat
  source: registry.redhat.io/redhat
- mirrors:
  - <enterprise registry host:port>/<target-path>/rhel8
  source: registry.redhat.io/rhel8
- mirrors:
  - <enterprise registry host:port>/<target-path>/cp/df
  source: cp.icr.io/cp/df
- mirrors:
  - <enterprise registry host:port>/<target-path>/cpopen
  source: cp.icr.io/cpopen
- mirrors:
  - <enterprise registry host:port>/<target-path>/cpopen
  source: icr.io/cpopen
- mirrors:
  - <enterprise registry host:port>/<target-path>/cp/ibm-ceph
  source: cp.icr.io/cp/ibm-ceph
- mirrors:
  - <enterprise registry host:port>/<target-path>/lvms4
  source: registry.redhat.io/lvms4

Create a CatalogSource named
redhat-operators. 
Note: Do this step when the Data Foundation uses the
local disk.

apiVersion: operators.coreos.com/v1alpha1
kind: CatalogSource
metadata:
 name: redhat-operators
 namespace: openshift-marketplace
spec:
 displayName: Red Hat Operators
 image: <enterprise registry host:port>/<target-path>/redhat/redhat-operator-index:v<OCP_VERSION>
 publisher: Red Hat
 sourceType: grpc

Add ImageTagMirrorSet for Data Foundation: 

apiVersion: config.openshift.io/v1
kind: ImageTagMirrorSet
metadata:
  name: isf-fdf
spec:
  imageTagMirrors:
    - mirrors:
      - <enterprise registry host:port>/<target-path>/df/isf-data-foundation-catalog
      source: icr.io/cpopen/isf-data-foundation-catalog 
   mirrorSourcePolicy: 
       AllowContactingSource 0









