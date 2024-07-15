https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=myier-mirroring-data-foundation-images-deployed-openshift-container-platform-412-413-using-imagecontentsourcepolicy



Mirroring Data Foundation images deployed on OpenShift Container Platform
4.12 or 4.13 using
ImageContentSourcePolicy
Mirror the Data Foundation images to your
enterprise registry by using the ImageContentSourcePolicy.
Before you begin

Make sure that you install the oc-mirror
OpenShift CLI
plug-in. For more information about oc-mirror
OpenShift CLI plug in
installation, see Installing the oc-mirror OpenShift CLI plugin.
Make sure that the OpenShift® Container Platform version is 4.12 or 4.13.

Note: For mirroring Fusion Data Foundation 4.14 or higher
images, use  ImageDigestMirrorSet. For the procedure, see Mirroring Data Foundation images deployed on OpenShift Container Platform 4.14 or higher using ImageDigestMirrorSet.



About this task
The version Fusion Data Foundation 4.12
with OpenShift Container Platform 4.12 is used in the procedure as an
example. Replace it with your appropriate supported versions. 
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
Note: Port is a non-mandatory value when you set the LOCAL_ISF_REGISTRY
variable. If your enterprise registry is accessible and has a secure connection, then you can ignore
it.
Sample value for without
port:export LOCAL_ISF_REGISTRY="registryhost.com"
See the following sample values:
export LOCAL_ISF_REGISTRY="registryhost.com:443"
export LOCAL_ISF_REPOSITORY="fusion-mirror"

LOCAL_ISF_REGISTRY is your entitlement registry.
LOCAL_ISF_REPOSITORY is the image path in which you want to mirror the images.
You can choose your own repository paths. 
For example, in , the name can be sds-2.8.0/isf or sds-2.8.0.


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
    - catalog: icr.io/cpopen/isf-data-foundation-catalog:v4.12
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

Run the following oc command to mirror the
images:oc mirror --config imageset-config-fdf.yaml docker://${TARGET_PATH} --dest-skip-tls --ignore-history


Ensure the catalog is mirrored. 
oc mirror list operators --catalog <enterprise registry host:port>/<target-path>/cpopen/isf-data-foundation-catalog:v4.12

WARN[0020] DEPRECATION NOTICE:

Sqlite-based catalogs and their related subcommands are deprecated. Support for
them will be removed in a future release. Please migrate your catalog workflow to the new file-based catalog format.

NAME                               DISPLAY                     NAME            DEFAULT CHANNEL

mcg-operator                        NooBaa                     Operator          stable-4.12

ocs-client-operator                 OpenShift Data Foundation  Client            stable-4.12

ocs-operator                        Container                   Storage          stable-4.12

odf-csi-addons-operator             CSI                         Addons           stable-4.12

odf-multicluster-orchestrator       Multicluster                Orchestrator      stable-4.12

odf-operator                        IBM Storage Fusion          Data Foundation   stable-4.12

odr-cluster-operator                DR Cluster                  Operator          stable-4.12

odr-hub-operator                    DR Hub                      Operator          stable-4.12


Create the image set configuration for local storage operator. See the following image set
configuration:cat << EOF > imageset-config-lso.yaml
kind: ImageSetConfiguration
apiVersion: mirror.openshift.io/v1alpha2
storageConfig:
  registry:
    imageURL: "$TARGET_PATH/df/odf-lso-metadata:latest"
    skipTLS: true
mirror:
  operators:
    - catalog: registry.redhat.io/redhat/redhat-operator-index:v4.12
      packages:
        - name: "local-storage-operator"
        - name: "lvms-operator"
EOF
Run the following oc command to mirror the
images:oc mirror --config imageset-config-lso.yaml docker://${TARGET_PATH} --dest-skip-tls --ignore-history
Note: If Red Hat® operator catalog is
running on your cluster, prune and push all earlier packages, including the
local-storage-operator and lvms-operator. Otherwise, old packages
get lost from the Red Hat operator index image.


Add ImageContentSourcePolicy for IBM Fusion Data Foundation. 
Note: The ImageContentSourcePolicy contains list of repositories, copy digests for
the IBM Fusion Data Foundation.
See the following ImageContentSourcePolicy:Note: Replace the variable
$TARGET_PATH with your registry details where images are mirrored.

apiVersion: operator.openshift.io/v1alpha1
kind: ImageContentSourcePolicy
metadata:
  name: isf-fdf-icsp
spec:
  repositoryDigestMirrors:
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
 image: <enterprise registry host:port>/<target-path>/redhat/redhat-operator-index:v4.12
 publisher: Red Hat
 sourceType: grpc

Get Data Foundation catalog image
digest. skopeo inspect docker://<enterprise registry host:port>/<target-path>/cpopen/isf-data-foundation-catalog:v4.12 | jq -r ".Digest"
Example Output:
sha256:2d9e78d69a457b722cf6037968dae5f48eccd9e48ef4369a7fe661de0d96df95
To
install the Skopeo tool, see https://github.com/containers/skopeo/blob/main/install.md.

Add Data Foundation catalog image
digest: 
Follow the IBM Storage Fusion installation
documentation. Wait for Data Foundation
service to show up in the Services page. 
Add Data Foundation catalog image digest to
FusionServiceDefinition CR.
Run the following OC command:
 oc edit fusionservicedefinition data-foundation-service -n ibm-spectrum-fusion-ns
Here, replace ibm-spectrum-fusion-ns with your Fusion namespace. 
Update  .spec.onboarding.serviceOperatorSubscription.multiVersionCatSrcDetails.ocp412-t.imageDigest
with the actual image digest value you got in step 9 or
run the following OC command:  oc patch fusionservicedefinition data-foundation-service -p '{"spec":{"onboarding":{"serviceOperatorSubscription":{"multiVersionCatSrcDetails":{"ocp412-t":{"imageDigest":"<Digest>"}}}}}}' --type=merge -n ibm-spectrum-fusion-ns
Here,
replace <Digest> with the actual image digest value you got in step 9. Also, replace ibm-spectrum-fusion-ns with
your namespace.
The value of ocp412-t depends on your OpenShift Container
Platform version.

Example CR after edit:

spec:
  hasRelatedDefinition: false
  onboarding:
...
    serviceOperatorSubscription:
      catalogSourceName: isf-data-foundation-catalog
      createCatalogSource: true
      globalCatalogSource: true
      isClusterWide: false
      multiVersionCatSrcDetails:
        ocp49:
          skipCatSrcCreation: true
        ocp410:
          skipCatSrcCreation: true
        ocp411:
          skipCatSrcCreation: true
        ocp412-t:
          displayName: Data Foundation Catalog
          imageDigest: sha256:2d9e78d69a457b722cf6037968dae5f48eccd9e48ef4369a7fe661de0d96df95
          imageName: isf-data-foundation-catalog
          imageTag: v4.12
          publisher: IBM
          registryPath: icr.io/cpopen
          skipCatSrcCreation: false









