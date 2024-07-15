https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=prerequisites-securitycontextconstraints



SecurityContextConstraints
Red Hat®
OpenShift®
SecurityContextConstraints requirement controls pod permissions. These permissions
include pod actions and resources that it can access. 
You do not have to set any of these constraints as all non-default constraints are automatically
set by the product installer. To view the set of SecurityConstantConstraints, log
in to OpenShift Container Platform and run the following
command:oc get scc
For more information about SecurityContextConstraints, see https://docs.openshift.com/container-platform/4.15/authentication/managing-security-context-constraints.html.
The IBM Storage Scale specific constraints are as
follows:Note:
IBM Storage Fusion 2.8.0 or higher supports IBM Storage Scale 5.2.0.

NAME                                      PRIV    CAPS          SELINUX     RUNASUSER          FSGROUP     SUPGROUP    PRIORITY     READONLYROOTFS   VOLUMES
ibm-spectrum-scale-privileged             true    ["*"]         RunAsAny    RunAsAny           RunAsAny    RunAsAny    <no value>   false            ["*"]
restricted-ibm-spectrum-protect-plus-ns   false   <no value>    MustRunAs   MustRunAsRange     MustRunAs   RunAsAny    <no value>   false            ["configMap","downwardAPI","emptyDir","persistentVolumeClaim","projected","secret"]
spectrum-scale-csiaccess                  true    []            RunAsAny    RunAsAny           MustRunAs   RunAsAny    <no value>   false            ["configMap","downwardAPI","emptyDir","hostPath","persistentVolumeClaim","projected","secret"]
data-protection-scc-ibm-backup-restore    true    <no value>    RunAsAny    RunAsAny           RunAsAny    RunAsAny    <no value>   false            
data-protection-scc-ibm-dataprotection    true    <no value>    RunAsAny    RunAsAny           RunAsAny    RunAsAny    <no value>   false            
data-protection-scc-ibm-dp                true    <no value>    RunAsAny    RunAsAny           RunAsAny    RunAsAny    <no value>   false            
guardian-dm-datamover-scc                 true    ["SYS_ADMIN"] RunAsAny    RunAsAny           RunAsAny    RunAsAny    <no value>   false            ["configMap","emptyDir","hostPath","persistentVolumeClaim","secret"]
velero-privileged                         true    ["*"]         RunAsAny    RunAsAny           RunAsAny    RunAsAny    <no value>   false            ["*"]



Parent topic: Prerequisites






