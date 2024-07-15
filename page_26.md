https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=registry-mirroring-data-cataloging-images



Mirroring Data Cataloging images
Mirror the Data Cataloging images to your
enterprise registry.
Before you begin

Make sure that you install the oc-mirror OpenShift CLI plug-in. For more
information about oc-mirror OpenShift CLI plug-in installation, see Installing the oc-mirror OpenShift CLI plugin.
Make sure that you use OpenShift® Container Platform version 4.12
or higher in the commands. Use your specific version number in the commands.
Make sure OpenShift Container Platform version is at least
4.12.
Install either docker or podman to run login commands.


About this task
For more information about Air gap setup for network restricted Red Hat®
OpenShift Container Platform clusters, see Offline setup for network restricted Red Hat OpenShift Container
Platform clusters.Note:

This procedure is only necessary if you plan to enable the Data Cataloging
IBM Storage Fusion HCI System service.
The destination registry where all Data Cataloging
images are going to be copied need to support both OCI
(application/vnd.oci.image.manifest.v1+json) and Docker V2
(application/vnd.docker.distribution.manifest.v2+json) manifest types.




ProcedureEnsure that the amq-streams operator package is
present in your cluster. 
Note: If you have not mirrored amq-streams from the Red Hat packages previously, then follow the steps
that are provided in the Mirroring Red Hat operator images to enterprise registry.

Note:

Run the following command to get list of mirrored Red
Hat packages available on your
cluster.oc get packagemanifests | grep -i "Red Hat Operators"
If you do not get redhat-oadp-operator operator package from the previous step,
then you must follow the step 1. 
Ensure that you also add existing packages along with new one in
ImageSetConfiguration file. Otherwise, old packages can be lost from the
Red Hat operator index image.



Run the following command to login the Red Hat enterprise registry and the IBM Entitled
Container Registry using your credentials. 
Note: Make sure that your entitlement key for IBM Storage Fusion contains the correct entitlement.
For docker
users:docker login registry.redhat.io -u <Red Hat enterprise registry username> -p <Red Hat enterprise registry password>

docker login cp.icr.io -u cp -p <your entitlement key>
For podman
users:podman login registry.redhat.io -u <Red Hat enterprise registry username> -p <Red Hat enterprise registry password>

podman login cp.icr.io -u cp -p <Your entitlement key>

Set the following environment variable. 
export LOCAL_ISF_REGISTRY="<Your enterprise registry host>"
LOCAL_ISF_REGISTRY is your enterprise registry. Examples based on IBM Registry:
cp.icr.io, cp.icr.io:443 and cp.icr.io/my/custom/path.

Run the command to login to the Docker registry with your enterprise registry
credentials. 
For docker
users:docker login $LOCAL_ISF_REGISTRY -u <your enterprise registry username> -p <your enterprise registry password>
For podman
users:podman login $LOCAL_ISF_REGISTRY -u <your enterprise registry username> -p <your enterprise registry password>

Create the image set configuration for Data Cataloging. 
cat << EOF > imagesetconfiguration_dcs.yaml
kind: ImageSetConfiguration
apiVersion: mirror.openshift.io/v1alpha2
storageConfig:
  registry:
    imageURL: "${LOCAL_ISF_REGISTRY}/isf-dcs-metadata:latest"
    skipTLS: true
mirror:
  operators:
    - catalog: "oci:///tmp/dcs_catalog"
      packages:
        - name: "ibm-spectrum-discover-operator"
    - catalog: icr.io/cpopen/ibm-operator-catalog:latest
      packages:
        - name: "db2u-operator"
          channels:
            - name: "v110509.0"
  additionalImages:
    - name: icr.io/db2u/db2u@sha256:793e05f77076e8e1e055c738e90c9706d582c7da286e908955504842f844ce06
    - name: icr.io/db2u/db2u.restricted@sha256:afd250032aef39549f43d992a487a9d7b004f074e2cce3d8aadf6a8f327cecfb
    - name: icr.io/db2u/db2u.db2wh@sha256:0886ee44e500e571ffcb47a82701b616da94feb9ff9eb2c0582a0852c30194fa
    - name: icr.io/db2u/db2u.dv.api@sha256:621f1226c0041ec8961a219e804abb6b45a0b9332a9dc2dcdb216549035ee9b5
    - name: icr.io/db2u/db2u.dv.caching@sha256:86be7fd023978bfaa922da408d457d864a0ad353d18cd07770f28a5b924fe41b
    - name: icr.io/db2u/db2u.dv.utils@sha256:79258a4b20e4063109e943c7f0aedb513bb837ddcd7dfb2ce72e9d1d598b2bb9
    - name: icr.io/db2u/etcd@sha256:d1dd2eae940427ff7bcd40506cc2181f3fc7826d48dbbb3a4bc3349a2d8c2f93
    - name: icr.io/db2u/db2u.logstreaming.fluentd@sha256:55fbd2c1938cb0f735e32a8385748b702c38c3e41c83cb44e8b3d5e41b685269
    - name: icr.io/db2u/db2u.hurricane@sha256:c28133ed6c25c163b5c63957773f7ff3375874f7a40bec9d3579bfc1349a78eb
    - name: icr.io/db2u/db2u.instdb@sha256:cf2f99358fb6beac6ca2f9553855b8f33d4cfcd7748bd191c66b725180722cab
    - name: icr.io/db2u/db2u.instdb.restricted@sha256:a78c2c6f7b43e857554e1eed21a9d1fd41202559cb9e4231d975c48c0eb7075b
    - name: icr.io/db2u/db2u.auxiliary.auth@sha256:90d80d10fa6573ea466512a3fc88c9f80ccb67f4d188206fa515b15993c56a96
    - name: icr.io/db2u/db2u.mustgather@sha256:a8a5f6ab563a7fbd93f22ee2eda3a2250c297c67011a1aadb46d6c68482535a3
    - name: icr.io/db2u/db2u.qrep@sha256:c1121abab93abee6cf1d27019a2ba4ac2b8f7ade980207713054b184812d6d65
    - name: icr.io/db2u/db2u.rest@sha256:7cda76f07c2d6ced608befb3a4cf6f88c3318bb3a54d02e6b3c6c03f8abf92d2
    - name: icr.io/db2u/db2u.update.image@sha256:68cac0eb685747dbad88cb160ea859298bd3a86c3d31a2ddd6b2da28180e56fc
    - name: icr.io/db2u/db2u.tools@sha256:290532cb23d45a246dad7bca1aa761407480a3423f645800f5aa6ca1dedd863d
    - name: icr.io/db2u/db2u.veleroplugin@sha256:01369d5f1da84f5ceb170c9bb9287e4fdac1dd39f30515b6a13ae37c1f38c559
    - name: icr.io/db2u/db2u.watsonquery@sha256:e1c9542fd5a6ea90b7a265d823e348aaba669545f817f47ce7076dc5753963fe
EOF

Prepare the Data Cataloging catalog image and
registries configuration. 
skopeo --override-os=linux copy docker://icr.io/cpopen/ibm-spectrum-discover-operator-catalog@sha256:c2538264cb1882b1c98fea5ef162f198ce38ed8c940e82e3b9db458a9a46cb15 oci:///tmp/dcs_catalog --format v2s2
skopeo --override-os=linux copy --all docker://icr.io/cpopen/ibm-spectrum-discover-operator-catalog@sha256:c2538264cb1882b1c98fea5ef162f198ce38ed8c940e82e3b9db458a9a46cb15 docker://${LOCAL_ISF_REGISTRY}/cpopen/ibm-spectrum-discover-operator-catalog@sha256:c2538264cb1882b1c98fea5ef162f198ce38ed8c940e82e3b9db458a9a46cb15


cat << EOF > registries_dcs.conf
[[registry]]
  location = "icr.io/cp/ibm-spectrum-discover"
  insecure = false
  blocked = false
  mirror-by-digest-only = true
  prefix = ""

  [[registry.mirror]]
    location = "cp.icr.io/cp/ibm-spectrum-discover"
    insecure = false
EOF

Mirror the images using the image set configuration. 
oc mirror --config imagesetconfiguration_dcs.yaml docker://${LOCAL_ISF_REGISTRY} --dest-skip-tls --ignore-history --oci-registries-config registries_dcs.conf

Create an ImageContentSourcePolicy for IBM Storage Fusion
Data Cataloging. 
cat << EOF > imagecontentsourcepolicy_dcs.yaml
apiVersion: operator.openshift.io/v1alpha1
kind: ImageContentSourcePolicy
metadata:
  name: isf-dcs-icsp
spec:
  repositoryDigestMirrors:
    - mirrors:
        - $LOCAL_ISF_REGISTRY/cpopen
      source: icr.io/cpopen
    - mirrors:
        - $LOCAL_ISF_REGISTRY/redhat
      source: registry.redhat.io/redhat
    - mirrors:
        - $LOCAL_ISF_REGISTRY/ubi8
      source: registry.redhat.io/ubi8
    - mirrors:
        - $LOCAL_ISF_REGISTRY/amq-streams
      source: registry.redhat.io/amq-streams
    - mirrors:
        - $LOCAL_ISF_REGISTRY/openshift4
      source: registry.redhat.io/openshift4
    - mirrors:
        - $LOCAL_ISF_REGISTRY/cp/ibm-spectrum-discover
      source: cp.icr.io/cp/ibm-spectrum-discover
    - mirrors:
        - $LOCAL_ISF_REGISTRY/db2u
      source: icr.io/db2u
EOF
oc apply -f imagecontentsourcepolicy_dcs.yaml

Create the IBM Storage Fusion operators and Red Hat operators catalogs. 
for catalog in $(ls oc-mirror-workspace/results-*/catalogSource* | grep -v spectrum-discover); do echo "Creating CatalogSource from file: $catalog"; echo "oc apply -f $catalog"; done








