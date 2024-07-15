https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=registry-mirroring-storage-fusion-images



Mirroring IBM Storage Fusion images
Mirror the IBM Storage Fusion images to your
enterprise registry.
About this taskIf you do not have Docker, you can use Podman. 
ProcedureRun the following command to login to Docker registry with your Red Hat® enterprise credentials:
docker login registry.redhat.io -u <Red Hat enterprise registry username> -p <Red Hat enterprise registry password>
Log in to the IBM Entitled Container Registry using the IBM entitlement key:
docker login cp.icr.io -u cp -p <your entitlement key>Note: Ensure that your entitlement key for IBM Storage Fusion contains the correct
entitlement.
Set the following environment variables:


export LOCAL_ISF_REGISTRY="<Your enterprise registry host>:<port>"
export LOCAL_ISF_REPOSITORY="<Your image path>"
IFS='/' read -r NAMESPACE PREFIX <<< "$LOCAL_ISF_REPOSITORY"
if [[ "$PREFIX" != "" ]]; then export TARGET_PATH="$LOCAL_ISF_REGISTRY/$NAMESPACE/$PREFIX";  export REPO_PREFIX=$(echo "$PREFIX"| sed -r 's/\//-/g')-; else export TARGET_PATH="$LOCAL_ISF_REGISTRY/$NAMESPACE"; export REPO_PREFIX=""; fi
#verify both variables set correctly
echo "$TARGET_PATH"
echo "$REPO_PREFIX"

Note: Port is a non-mandatory value when setting the LOCAL_ISF_REGISTRY variable.
You can ignore this if your enterprise registry is accessible and has a secure connection.
Sample value for without
port:export LOCAL_ISF_REGISTRY="registryhost.com"
See the following sample values:

export LOCAL_ISF_REGISTRY="registryhost.com:443"
export LOCAL_ISF_REPOSITORY="fusion-mirror"

LOCAL_ISF_REGISTRY is your entitlement registry.
LOCAL_ISF_REPOSITORY is the image path in which you want to mirror the images.
You can choose your own repository paths. For example, sds-2.8.0/isf or
sds-2.8.0.


Run the command to login to the Docker registry with your enterprise registry
credentials. 
docker login $LOCAL_ISF_REGISTRY -u <your enterprise registry username> -p <your enterprise registry password>


From the mirroring host, run the following copy command to copy IBM Storage Fusion images to the host: 
Note:

Make sure that you are logged in to the source and destination repositories by using the docker
login command.
If you mirror to a Quay registry, use a destination tag name (<image-name>:xxxxxx) rather
than the digest name to prevent Red Hat Quay from
deleting your downloaded
images.skopeo copy --all docker://cp.icr.io/cp/isf-sds/<image-name>@sha256:xxxxx docker://$TARGET_PATH/<image-name>:xxxxx
Example skopeo command: 
skopeo copy --all docker://cp.icr.io/cp/isf-sds/fusion-ui@sha256:705b20557b63315e6ddc403808aa57ee9cf0a621d531ddf2f3f196b63ca11acb docker://$TARGET_PATH/fusion-ui:705b20557b63315e6ddc403808aa57ee9cf0a621d531ddf2f3f196b63ca11acbFor
more information about Red Hat Quay garbage collection, see https://access.redhat.com/documentation/en-us/red_hat_quay/3.10/html/manage_red_hat_quay/garbage-collection. 



skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/isf-sds/callhomeclient@sha256:964e5d16b2a570d15a54effbb73f653298012fbe53a8532f83a228a3af68a8e7 docker://$TARGET_PATH/callhomeclient@sha256:964e5d16b2a570d15a54effbb73f653298012fbe53a8532f83a228a3af68a8e7
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/isf-sds/eventmanager@sha256:1586572bae1ffc44cd5bc7e68f3f37cd8d5c3e2c788b6d3d23f14c2e5854d448 docker://$TARGET_PATH/eventmanager@sha256:1586572bae1ffc44cd5bc7e68f3f37cd8d5c3e2c788b6d3d23f14c2e5854d448
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/isf-sds/eventmanager-snmp3@sha256:f379b7dffcee22ce51a34464455309dc803786d523cb6b8c40a2bddf73341f95 docker://$TARGET_PATH/eventmanager-snmp3@sha256:f379b7dffcee22ce51a34464455309dc803786d523cb6b8c40a2bddf73341f95
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/isf-sds/fusion-ui@sha256:705b20557b63315e6ddc403808aa57ee9cf0a621d531ddf2f3f196b63ca11acb docker://$TARGET_PATH/fusion-ui@sha256:705b20557b63315e6ddc403808aa57ee9cf0a621d531ddf2f3f196b63ca11acb
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/isf-sds/isf-application-operator@sha256:8b654f88051f81746d3cb0a350c38f30df5da3151a4b8846655ca4fdc6238788 docker://$TARGET_PATH/isf-application-operator@sha256:8b654f88051f81746d3cb0a350c38f30df5da3151a4b8846655ca4fdc6238788
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/isf-sds/isf-cns-operator@sha256:13217921c6c64607ad0cd3cbc14fd156af3ec5f439b96ec9f81670dcd574a53e docker://$TARGET_PATH/isf-cns-operator@sha256:13217921c6c64607ad0cd3cbc14fd156af3ec5f439b96ec9f81670dcd574a53e
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/isf-sds/isf-data-protection-operator@sha256:204a23a5836d1274481576b46681bd80ae06240ace2740036010f6448650fe11 docker://$TARGET_PATH/isf-data-protection-operator@sha256:204a23a5836d1274481576b46681bd80ae06240ace2740036010f6448650fe11
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/isf-sds/isf-management-consoleplugin@sha256:ddbab64895bea43b0fa1fc3cbb39d3ac2a12f23b041db70793696d3822bb3153 docker://$TARGET_PATH/isf-management-consoleplugin@sha256:ddbab64895bea43b0fa1fc3cbb39d3ac2a12f23b041db70793696d3822bb3153
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/isf-sds/isf-prereq-operator@sha256:05b169dcf76ad9a7b34eb85abf441c0836318cec14072a86a5f4a00e01803a86 docker://$TARGET_PATH/isf-prereq-operator@sha256:05b169dcf76ad9a7b34eb85abf441c0836318cec14072a86a5f4a00e01803a86
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/isf-sds/isf-proxy@sha256:e7ace0060bd473743e70cdfe1c469394600c2b6642bd9a23e8858d3bea53da35 docker://$TARGET_PATH/isf-proxy@sha256:e7ace0060bd473743e70cdfe1c469394600c2b6642bd9a23e8858d3bea53da35
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/isf-sds/isf-serviceability-operator@sha256:f8f4460b9de8f754ff1f58c027596e8dee0a621d008b1bb52746263be127863a docker://$TARGET_PATH/isf-serviceability-operator@sha256:f8f4460b9de8f754ff1f58c027596e8dee0a621d008b1bb52746263be127863a
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/isf-sds/isf-ui-operator@sha256:a40346c44a49e7990e75fab813f2ef209272043a57c7a6499d8ce0d805bc9cde docker://$TARGET_PATH/isf-ui-operator@sha256:a40346c44a49e7990e75fab813f2ef209272043a57c7a6499d8ce0d805bc9cde
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/isf-sds/isf-update-operator@sha256:9fc4fc0dc5545e9d2dd04f96b0760025909520a01c0549d229b7a5abccc493a8 docker://$TARGET_PATH/isf-update-operator@sha256:9fc4fc0dc5545e9d2dd04f96b0760025909520a01c0549d229b7a5abccc493a8
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/isf-sds/logcollector@sha256:9238c5cfe576e0511849dbd3bf75f39f11fbc71310ee4db49d783717190243f2 docker://$TARGET_PATH/logcollector@sha256:9238c5cfe576e0511849dbd3bf75f39f11fbc71310ee4db49d783717190243f2
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/isf-operator-software-bundle@sha256:b79a0d3ee86abb12636b6cdc02486da3fef09584b7c953be7ee765bfaf516c21 docker://$TARGET_PATH/isf-operator-software-bundle@sha256:b79a0d3ee86abb12636b6cdc02486da3fef09584b7c953be7ee765bfaf516c21
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/isf-operator-software-catalog:2.8.0 docker://$TARGET_PATH/isf-operator-software-catalog:2.8.0
skopeo copy --insecure-policy --preserve-digests --all docker://registry.redhat.io/openshift4/ose-kube-rbac-proxy@sha256:767682dd3bd65651a8204c9fb732b9c48b99127189992b43abc6ecce027f4589 docker://$TARGET_PATH/openshift4/ose-kube-rbac-proxy@sha256:767682dd3bd65651a8204c9fb732b9c48b99127189992b43abc6ecce027f4589


Note: Ensure all the copy commands complete successfully without errors. For example, if you have
the correct entitlement key but still observe the following error for any or all of the copy
commands, then contact IBM
support:denied: insufficient scope


Add ImageContentSourcePolicy. 
Note:

The ImageContentSourcePolicy contains list of repositories, copy digests for
the IBM Storage Fusion.
Replace the variable $TARGET_PATH with your registry details where images are
mirrored.


See the following ImageContentSourcePolicy:
apiVersion: operator.openshift.io/v1alpha1 
kind: ImageContentSourcePolicy 
metadata: 
  name: isf-fusion-icsp 
spec: 
  repositoryDigestMirrors:  
  - mirrors:
    - $TARGET_PATH 
    source: cp.icr.io/cp/isf-sds 
  - mirrors:
    - $TARGET_PATH 
    source: icr.io/cpopen 
  - mirrors: 
    - $TARGET_PATH/openshift4 
    source: registry.redhat.io/openshift4 









