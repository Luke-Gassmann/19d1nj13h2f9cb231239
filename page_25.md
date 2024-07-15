https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=registry-mirroring-backup-restore-images



Mirroring Backup & Restore images
Mirror the Backup & Restore images to your
enterprise registry.
About this task
For more information about Air gap setup for network restricted Red Hat®
OpenShift® Container Platform clusters, see Offline setup for network restricted Red Hat OpenShift Container
Platform clusters.Note: This procedure is only necessary if you plan to enable the Backup & Restore
IBM Storage Fusion service.


Procedure
Run the following command to login to the Docker registry with your Red Hat enterprise credentials:
docker login registry.redhat.io -u <Red Hat enterprise registry username> -p <Red Hat enterprise registry password>Run
the following command to login to Red Hat quay.iowith with your Red Hat enterprise
credentials:docker login quay.io -u <Red Hat enterprise registry username> -p <Red Hat enterprise registry password>Log
in to the IBM Entitled Container Registry using the IBM entitlement key:
docker login cp.icr.io -u cp -p <your entitlement key>Note: Ensure that your entitlement key for IBM Storage Fusion contains the correct
entitlement.
Set the following environment variables: 


export LOCAL_ISF_REGISTRY="<Your enterprise registry host>:<port>" 
export LOCAL_ISF_REPOSITORY="<Your image path>" 
export TARGET_PATH="$LOCAL_ISF_REGISTRY/$LOCAL_ISF_REPOSITORY" 
echo "$TARGET_PATH" 
Note: Port is a non-mandatory value when setting the LOCAL_ISF_REGISTRY variable.
You can ignore this if your enterprise registry is accessible and has a secure connection.
Sample value for without
port:export LOCAL_ISF_REGISTRY="registryhost.com"
See the following sample values:


export LOCAL_ISF_REGISTRY="registryhost.com:443"
export LOCAL_ISF_REPOSITORY="fusion-mirror"

LOCAL_ISF_REGISTRY is your entitlement registry.
LOCAL_ISF_REPOSITORY is the image path in which you want to mirror the images.
You can choose your own repository paths. For example, sds-2.8.0/isf or sds-2.8.0.


Run the command to login to the Docker registry with your enterprise registry
credentials. 
docker login $LOCAL_ISF_REGISTRY -u <your enterprise registry username> -p <your enterprise registry password>


Ensure that the redhat-oadp-operator and
amq-streams operator packages are present in your cluster. 
Note: If you have not mirrored redhat-oadp-operator and
amq-streams from the Red Hat
packages previously, then follow the steps that are provided in the Mirroring Red Hat operator images to enterprise registry.


Note:

Run the following command to get list of mirrored Red
Hat packages available on your
cluster.oc get packagemanifests | grep -i "Red Hat Operators"
If you do not get redhat-oadp-operator and amq-streams
operator packages from the previous step, then you must follow the step 3. 
Ensure that you also add existing packages along with new one in
ImageSetConfiguration file. Otherwise, old packages can be lost from the
Red Hat operator index image.



From the mirroring host, run the following commands to copy the Backup & Restore images to the artifactory and Quay
registry: 
Artifactory:
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/fbr/guardian-application-service@sha256:4af659712ed613d110383f4ac43a102ba887795763f312a8bf8db835653b5cf9 docker://$TARGET_PATH/guardian-application-service@sha256:4af659712ed613d110383f4ac43a102ba887795763f312a8bf8db835653b5cf9
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/fbr/guardian-backup-location@sha256:62658a1735311606d584857f902f2c4a423f1c3e85b2ea289ae54727193cd825 docker://$TARGET_PATH/guardian-backup-location@sha256:62658a1735311606d584857f902f2c4a423f1c3e85b2ea289ae54727193cd825
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/fbr/guardian-backup-policy@sha256:89e21c7425ea72aef2f3f8e53c36a74d8becb561d3b1e3476b75e22004dd6d49 docker://$TARGET_PATH/guardian-backup-policy@sha256:89e21c7425ea72aef2f3f8e53c36a74d8becb561d3b1e3476b75e22004dd6d49
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/fbr/guardian-backup-service@sha256:56e4119fc3ca89fe8a1c2babffaaabf3d91aeecc8076023347a5381c607d4ae3 docker://$TARGET_PATH/guardian-backup-service@sha256:56e4119fc3ca89fe8a1c2babffaaabf3d91aeecc8076023347a5381c607d4ae3
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/fbr/guardian-job-manager@sha256:d5eb66db95e62170874e2d0f3ec5e097819596768f90f650013a2456a0fc83b7 docker://$TARGET_PATH/guardian-job-manager@sha256:d5eb66db95e62170874e2d0f3ec5e097819596768f90f650013a2456a0fc83b7
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/fbr/guardian-transaction-manager@sha256:f09efb569de67917d41a6b3f374dcee4703f859787513ca452a2c5ad965d3f58 docker://$TARGET_PATH/guardian-transaction-manager@sha256:f09efb569de67917d41a6b3f374dcee4703f859787513ca452a2c5ad965d3f58
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/fbr/guardian-kubevirt-velero-plugin@sha256:9f6d83593f5053c1ece1619243c88ff7fa4a5e3a6a1f9b4df944b45d73211f3e docker://$TARGET_PATH/guardian-kubevirt-velero-plugin@sha256:9f6d83593f5053c1ece1619243c88ff7fa4a5e3a6a1f9b4df944b45d73211f3e
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-datamover@sha256:76c3f168faec35d1cf7c56010646b731123ba123abb1a60427409edd13ec6b70 docker://$TARGET_PATH/guardian-datamover@sha256:76c3f168faec35d1cf7c56010646b731123ba123abb1a60427409edd13ec6b70
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-dm-operator@sha256:35562a8b290b600c626d81b1e573931d33f2e15e2b0a9d46cd3fb59e23ce0ae8 docker://$TARGET_PATH/guardian-dm-operator@sha256:35562a8b290b600c626d81b1e573931d33f2e15e2b0a9d46cd3fb59e23ce0ae8
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-dp-operator@sha256:faec1b7a85aaab714716a850ac4109d6b0079e6214f3e06b1d8a91cd5b73fa5f docker://$TARGET_PATH/guardian-dp-operator@sha256:faec1b7a85aaab714716a850ac4109d6b0079e6214f3e06b1d8a91cd5b73fa5f
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/idp-agent-operator@sha256:3a927d363fccfca3ca75023d2c94ed923e6e86828a7d086d790e999b0f0e1ff1 docker://$TARGET_PATH/idp-agent-operator@sha256:3a927d363fccfca3ca75023d2c94ed923e6e86828a7d086d790e999b0f0e1ff1
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/idp-server-operator@sha256:50f119e4ae22cc21a4b9b7fe5d3b1da4b8352c2d4635b58bbe5956ae62b36d22 docker://$TARGET_PATH/idp-server-operator@sha256:50f119e4ae22cc21a4b9b7fe5d3b1da4b8352c2d4635b58bbe5956ae62b36d22
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/idp-server-operator-bundle@sha256:aadfc6b18c33ed632f660ec5df9e1bf7ed866359737f61ffe27bc308e9816567 docker://$TARGET_PATH/idp-server-operator-bundle@sha256:aadfc6b18c33ed632f660ec5df9e1bf7ed866359737f61ffe27bc308e9816567
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/idp-server-operator-catalog@sha256:5462246b796dd0c6e729c8802491b7cd5bb59cb98476ab118bee6a1f520c5c2d docker://$TARGET_PATH/idp-server-operator-catalog@sha256:5462246b796dd0c6e729c8802491b7cd5bb59cb98476ab118bee6a1f520c5c2d
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-mongo-operator@sha256:006765a2a3a5451b8eebdc8e0ec10a4384124e99f7099f281ab9f04b13d9e357 docker://$TARGET_PATH/guardian-mongo-operator@sha256:006765a2a3a5451b8eebdc8e0ec10a4384124e99f7099f281ab9f04b13d9e357
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-redis-operator@sha256:cb698d0f89bf3c04191dd1902dc1e29269544e7720987aa557fb6b6130d11e0e docker://$TARGET_PATH/guardian-redis-operator@sha256:cb698d0f89bf3c04191dd1902dc1e29269544e7720987aa557fb6b6130d11e0e
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-dm-operator-bundle@sha256:938433010f4ed3b71e7eaba41020c5114604ce0d77300aa3efbf2c5fe5465095 docker://$TARGET_PATH/guardian-dm-operator-bundle@sha256:938433010f4ed3b71e7eaba41020c5114604ce0d77300aa3efbf2c5fe5465095
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-dp-operator-bundle@sha256:a8fbec8721edb951d02566369df74eea161ad859b3e28d9e44ce7b642fb104d1 docker://$TARGET_PATH/guardian-dp-operator-bundle@sha256:a8fbec8721edb951d02566369df74eea161ad859b3e28d9e44ce7b642fb104d1
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/idp-agent-operator-bundle@sha256:a4528ccd64f63e64326dd519fbec19625933f61e150ad3a6f7ba9bcd5a9dcbe2 docker://$TARGET_PATH/idp-agent-operator-bundle@sha256:a4528ccd64f63e64326dd519fbec19625933f61e150ad3a6f7ba9bcd5a9dcbe2
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-mongo-operator-bundle@sha256:79a86e9c1160463045fe03f54d8f87b0f7b6e6293a2900d437e8138ab1ff7481 docker://$TARGET_PATH/guardian-mongo-operator-bundle@sha256:79a86e9c1160463045fe03f54d8f87b0f7b6e6293a2900d437e8138ab1ff7481
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-redis-operator-bundle@sha256:ec8bd43483d77e6b0b41daf777d8dbbd83e54fee233e3a7faa714cbf6da1b3f6 docker://$TARGET_PATH/guardian-redis-operator-bundle@sha256:ec8bd43483d77e6b0b41daf777d8dbbd83e54fee233e3a7faa714cbf6da1b3f6
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/fbr-mongo-exporter@sha256:21aeeb051009d7784be0e0a8e86440dca26ac2ef57ffc461611de0414f1bb676 docker://$TARGET_PATH/fbr-mongo-exporter@sha256:21aeeb051009d7784be0e0a8e86440dca26ac2ef57ffc461611de0414f1bb676
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/fbr-mongo@sha256:73a3b08cd819a2175ae3308dcb72fa07518d0417071f79196338f636219127f4 docker://$TARGET_PATH/fbr-mongo@sha256:73a3b08cd819a2175ae3308dcb72fa07518d0417071f79196338f636219127f4
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/fbr-redis@sha256:2131345868484fe9540746c9e4a4a2a9b71dbbb80de5916d74604f2bfc4ec0f5 docker://$TARGET_PATH/fbr-redis@sha256:2131345868484fe9540746c9e4a4a2a9b71dbbb80de5916d74604f2bfc4ec0f5
skopeo copy --insecure-policy --preserve-digests --all docker://quay.io/openshift-release-dev/ocp-v4.0-art-dev@sha256:a731786db7f7bc7a4137309a16a7d27acbb9fd21c5731602e2ccaadc58155805 docker://$TARGET_PATH/ocp-v4.0-art-dev@sha256:a731786db7f7bc7a4137309a16a7d27acbb9fd21c5731602e2ccaadc58155805
skopeo copy --insecure-policy --preserve-digests --all docker://quay.io/openshift-release-dev/ocp-v4.0-art-dev@sha256:bf7bbc0987b7514ab15f3e20f1b432ee19d09f83c8072900b8718e158f78a5f6 docker://$TARGET_PATH/ocp-v4.0-art-dev@sha256:bf7bbc0987b7514ab15f3e20f1b432ee19d09f83c8072900b8718e158f78a5f6
skopeo copy --insecure-policy --preserve-digests --all docker://quay.io/minio/minio@sha256:a9cec9ed5bda5b4e1b2153823e01b309965b9de7ed6eb7f098d45592eecdfc78 docker://$TARGET_PATH/minio@sha256:a9cec9ed5bda5b4e1b2153823e01b309965b9de7ed6eb7f098d45592eecdfc78
skopeo copy --insecure-policy --preserve-digests --all docker://registry.redhat.io/rhel9/redis-7@sha256:33d868f8832be3dbe73adaf77e394646c8eda91af9bfb79d5e800c755925878c docker://$TARGET_PATH/rhel9/redis-7@sha256:33d868f8832be3dbe73adaf77e394646c8eda91af9bfb79d5e800c755925878c
Quay registry:
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/fbr/guardian-application-service@sha256:4af659712ed613d110383f4ac43a102ba887795763f312a8bf8db835653b5cf9 docker://$TARGET_PATH/guardian-application-service:4af659712ed613d110383f4ac43a102ba887795763f312a8bf8db835653b5cf9
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/fbr/guardian-backup-location@sha256:62658a1735311606d584857f902f2c4a423f1c3e85b2ea289ae54727193cd825 docker://$TARGET_PATH/guardian-backup-location:62658a1735311606d584857f902f2c4a423f1c3e85b2ea289ae54727193cd825
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/fbr/guardian-backup-policy@sha256:89e21c7425ea72aef2f3f8e53c36a74d8becb561d3b1e3476b75e22004dd6d49 docker://$TARGET_PATH/guardian-backup-policy:89e21c7425ea72aef2f3f8e53c36a74d8becb561d3b1e3476b75e22004dd6d49
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/fbr/guardian-backup-service@sha256:56e4119fc3ca89fe8a1c2babffaaabf3d91aeecc8076023347a5381c607d4ae3 docker://$TARGET_PATH/guardian-backup-service:56e4119fc3ca89fe8a1c2babffaaabf3d91aeecc8076023347a5381c607d4ae3
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/fbr/guardian-job-manager@sha256:d5eb66db95e62170874e2d0f3ec5e097819596768f90f650013a2456a0fc83b7 docker://$TARGET_PATH/guardian-job-manager:d5eb66db95e62170874e2d0f3ec5e097819596768f90f650013a2456a0fc83b7
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/fbr/guardian-transaction-manager@sha256:f09efb569de67917d41a6b3f374dcee4703f859787513ca452a2c5ad965d3f58 docker://$TARGET_PATH/guardian-transaction-manager:f09efb569de67917d41a6b3f374dcee4703f859787513ca452a2c5ad965d3f58
skopeo copy --insecure-policy --preserve-digests --all docker://cp.icr.io/cp/fbr/guardian-kubevirt-velero-plugin@sha256:9f6d83593f5053c1ece1619243c88ff7fa4a5e3a6a1f9b4df944b45d73211f3e docker://$TARGET_PATH/guardian-kubevirt-velero-plugin:9f6d83593f5053c1ece1619243c88ff7fa4a5e3a6a1f9b4df944b45d73211f3e
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-datamover@sha256:76c3f168faec35d1cf7c56010646b731123ba123abb1a60427409edd13ec6b70 docker://$TARGET_PATH/guardian-datamover:76c3f168faec35d1cf7c56010646b731123ba123abb1a60427409edd13ec6b70
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-dm-operator@sha256:35562a8b290b600c626d81b1e573931d33f2e15e2b0a9d46cd3fb59e23ce0ae8 docker://$TARGET_PATH/guardian-dm-operator:35562a8b290b600c626d81b1e573931d33f2e15e2b0a9d46cd3fb59e23ce0ae8
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-dp-operator@sha256:faec1b7a85aaab714716a850ac4109d6b0079e6214f3e06b1d8a91cd5b73fa5f docker://$TARGET_PATH/guardian-dp-operator:faec1b7a85aaab714716a850ac4109d6b0079e6214f3e06b1d8a91cd5b73fa5f
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/idp-agent-operator@sha256:3a927d363fccfca3ca75023d2c94ed923e6e86828a7d086d790e999b0f0e1ff1 docker://$TARGET_PATH/idp-agent-operator:3a927d363fccfca3ca75023d2c94ed923e6e86828a7d086d790e999b0f0e1ff1
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/idp-server-operator@sha256:50f119e4ae22cc21a4b9b7fe5d3b1da4b8352c2d4635b58bbe5956ae62b36d22 docker://$TARGET_PATH/idp-server-operator:50f119e4ae22cc21a4b9b7fe5d3b1da4b8352c2d4635b58bbe5956ae62b36d22
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/idp-server-operator-bundle@sha256:aadfc6b18c33ed632f660ec5df9e1bf7ed866359737f61ffe27bc308e9816567 docker://$TARGET_PATH/idp-server-operator-bundle:aadfc6b18c33ed632f660ec5df9e1bf7ed866359737f61ffe27bc308e9816567
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/idp-server-operator-catalog@sha256:5462246b796dd0c6e729c8802491b7cd5bb59cb98476ab118bee6a1f520c5c2d docker://$TARGET_PATH/idp-server-operator-catalog:5462246b796dd0c6e729c8802491b7cd5bb59cb98476ab118bee6a1f520c5c2d
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-mongo-operator@sha256:006765a2a3a5451b8eebdc8e0ec10a4384124e99f7099f281ab9f04b13d9e357 docker://$TARGET_PATH/guardian-mongo-operator:006765a2a3a5451b8eebdc8e0ec10a4384124e99f7099f281ab9f04b13d9e357
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-redis-operator@sha256:cb698d0f89bf3c04191dd1902dc1e29269544e7720987aa557fb6b6130d11e0e docker://$TARGET_PATH/guardian-redis-operator:cb698d0f89bf3c04191dd1902dc1e29269544e7720987aa557fb6b6130d11e0e
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-dm-operator-bundle@sha256:938433010f4ed3b71e7eaba41020c5114604ce0d77300aa3efbf2c5fe5465095 docker://$TARGET_PATH/guardian-dm-operator-bundle:938433010f4ed3b71e7eaba41020c5114604ce0d77300aa3efbf2c5fe5465095
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-dp-operator-bundle@sha256:a8fbec8721edb951d02566369df74eea161ad859b3e28d9e44ce7b642fb104d1 docker://$TARGET_PATH/guardian-dp-operator-bundle:a8fbec8721edb951d02566369df74eea161ad859b3e28d9e44ce7b642fb104d1
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/idp-agent-operator-bundle@sha256:a4528ccd64f63e64326dd519fbec19625933f61e150ad3a6f7ba9bcd5a9dcbe2 docker://$TARGET_PATH/idp-agent-operator-bundle:a4528ccd64f63e64326dd519fbec19625933f61e150ad3a6f7ba9bcd5a9dcbe2
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-mongo-operator-bundle@sha256:79a86e9c1160463045fe03f54d8f87b0f7b6e6293a2900d437e8138ab1ff7481 docker://$TARGET_PATH/guardian-mongo-operator-bundle:79a86e9c1160463045fe03f54d8f87b0f7b6e6293a2900d437e8138ab1ff7481
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/guardian-redis-operator-bundle@sha256:ec8bd43483d77e6b0b41daf777d8dbbd83e54fee233e3a7faa714cbf6da1b3f6 docker://$TARGET_PATH/guardian-redis-operator-bundle:ec8bd43483d77e6b0b41daf777d8dbbd83e54fee233e3a7faa714cbf6da1b3f6
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/fbr-mongo-exporter@sha256:21aeeb051009d7784be0e0a8e86440dca26ac2ef57ffc461611de0414f1bb676 docker://$TARGET_PATH/fbr-mongo-exporter:21aeeb051009d7784be0e0a8e86440dca26ac2ef57ffc461611de0414f1bb676
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/fbr-mongo@sha256:73a3b08cd819a2175ae3308dcb72fa07518d0417071f79196338f636219127f4 docker://$TARGET_PATH/fbr-mongo:73a3b08cd819a2175ae3308dcb72fa07518d0417071f79196338f636219127f4
skopeo copy --insecure-policy --preserve-digests --all docker://icr.io/cpopen/fbr-redis@sha256:2131345868484fe9540746c9e4a4a2a9b71dbbb80de5916d74604f2bfc4ec0f5 docker://$TARGET_PATH/fbr-redis:2131345868484fe9540746c9e4a4a2a9b71dbbb80de5916d74604f2bfc4ec0f5
skopeo copy --insecure-policy --preserve-digests --all docker://quay.io/openshift-release-dev/ocp-v4.0-art-dev@sha256:a731786db7f7bc7a4137309a16a7d27acbb9fd21c5731602e2ccaadc58155805 docker://$TARGET_PATH/ocp-v4.0-art-dev:a731786db7f7bc7a4137309a16a7d27acbb9fd21c5731602e2ccaadc58155805
skopeo copy --insecure-policy --preserve-digests --all docker://quay.io/openshift-release-dev/ocp-v4.0-art-dev@sha256:bf7bbc0987b7514ab15f3e20f1b432ee19d09f83c8072900b8718e158f78a5f6 docker://$TARGET_PATH/ocp-v4.0-art-dev:bf7bbc0987b7514ab15f3e20f1b432ee19d09f83c8072900b8718e158f78a5f6
skopeo copy --insecure-policy --preserve-digests --all docker://quay.io/minio/minio@sha256:a9cec9ed5bda5b4e1b2153823e01b309965b9de7ed6eb7f098d45592eecdfc78 docker://$TARGET_PATH/minio:a9cec9ed5bda5b4e1b2153823e01b309965b9de7ed6eb7f098d45592eecdfc78
skopeo copy --insecure-policy --preserve-digests --all docker://registry.redhat.io/rhel9/redis-7@sha256:33d868f8832be3dbe73adaf77e394646c8eda91af9bfb79d5e800c755925878c docker://$TARGET_PATH/rhel9/redis-7:33d868f8832be3dbe73adaf77e394646c8eda91af9bfb79d5e800c755925878cd3577e4

Add ImageContentSourcePolicy after skopeo commands are
executed successfully on the cluster. See the following ImageContentSourcePolicy: Note: Replace the variable
$TARGET_PATH with your registry details where images are
mirrored.
apiVersion: operator.openshift.io/v1alpha1
kind: ImageContentSourcePolicy
metadata:
  labels:
    operators.openshift.org/catalog: "true"
  name: ifbr-offline-mirrors
spec:
  repositoryDigestMirrors:
  - mirrors:
    - $TARGET_PATH
    source: cp.icr.io/cp/fbr
  - mirrors:
    - $TARGET_PATH
    source: icr.io/cpopen
  - mirrors:
    - $TARGET_PATH/rhel9
    source: registry.redhat.io/rhel9
  - mirrors:
    - $TARGET_PATH
    source: quay.io/minio







