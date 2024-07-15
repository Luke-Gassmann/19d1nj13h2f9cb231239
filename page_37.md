https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=fusion-uninstalling-storage



Uninstalling IBM Storage Fusion
Steps to uninstall IBM Storage Fusion from Red Hat®
OpenShift® web console.
Before you begin

Uninstall all IBM Storage Fusion services before you
uninstall IBM Storage Fusion. For the procedure, see
Uninstalling services.
Ensure that you delete all the connection CRDs. For the procedure to delete, see Uninstalling services.


ProcedureRun the following commands to delete the CRDs and related objects:  
oc delete isfproxydeps isf-proxy
oc delete isflcdeps logcollector
oc delete isfchdeps callhomeclient
oc delete oauthclient isf-oauth
oc delete consolelink ibm-spectrum-fusion

oc delete sppmanagers sppmanager
oc delete updatemanager version
	
oc delete crd fusionservicedefinitions.service.isf.ibm.com
oc delete crd fusionserviceinstances.service.isf.ibm.com
	
oc delete crd odfmanagers.odf.isf.ibm.com
oc delete crd odfclusters.odf.isf.ibm.com
oc delete crd applications.application.isf.ibm.com
oc delete crd clusters.application.isf.ibm.com
oc delete crd connections.application.isf.ibm.com
oc delete crd backuppolicies.data-protection.isf.ibm.com
oc delete crd backups.data-protection.isf.ibm.com
oc delete crd backupstoragelocations.data-protection.isf.ibm.com
oc delete crd callhomes.scale.spectrum.ibm.com
oc delete crd clusters.scale.spectrum.ibm.com
oc delete crd compressionjobs.scale.spectrum.ibm.com
oc delete crd controlplanebackups.bkprstr.isf.ibm.com
oc delete crd csiscaleoperators.csi.ibm.com
oc delete crd daemons.scale.spectrum.ibm.com
oc delete crd deletebackuprequests.data-protection.isf.ibm.com
oc delete crd encryptionclients.cns.isf.ibm.com
oc delete crd encryptionconfigs.scale.spectrum.ibm.com
oc delete crd encryptionservers.cns.isf.ibm.com
oc delete crd filesystems.scale.spectrum.ibm.com
oc delete crd grafanabridges.scale.spectrum.ibm.com
oc delete crd guis.scale.spectrum.ibm.com
oc delete crd hooks.data-protection.isf.ibm.com
oc delete crd ibmsppcs.sppc.ibm.com
oc delete crd ibmspps.ocp.spp.ibm.com
oc delete crd isfchdeps.mgmtsft.isf.ibm.com
oc delete crd isfemdeps.mgmtsft.isf.ibm.com
oc delete crd isflcdeps.mgmtsft.isf.ibm.com
oc delete crd isfproxydeps.mgmtsft.isf.ibm.com
oc delete crd isfuideps.mgmtsft.isf.ibm.com
oc delete crd isfconsoleplugins.mgmtsft.isf.ibm.com
oc delete crd localdisks.scale.spectrum.ibm.com
oc delete crd pmcollectors.scale.spectrum.ibm.com
oc delete crd policyassignments.data-protection.isf.ibm.com
oc delete crd recoverygroups.scale.spectrum.ibm.com
oc delete crd remoteclusters.scale.spectrum.ibm.com
oc delete crd restores.data-protection.isf.ibm.com
oc delete crd scaleclusters.cns.isf.ibm.com
oc delete crd scalemanagers.cns.isf.ibm.com
oc delete crd spectrumfusions.prereq.isf.ibm.com
oc delete crd sppmanagers.spp.isf.ibm.com
oc delete crd updatemanagers.update.isf.ibm.com
oc delete crd computeprovisionworkers.install.isf.ibm.com
oc delete crd storagesetups.install.isf.ibm.com
oc delete crd nodeconfigs.monitor.isf.ibm.com
oc delete crd fusionservicedefinitions.service.isf.ibm.com
oc delete crd fusionserviceinstances.service.isf.ibm.com
oc delete crd recipes.spp-data-protection.isf.ibm.com
oc delete crd sncfilesystems.cns.isf.ibm.com
oc delete crd sncnodes.cns.isf.ibm.com
oc delete crd cloudcsidisks.scale.spectrum.ibm.com
oc delete crd diskjobs.scale.spectrum.ibm.com
oc delete crd dnss.scale.spectrum.ibm.com
oc delete crd dnsconfigs.scale.spectrum.ibm.com
oc delete crd jobs.scale.spectrum.ibm.com
oc delete crd restripefsjobs.scale.spectrum.ibm.com
oc delete crd stretchclusters.scale.spectrum.ibm.com
oc delete crd stretchclusterinitnodes.scale.spectrum.ibm.com
oc delete crd stretchclustertiebreakers.scale.spectrum.ibm.com
oc delete crd upgradeapprovals.scale.spectrum.ibm.com


Log in to Red Hat
OpenShift Container Platform console, go to
Operators > Installed
Operators.
Select IBM Storage Fusion > Uninstall
Operator.
Export IBM Storage Fusion namespace as an
environmental variable. 
Note: If the IBM Storage Fusion is installed in a
different namespace, replace the existing namespace: 
export FUSION_NS="ibm-spectrum-fusion-ns"

Run the following command to delete the IBM Storage Fusion namespace: 
oc delete ns ${FUSION_NS}

Run the following commands to clean the manifests:  

oc delete clusterrole isf-application-operator-role-connection-kube-config
oc delete clusterrolebinding isf-application-operator-rolebinding-connection-kube-config





Parent topic: Deploying IBM Storage Fusion






