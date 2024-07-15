https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=registry-mirroring-storage-scale-images



Mirroring IBM Storage Scale images
Mirror the IBM Storage Scale images to
your enterprise registry.
About this task
For more reference information, see Offline setup for network restricted Red Hat OpenShift Container
Platform clusters in IBM Spectrum Scale Container Native 5.2.0.

Note:

This procedure is only necessary if you plan to enable the Global data
platform
IBM Storage Fusion service.
IBM Storage Fusion 2.8.0 or higher supports IBM Storage Scale 5.2.0. 




Procedure
Log in to the IBM Entitled Container Registry using the IBM entitlement key. 
docker login cp.icr.io -u cp -p <your entitlement key> 
Note: Ensure that your entitlement key for IBM Storage Fusion contains the correct entitlement.
Set the following environment variables:


export LOCAL_ISF_REGISTRY="<Your enterprise registry host>:<port>" 
export LOCAL_ISF_REPOSITORY="<Your image path>" 
export TARGET_PATH="$LOCAL_ISF_REGISTRY/$LOCAL_ISF_REPOSITORY" 
#verify target repository value echo "$TARGET_PATH"
Note: Port is a non-mandatory value when setting the LOCAL_ISF_REGISTRY variable.
You can ignore this if your enterprise registry is accessible and has a secure connection.
Sample value for without
port:export LOCAL_ISF_REGISTRY="registryhost.com"
See the following sample values:

export LOCAL_ISF_REGISTRY="registryhost.com:443"
export LOCAL_ISF_REPOSITORY="fusion-mirror"

LOCAL_ISF_REGISTRY is your entitlement registry with port, if you are not using
the default port 443.
LOCAL_ISF_REPOSITORY is the image path in which you want to mirror the images.
You can choose your own repository paths. For example, sds-2.8.0/isf or
sds-2.8.0.


Run the command to login to the Docker registry with your enterprise registry
credentials. 
docker login $LOCAL_ISF_REGISTRY -u <your enterprise registry username> -p <your enterprise registry password>


From the mirroring host, run the following copy command to copy IBM Storage Scale images to the host: 
Note: Make sure you are logged into the source and destination repositories via docker login
command.


skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/data-management/ibm-spectrum-scale-daemon@sha256:65a1b65e4076ac7be840904a6a1d59eb74849cda58a1a4a59b2f9a8de94652de docker://$TARGET_PATH/data-management/ibm-spectrum-scale-daemon@sha256:65a1b65e4076ac7be840904a6a1d59eb74849cda58a1a4a59b2f9a8de94652de
skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/ibm-spectrum-scale-core-init@sha256:089718b2d96d909b86bf19448c4d86f31a3877eb450d465d830e55133415015d docker://$TARGET_PATH/ibm-spectrum-scale-core-init@sha256:089718b2d96d909b86bf19448c4d86f31a3877eb450d465d830e55133415015d
skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/ibm-spectrum-scale-gui@sha256:93288c812f0bace075eb785f519d6d7f684bdb33407c44a93b53df9abdd16e0a docker://$TARGET_PATH/ibm-spectrum-scale-gui@sha256:93288c812f0bace075eb785f519d6d7f684bdb33407c44a93b53df9abdd16e0a
skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/postgres@sha256:bbd7346fab25b7e0b25f214829d6ebfb78ef0465059492e46dee740ce8fcd844 docker://$TARGET_PATH/postgres@sha256:bbd7346fab25b7e0b25f214829d6ebfb78ef0465059492e46dee740ce8fcd844
skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/ubi-minimal@sha256:bc552efb4966aaa44b02532be3168ac1ff18e2af299d0fe89502a1d9fabafbc5 docker://$TARGET_PATH/ubi-minimal@sha256:bc552efb4966aaa44b02532be3168ac1ff18e2af299d0fe89502a1d9fabafbc5
skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/ibm-spectrum-scale-pmcollector@sha256:07a9e951ab315724ca39e332a7559ca98519442b0669241fd97ffdb3a0381667 docker://$TARGET_PATH/ibm-spectrum-scale-pmcollector@sha256:07a9e951ab315724ca39e332a7559ca98519442b0669241fd97ffdb3a0381667
skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/ibm-spectrum-scale-monitor@sha256:3f41d20e7beaf757778d8650172adf8456569607dab3479eb4524407ed2e4a13 docker://$TARGET_PATH/ibm-spectrum-scale-monitor@sha256:3f41d20e7beaf757778d8650172adf8456569607dab3479eb4524407ed2e4a13
skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/ibm-spectrum-scale-grafana-bridge@sha256:a6ca689d8205f17bb278910c521842f98ced8537aba55b287792a91269bf2f41 docker://$TARGET_PATH/ibm-spectrum-scale-grafana-bridge@sha256:a6ca689d8205f17bb278910c521842f98ced8537aba55b287792a91269bf2f41
skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/ibm-spectrum-scale-coredns@sha256:88cbfe40fd302a6467cb7e852b298f6c8d8659782ab313706d491d3ddf172a6e docker://$TARGET_PATH/ibm-spectrum-scale-coredns@sha256:88cbfe40fd302a6467cb7e852b298f6c8d8659782ab313706d491d3ddf172a6e
skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/csi/csi-snapshotter@sha256:1a29ab1e4ecdc33a84062cec757620d9787c28b28793202c5b78ae097c3dee27 docker://$TARGET_PATH/csi/csi-snapshotter@sha256:1a29ab1e4ecdc33a84062cec757620d9787c28b28793202c5b78ae097c3dee27
skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/csi/csi-attacher@sha256:d69cc72025f7c40dae112ff989e920a3331583497c8dfb1600c5ae0e37184a29 docker://$TARGET_PATH/csi/csi-attacher@sha256:d69cc72025f7c40dae112ff989e920a3331583497c8dfb1600c5ae0e37184a29
skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/csi/csi-provisioner@sha256:de79c8bbc271622eb94d2ee8689f189ea7c1cb6adac260a421980fe5eed66708 docker://$TARGET_PATH/csi/csi-provisioner@sha256:de79c8bbc271622eb94d2ee8689f189ea7c1cb6adac260a421980fe5eed66708
skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/csi/livenessprobe@sha256:5baeb4a6d7d517434292758928bb33efc6397368cbb48c8a4cf29496abf4e987 docker://$TARGET_PATH/csi/livenessprobe@sha256:5baeb4a6d7d517434292758928bb33efc6397368cbb48c8a4cf29496abf4e987
skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/csi/csi-node-driver-registrar@sha256:c53535af8a7f7e3164609838c4b191b42b2d81238d75c1b2a2b582ada62a9780 docker://$TARGET_PATH/csi/csi-node-driver-registrar@sha256:c53535af8a7f7e3164609838c4b191b42b2d81238d75c1b2a2b582ada62a9780
skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/csi/csi-resizer@sha256:4c148bbdf883153bc72d321be4dc55c33774a6d98b2b3e0c2da6ae389149a9b7 docker://$TARGET_PATH/csi/csi-resizer@sha256:4c148bbdf883153bc72d321be4dc55c33774a6d98b2b3e0c2da6ae389149a9b7
skopeo copy --all --preserve-digests docker://cp.icr.io/cp/spectrum/scale/csi/ibm-spectrum-scale-csi-driver@sha256:b2bc343eadbc11d9ed74a8477d2cd0a7a8460a72203d3f6236d4662e68df1166 docker://$TARGET_PATH/csi/ibm-spectrum-scale-csi-driver@sha256:b2bc343eadbc11d9ed74a8477d2cd0a7a8460a72203d3f6236d4662e68df1166
skopeo copy --all --preserve-digests docker://icr.io/cpopen/ibm-spectrum-scale-operator@sha256:d44f11cc61f410dd20d7bb52ac28eebc80f928eede9be434c270a7ad5648b626 docker://$TARGET_PATH/ibm-spectrum-scale-operator@sha256:d44f11cc61f410dd20d7bb52ac28eebc80f928eede9be434c270a7ad5648b626
skopeo copy --all --preserve-digests docker://icr.io/cpopen/ibm-spectrum-scale-csi-operator@sha256:bd264199ac10d574163bfa32bb88844fd786ee6f794a56e235591d2f051c7807 docker://$TARGET_PATH/ibm-spectrum-scale-csi-operator@sha256:bd264199ac10d574163bfa32bb88844fd786ee6f794a56e235591d2f051c7807
skopeo copy --all --preserve-digests docker://icr.io/cpopen/ibm-spectrum-scale-must-gather@sha256:eab5b2e72579b96f2cfc04162e4dd6ace7eb3570f2f08dca552c045ea29faa3d docker://$TARGET_PATH/ibm-spectrum-scale-must-gather@sha256:eab5b2e72579b96f2cfc04162e4dd6ace7eb3570f2f08dca552c045ea29faa3d

In the OpenShift® Container Platform cluster, add
ImageContentSourcePolicy: 
Note:

The ImageContentSourcePolicy contains list of repositories, copy digests for
the IBM Storage Scale.
Replace the variable $TARGET_PATH with your registry details where images are
mirrored.


See the following
ImageContentSourcePolicy.apiVersion: operator.openshift.io/v1alpha1
kind: ImageContentSourcePolicy
metadata:
  name: isf-scale-icsp
spec:
  repositoryDigestMirrors: 
  # for scale
  - mirrors:
    - $TARGET_PATH
    source: cp.icr.io/cp/spectrum/scale
  - mirrors:
    - $TARGET_PATH
    source: icr.io/cpopen
Do not add white spaces while you update the mirror path in ImageContentSourcePolicies.
If you want to do so, add values within double quotation marks. For example, if the new path where
the images are mirrored is registryhost.com:443/isf-new-path, then encapsulate
within double quotation marks ("") while you edit to avoid white spaces in the
line.
- mirrors:
    - "registryhost.com:443/isf-new-path"
    - registryhost.com:443/old-path
    source: cp.icr.io/cp/spectrum/scale







