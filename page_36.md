https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=fusion-validating-storage-installation



Validating  IBM Storage Fusion installation
Steps to confirm the success of the installation.

Health status of individual services
Verify the IBM Storage Fusion installation
Verify the Storage or Global data platform installation
Verify the Backup & Restore installation
Verify the IBM Fusion Data Foundation
Verify the Data Cataloging installation
Verify the IBM Storage Fusion CR

Health status of individual services
In the Services page, check the health status of your installed services.
The services must be in running or healthy state. 

Verify the IBM Storage Fusion installation

Verify pods from the OpenShift® Container Platform console:


Click View Operator to view the installed operators in the selected
namespace. In this example, it is ibm-spectrum-fusion-ns namespace.
Go to
Workloads > Pods.
Select the namespace where you installed IBM Storage Fusion.
Check whether the following pods are running successfully: 
isf-application-operator-controller-manager
isf-cns-operator-controller-manager
isf-data-protection-operator-controller-manager
isf-prereq-operator-controller-manager
isf-serviceability-operator-controller-manager
isf-ui-operator-controller-manager
spp-dp-controller-manager 
callhomeclient
isf-proxy
isf-ui-dep
logcollector 
eventmanager
trapserver
isf-update-operator-controller-manager




Alternatively, you can verify the installation by running the oc commands: 

oc get pods -n ibm-spectrum-fusion-ns
A sample result of the oc command is as follows: [root@vm-1527 ~]# oc get pods
NAME                                                              READY   STATUS    RESTARTS   AGE
callhomeclient-75cb5d95b9-f6nmk                                   1/1     Running   0          130m
isf-application-operator-controller-manager-7b95c84d6d-fqpbp      2/2     Running   0          137m
isf-cns-operator-controller-manager-6d8754cfd4-lnnlz              2/2     Running   1          137m
isf-data-protection-operator-controller-manager-986bfc476-pzsv6   2/2     Running   1          137m
isf-prereq-operator-controller-manager-597c68796-62cnk            2/2     Running   1          137m
isf-proxy-5bbcbd786b-hhzsj                                        1/1     Running   0          134m
isf-serviceability-operator-controller-manager-54c555676c-7l4pq   2/2     Running   0          137m
isf-ui-dep-8486747fff-xjhkw                                       1/1     Running   0          134m
isf-ui-operator-controller-manager-6b6678dc9c-sqxhk               2/2     Running   1          137m
logcollector-76f696c4bb-lppmg                                     1/1     Running   0          130m
spp-dp-controller-manager-84b9d984d9-wjwnn                        1/1     Running   1          137m
isf-update-operator-controller-manager-97f666b4f-tc47k            1/1     Running   0Make
sure all the pods are up and running.

Verify the IBM Storage Fusion instances as follows:


Click Operators > Install
operators. Select the namespace in which IBM Storage Fusion was installed from the
Project tab.
Select the IBM Storage Fusion.
Go to All instance tab. It lists the IBM Storage Fusion instances that are created. Ensure that the
status shows completed for all instances.The following instances get created and can be
validation points for IBM Storage Fusion post
installation.

spectrumfusion CR instance of Kind SpectrumFusion
data-cataloging-service-definition CR instance of Kind
FusionServiceDefinition
data-foundation-service CR instance of Kind
FusionServiceDefinition
ibm-backup-restore-agent-service CR instance of Kind
FusionServiceDefinition
ibm-backup-restore-service CR instance of Kind
FusionServiceDefinition
Cluster object of kind Cluster, the name of the object can be the DNS entry of
the cluster.For example: apps.sds-auto3.cp.fyre.ibm.com

CR instance objects of Kind Application with
names:ibm-backup-restore
ibm-data-cataloging
ibm-spectrum-fusion-ns
rook-ceph

CR instance objects of Kind BackupStorageLocation with
names:in-place-snapshot
isf-dp-inplace-snapshot

Recipe object with name fusion-cr-backup





To open the IBM Storage Fusion user interface in the OpenShift Container Platform web console, click the
Applications icon in the title bar and select IBM Storage Fusion.Note: You can use IBM Storage Fusion user interface only when the installation of
IBM Storage Fusion is completed successfully.


Verify the Storage or Global data platform installation
Note:

Ensure that the Global data platform service is enabled before
validation.
IBM Storage Fusion 2.8.0 or higher supports IBM Storage Scale 5.2.0.





Verify whether the IBM Storage Scale
installed successfully.

Note: Before you validate, ensure that the IBM Storage Scale is used as the storage
provider.
Note: The ibm-spectrum-scale namespace does not have any pods until the remote
mount is configured from IBM Storage Fusion UI, that is, the
remote mount filesystem is created.

Run the following command to validate the IBM Storage Scale installation.
oc describe scalemanager -n ibm-spectrum-fusion-ns
Check whether the status at the end of CR reflects as completed.
If the IBM Storage Scale installation is
still in progress, the status continues to show Installing. Wait and ensure that the IBM Storage Scale installation completes.


Verify the IBM Storage Scale pods as
follows:


Verify the IBM Storage Scale pods from the
OpenShift Container Platform console:
Go to
Workloads > Pods.
Select ibm-spectrum-scale, ibm-spectrum-scale-csi, and
ibm-spectrum-scale-operator namespaces. It lists all the pods and makes sure that
all pods are running.Note: The ibm-spectrum-scale namespace does not have any pods
until the remote mount is configured from IBM Storage Fusion
UI.



Verify the IBM Storage Scale deployments and
pods from the IBM Storage Fusion CLI.After you
successfully remote mount the filesystem, run the following commands to validate it.

To list all scale pods, run the following
command:oc -n ibm-spectrum-scale get podsExample output:
./oc get pods -n ibm-spectrum-scale
NAME                               READY   STATUS                  RESTARTS   AGE
ibm-spectrum-scale-gui-0           4/4     Running                 0          8m30s
ibm-spectrum-scale-gui-1           4/4     Running                 0          4m30s
ibm-spectrum-scale-pmcollector-0   2/2     Running                 0          8m
ibm-spectrum-scale-pmcollector-1   2/2     Running                 0          6m29s
worker0                            2/2     Running                 0          8m30s
worker1                            2/2     Running                 0          8m30s
worker2                            2/2     Running                 0          8m30s The
output lists two GUI pods and a daemon pod for each worker node.
Validate pods in ibm-spectrum-scale-dns:
oc get pods -n ibm-spectrum-scale-dnsExample output: 
NAME                               READY   STATUS                  RESTARTS     AGE
coredns-98mqn                       1/1     Running                 0          8m43s
coredns-9ngqc                       1/1     Running                 0          8m43s
coredns-h658w                       1/1     Running                 0          8m43s
coredns-nw8dj                       1/1     Running                 0          8m43s                            2/2     Running                 0          8m30s
coredns-pqh5f                       1/1     Running                 0          8m43s
coredns-qzgdk                       1/1     Running                 0          8m43s

To list all the CSI pods, run the following
command:oc get pods -n ibm-spectrum-scale-csiExample output: 
NAME                                                    READY   STATUS             RESTARTS   AGE
ibm-spectrum-scale-csi-attacher-5d9684696b-9fvdq        1/1     Running               0       3m33s
ibm-spectrum-scale-csi-attacher-5d9684696b-mp8qn        1/1     Running               0       3m33s
ibm-spectrum-scale-csi-f6n17                            3/3     Running               0       3m33s
ibm-spectrum-scale-csi-j22nt                            3/3     Running               0       3m33s
ibm-spectrum-scale-csi-operator-8488bcd9c-vj2bz         1/1     Running               0       102m
ibm-spectrum-scale-csi-provisioner-5d5fbdffbb-qbgx9     1/1     Running               0       3m33s
ibm-spectrum-scale-csi-resizer-7d78944d7b-m74nm         1/1     Running               0       3m33s
ibm-spectrum-scale-csi-snapshotter-7f6dc898f-m5zdn      1/1     Running               0       3m33s
ibm-spectrum-scale-csi-sw9gk                            3/3     Running               0       3m33s
To show the IBM Storage Fusion defined scale cluster,
run the following
command:oc -n ibm-spectrum-fusion-ns get scalecluster -o yaml
To check the scale filesystem CR results, run the following
command:oc -n ibm-spectrum-scale get filesystem -o yaml
To check the scale remote cluster CR result, run the following
command:oc -n ibm-spectrum-scale get remotecluster -o yaml
Run the oc command and check whether Daemon.status.clusterID has a value or
not.oc -n ibm-spectrum-scale get daemon -oyaml







Verify the Backup & Restore installation

Note: Ensure that the Backup & Restore
IBM Storage Fusion service is enabled before
validation.

Verify that the Backup & Restore
IBM Storage Fusion service operators from the OpenShift Container Platform web console:


Go to Operators > Installed
operators from OpenShift Container Platform
web console.
Select the project as
ibm-backup-restore.
Verify that the following operators show the status as succeeded.
Red Hat Integration - AMQ Streams
IBM Storage Fusion Backup and Restore Server
IBM Storage Fusion Backup and Restore Agent
OADP Operator


Alternatively, you can verify the status of operators by running the following oc
command:Note: Note that more operators appear in the command line output than in the web
console.
oc get csv -n ibm-backup-restoreA sample result of the oc
command is as follows:# oc get csv -n ibm-backup-restore
NAME                              DISPLAY                                                 VERSION   REPLACES               PHASE
amqstreams.v2.6.0-2               AMQ Streams                                             2.6.0-2   amqstreams.v2.6.0-1    Succeeded
guardian-dm-operator.v2.8.0       IBM Storage Fusion Backup and Restore Data Mover        2.8.0                            Succeeded
guardian-dp-operator.v2.8.0       IBM Storage Fusion Backup and Restore Data Protection   2.8.0                            Succeeded
guardian-mongo-operator.v2.8.0    IBM Storage Fusion Backup and Restore Mongo             2.8.0                            Succeeded
ibm-dataprotectionagent.v2.8.0    IBM Storage Fusion Backup and Restore Agent             2.8.0                            Succeeded
ibm-dataprotectionserver.v2.8.0   IBM Storage Fusion Backup and Restore Server            2.8.0                            Succeeded
oadp-operator.v1.3.1              OADP Operator                                           1.3.1     oadp-operator.v1.3.0   Succeeded
redis-operator.v2.8.0             IBM Storage Fusion Backup and Restore Redis             2.8.0                            SucceededMake sure that the status shows Succeeded.



Verify the Backup & Restore pods from the OpenShift Container Platform console: 


Go to
Workloads > Pods.
Select the namespace, where you installed IBM Storage Fusion
Backup & Restore. In this case, select
ibm-backup-restore namespace.It lists all the pods. Ensure that all pods are
running.

Verify whether the following pods are running
successfully:amq-streams-cluster-operator
applicationsvc
backup-location-deployment
backup-service
backuppolicy-deployment
guardian-dm-controller-manager
guardian-dp-operator-controller-manager
guardian-kafka-cluster-entity-operator
guardian-kafka-cluster-kafka-0
guardian-kafka-cluster-kafka-1
guardian-kafka-cluster-kafka-2
guardian-kafka-cluster-zookeeper-0
guardian-kafka-cluster-zookeeper-1
guardian-kafka-cluster-zookeeper-2
guardian-minio-0
guardian-mongo-operator-controller-manager
ibm-dataprotectionagent-controller-manager            
ibm-dataprotectionserver-catalog-ibm-backup-restore
ibm-dataprotectionserver-controller-manager
ibm-backup-restoreagent-controller-manager
ibm-backup-restoreserver-controller-manager
job-manager
mongodb-0
mongodb-1
mongodb-2
mongodb-ab-0
openshift-adp-controller-manager
redis-master-0
redis-operator-controller-manager
redis-replicas-0
redis-replicas-1
redis-replicas-2
transaction-manager
velero
Alternatively, you can verify the installation by running the following oc
command:oc get pods -n ibm-backup-restoreA sample result of the oc command
is as
follows:NAME                                                              READY   STATUS      R
amq-streams-cluster-operator-v2.3.0-1-7d6fb79d84-jdkfh            1/1     Running     0
applicationsvc-55c9b4d6c9-6hdv7                                   1/1     Running     0
b0f64f9161e0882f278dde2eaa1ea9677f4a230a29180fcf21fc665761hvvxz   0/1     Completed   0
backup-location-deployment-6b565b856c-j4vjc                       1/1     Running     0
backup-service-54bf9988f6-47bpv                                   1/1     Running     0
backuppolicy-deployment-b997cc9bf-dfwnh                           1/1     Running     0
bc6176f08ef686ccde24395724b77ea07a586a0bd1fa27ebfd5d704d0dxv9pl   0/1     Completed   0
e349f7c16f02ad6c0c31e41ba2fb1750d5154b58537224d239fe47508872cj5   0/1     Completed   0
f3dd0cbe8cb98614cf163fc5372733148236ea2bdeb5efc6a5d5afe4c085qlk   0/1     Completed   0
ff53c6d827e0fd610a4392c4f9411beb0c785572d2fca1bda57e208650bwv2m   0/1     Completed   0
ffacc5cdaa1e0aa4f3b3c0021f3c87931aa7422f8415303d95457febc8nmzk7   0/1     Completed   0
guardian-dm-controller-manager-64d57bf9ff-28dqj                   2/2     Running     0
guardian-dp-operator-controller-manager-6f6d55f6f7-fhndb          2/2     Running     0
guardian-kafka-cluster-entity-operator-b59d699f7-5qxt8            3/3     Running     0
guardian-kafka-cluster-kafka-0                                    1/1     Running     0
guardian-kafka-cluster-kafka-1                                    1/1     Running     0
guardian-kafka-cluster-kafka-2                                    1/1     Running     0
guardian-kafka-cluster-zookeeper-0                                1/1     Running     0
guardian-kafka-cluster-zookeeper-1                                1/1     Running     0
guardian-kafka-cluster-zookeeper-2                                1/1     Running     0
guardian-minio-0                                                  1/1     Running     0
guardian-mongo-operator-controller-manager-6f47776cb4-s6tkm       2/2     Running     0
ibm-dataprotectionagent-controller-manager-54d66f7975-lgdgh       2/2     Running     0
ibm-dataprotectionserver-catalog-ibm-backup-restore-k967t         1/1     Running     0
ibm-dataprotectionserver-controller-manager-749554d89f-q6gmx      2/2     Running     0
job-manager-859484bfc5-fzpt8                                      1/1     Running     0
mongodb-0                                                         2/2     Running     1
mongodb-1                                                         2/2     Running     1
mongodb-2                                                         2/2     Running     1
mongodb-ab-0                                                      1/1     Running     0
openshift-adp-controller-manager-59fb9f86f4-gdbhb                 1/1     Running     0
redis-master-0                                                    1/1     Running     0
redis-operator-controller-manager-647cf89ff7-wl8w2                2/2     Running     0
redis-replicas-0                                                  1/1     Running     0
redis-replicas-1                                                  1/1     Running     0
redis-replicas-2                                                  1/1     Running     0
transaction-manager-5d9b59cf9f-hdzjm                              2/2     Running     0
velero-777d65c9b7-455fv                                           1/1     Running     0




Verify the Backup & Restore
IBM Storage Fusion service installation status from the OpenShift Container Platform web console:


Go to Operators > Installed
operators from OpenShift Container Platform
web console.
Select the namespace as
ibm-backup-restore.
Select IBM Storage Fusion
Backup & Restore server.
Click the Data Protection server tab and select Data Protection server.
Select the YAML tab.
In the status section, makes sure the following: 
HealthStatuses Shows the health status of all components listed. It may take 5
minutes or more for all components to show up as healthy.
Make sure the install status shows Complete and progressPercentage as 100.


Alternatively, you can verify the installation status by running the following oc
command:oc describe dataprotectionserver dataprotectionserver -n ibm-backup-restoreA
sample result of the oc command is as follows:Status:
  Health Statuses:
    Service Name:  applicationservice
    Status:        Healthy
    Service Name:  backuplocation
    Status:        Healthy
    Service Name:  backuppolicy
    Status:        Healthy
    Service Name:  backupservice
    Status:        Healthy
    Service Name:  jobmanager
    Status:        Healthy
    Service Name:  backupagent
    Status:        Healthy
    Service Name:  mongo
    Status:        Healthy
    Service Name:  redis
    Status:        Healthy
    Service Name:  kafka
    Status:        Healthy
  Install Status:
    Progress Percentage:  100
    Retry On Failure:     false
    Status:               Completed
  Installed Version:      2.5.1
  Upgrade In Progress:    false
  Upgrade Status:
    Retry On Failure:  false

Check the status section at the end of the CR and make sure the following: 
The Install Status section shows the status of the install along with the percentage
complete.
The install status shows the install status as Completed when the installation is successfully
completed.
The health status section lists and shows components health status as healthy.

Note: Individual component health statuses may show Unknown or
Degraded for up to five minutes, and show a healthy status when installation is
complete.








Verify the IBM Fusion Data Foundation

Verify the IBM Fusion Data Foundation installation was
completed successfully from the OpenShift Container Platform
console:


Go to Installed Operators to check whether the IBM Fusion Data Foundation operator is listed and status is
Succeeded.
Verify pods from the Red Hat®OpenShift Container Platform web console:
Go to Workloads > Pods. 
Select the openshift-storage namespace, where the IBM Fusion Data Foundation is installed.
Check whether the following pods are running successfully:
csi-addons-controller-manager
noobaa-operator
ocs-metrics-exporter
ocs-operator
odf-console
odf-operator-controller-manager
rook-ceph-operator




Alternatively, you can verify the installation by running the OC
commands:oc get pod -n openshift-storageA sample result of the OC command
is as follows:[root@fu40 ~]# oc get pod -n openshift-storage
NAME                                               READY   STATUS              RESTARTS   AGE
csi-addons-controller-manager-bdb965b47-jvfhs      2/2     Running             0          119s
noobaa-operator-746b6bc54-654lh                    1/1     Running             0          3m3s
ocs-metrics-exporter-69cfc56fd9-jk49s              1/1     Running             0          2m45s
ocs-operator-6879c74556-pppj9                      1/1     Running             0          2m46s
odf-console-849f64fdd7-rqd97                       1/1     Running             0          3m3s
odf-operator-controller-manager-5bd4c85d6b-q8g2f   2/2     Running             0          3m3s
rook-ceph-operator-76699f976c-2zpms                1/1     Running             0          2m46s

Ensure that all the pods are up and running.
Verify the IBM Fusion Data Foundation status as follows:
Click Operators > Install
operators. Select the namespace in which IBM Storage Fusion was installed from the Project tab.
Select the IBM Storage Fusion.
Go to Fusion Service Instance tab and click
odfmanager from the list.
Open YAML tab and ensure that .status.health is
Healthy.


Alternatively, you can verify the status by running the OC
commands:oc get fusionserviceinstances.service.isf.ibm.com -n ibm-spectrum-fusion-ns odfmanager -o jsonpath='{.status.health}{"\n"}'
Verify the local storage operator pods when backing storage type is local as follows:
Click Operators > Install
operators. Select the namespace in which IBM Storage Fusion was installed from the Project tab.
Select the IBM Storage Fusion.
Go to Fusion Service Instance tab and click
odfmanager from the list. 
Click YAML tab and check the
backingStorageType.
- name: backingStorageType
  provided: true
  value: Local

Alternatively, you can verify the backing storage type by running the oc
commands.oc get fusionserviceinstances.service.isf.ibm.com -n ibm-spectrum-fusion-ns odfmanager -o jsonpath='{.spec.parameters}{"\n"}'
If the backing storage type is local, then verify the local storage operator.Go to
Installed Operators to check whether the Local Storage operator is listed and
its status is Succeeded.
Note: The green check mark indicates that the local storage operator is
installed.

Verify pods from the Red HatOpenShift Container Platform web console:
Go to Workloads > Pods. 
Select the openshift-local-storage namespace, where the local storage operator
is installed.
Check whether the following pods are running successfully:
local-storage-operator-xxxxxFor example:
local-storage-operator-75c55cf57d-pfjcp



Ensure that all pods are running.
Alternatively, you can verify the installation by running the oc
commands:oc get pod -n openshift-local-storageA sample result of the oc
command is as follows:[root@fu40 ~]# oc get pod -n openshift-local-storage
NAME                                      READY   STATUS    RESTARTS   AGE
local-storage-operator-75c55cf57d-pfjcp   1/1     Running   0          109s







Verify the Data Cataloging installation


Verify the Data Cataloging installation
was completed successfully from the OpenShift Container Platform web
console:


Run the following command to verify the installed
operators.oc -n ibm-data-cataloging get csvNAME                                                 DISPLAY                VERSION              REPLACES              PHASE
amqstreams.v2.6.0-2                                  AMQ Streams            2.6.0-2              amqstreams.v2.6.0-1   Succeeded
db2u-operator.v110509.0.1                            IBM Db2                110509.0.1                                 Succeeded
ibm-spectrum-discover-operator.v216.0.0-1715012933   IBM Storage Discover   216.0.0-1715012933                         Succeeded

Run the following command to verify Data Cataloging
status.oc -n ibm-data-cataloging get isdExpected output
NAME                               READY   SUMMARY                        ERROR   AGE   HEALTHSTATUS
data-cataloging-service-instance   True    Awaiting next reconciliation           9d    Healthy

Run the following command to verify that all Persistent Volume Claims are
bounded.oc -n ibm-data-cataloging get pvcExpected output
NAME                        STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS                AGE
activelogs-c-isd-db2u-0     Bound    pvc-7e98eead-9a38-48b6-a880-16d730120796   150Gi      RWO            ocs-storagecluster-cephfs   9d
activelogs-c-isd-db2u-1     Bound    pvc-7af71786-1529-4b3c-bbd1-b5d1ee733d33   150Gi      RWO            ocs-storagecluster-cephfs   9d
c-isd-meta                  Bound    pvc-1ba20699-ddb8-4600-bf9f-4d637b14da49   50Gi       RWX            ocs-storagecluster-cephfs   9d
data-c-isd-db2u-0           Bound    pvc-488540db-c951-4f48-b65c-814bf634ca33   300Gi      RWO            ocs-storagecluster-cephfs   9d
data-c-isd-db2u-1           Bound    pvc-56a3105a-347e-4b55-b11a-d0a1d351d622   300Gi      RWO            ocs-storagecluster-cephfs   9d
data-isd-sasl-kafka-0       Bound    pvc-3924c9cc-173d-4244-90fa-a234325dc04b   100Gi      RWO            ocs-storagecluster-cephfs   9d
data-isd-sasl-zookeeper-0   Bound    pvc-3c66397b-ac03-4ed8-841a-e33d83355a23   64Gi       RWO            ocs-storagecluster-cephfs   9d
data-isd-ssl-kafka-0        Bound    pvc-ce0ebeaf-d2b6-4e40-8c31-e31d45a208e5   100Gi      RWO            ocs-storagecluster-cephfs   9d
data-isd-ssl-zookeeper-0    Bound    pvc-cd3fdd20-343b-49ca-ad1a-690f8eec3e60   64Gi       RWO            ocs-storagecluster-cephfs   9d
isd-backup                  Bound    pvc-2e077c8e-e992-4e1a-8b98-d24bfdbb5343   250Gi      RWX            ocs-storagecluster-cephfs   9d
isd-data                    Bound    pvc-b98e124f-1f98-43e5-9bf6-c8758c681192   250Gi      RWX            ocs-storagecluster-cephfs   9d
tempts-c-isd-db2u-0         Bound    pvc-7fdc9ac5-9158-48ac-bad3-3c24590f1f2b   50Gi       RWO            ocs-storagecluster-cephfs   9d
tempts-c-isd-db2u-1         Bound    pvc-a2adb668-a362-4f61-8ed3-ae103f9b2cd3   50Gi       RWO            ocs-storagecluster-cephfs   9d

Run the following command to verify Db2u cluster detailed
progress.oc -n ibm-data-cataloging get formations.db2u.databases.ibm.com isd -o go-template='{{range .status.components}}{{printf "%s,%s,%s\n" .kind .name .status.state}}{{end}}' | column -s, -tExpected output
account                account-ibm-data-cataloging-isd  OK
PersistentVolumeClaim  c-isd-meta                       OK
secret                 c-isd-sshkeys-db2uhausr          OK
secret                 c-isd-sshkeys-db2uadm            OK
secret                 c-isd-sshkeys-db2instusr         OK
secret                 c-isd-ldappassword               OK
secret                 c-isd-ldapblueadminpassword      OK
secret                 c-isd-instancepassword           OK
secret                 c-isd-db2u-lic                   OK
secret                 c-isd-certs-wv-rest              OK
secret                 c-isd-certs-db2u-api             OK
configmap              c-isd-db2uconfig                 OK
configmap              c-isd-db2regconfig               OK
configmap              c-isd-db2dbmconfig               OK
configmap              c-isd-db2dbconfig                OK
service                c-isd-ldap                       OK
Deployment             c-isd-ldap                       OK
service                c-isd-tools                      OK
Deployment             c-isd-tools                      OK
configmap              c-isd-db2u-api                   OK
service                c-isd-db2u-engn-svc              OK
service                c-isd-db2u-head-engn-svc         OK
Job                    c-isd-instdb                     OK
service                c-isd-etcd                       OK
StatefulSet            c-isd-etcd                       OK
service                c-isd-db2u-rest-svc              OK
networkpolicy          c-isd-rest-ext                   OK
Deployment             c-isd-rest                       OK
service                c-isd-db2u-graph-svc             OK
networkpolicy          c-isd-graph-ext                  OK
Deployment             c-isd-graph                      OK
service                c-isd-db2u-internal              OK
service                c-isd-db2u                       OK
StatefulSet            c-isd-db2u                       OK
networkpolicy          c-isd                            OK
networkpolicy          c-isd-ext                        OK
Job                    c-isd-restore-morph              OK

Run the following command to verify the Db2u cluster CR
status.oc -n ibm-data-cataloging get db2uclusterExpected output
NAME   STATE   MAINTENANCESTATE   AGE
isd    Ready   None               9d

Run the following command to verify that the ports 50000 and 50001 are
listing.oc exec -n ibm-data-cataloging -it $(oc -n ibm-data-cataloging get po --no-headers --show-labels=true --selector name=dashmpp-head-0 | awk '{print $1}') -- su - db2inst1 -c 'netstat -ntlp'Expected output
Defaulted container "db2u" out of: db2u, init-labels (init), init-kernel (init)
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 10.254.4.11:60000       0.0.0.0:*               LISTEN      23707/db2sysc 0
tcp        0      0 10.254.4.11:60001       0.0.0.0:*               LISTEN      23712/db2sysc 1
tcp        0      0 0.0.0.0:9443            0.0.0.0:*               LISTEN      -
tcp        0      0 0.0.0.0:50022           0.0.0.0:*               LISTEN      -
tcp        0      0 0.0.0.0:50000           0.0.0.0:*               LISTEN      23707/db2sysc 0
tcp        0      0 0.0.0.0:50001           0.0.0.0:*               LISTEN      23707/db2sysc 0
tcp6       0      0 :::50052                :::*                    LISTEN      -
tcp6       0      0 :::50022                :::*                    LISTEN      -

Run the following command to verify that workload is
PUREDATA_OLAP.oc exec -n ibm-data-cataloging -c db2u -it $(oc -n ibm-data-cataloging get po --no-headers --show-labels=true --selector name=dashmpp-head-0 | awk '{print $1}') -- sudo su - db2inst1 -c "db2set -all | grep DB2_WORKLOAD= | awk '{print \$2}'"Expected output
DB2_WORKLOAD=PUREDATA_OLAP

Run the following command to verify the database encryption
configurations.oc -n ibm-data-cataloging exec -c db2u $(oc -n ibm-data-cataloging get po --no-headers --show-labels=true --selector name=dashmpp-head-0 | awk '{print $1}') -- su - db2inst1 -c "db2 get db cfg for bludb | grep 'Encrypted database'" Encrypted database                                      = YES

Run the following command to verify the Kafka CRs
readiness.oc -n ibm-data-cataloging get kafkaExpected output
NAME       DESIRED KAFKA REPLICAS   DESIRED ZK REPLICAS   READY   WARNINGS
 isd-sasl   1                        1                     True
 isd-ssl    1                        1                     True

Run the following command to verify that the IBM®
Spectrum Discover pods are
running.oc -n ibm-data-cataloging get pod -l component=discoverExpected output
 NAME                                         READY   STATUS      RESTARTS     AGE
isd-api-7564475d98-cs6nx                     1/1     Running     0            9d
isd-auth-5fcb8bd95f-jvzwp                    1/1     Running     0            9d
isd-backup-restore-689fc64f7-pgx22           1/1     Running     0            9d
isd-connmgr-7d4cdb4cc7-xnkzm                 1/1     Running     1 (9d ago)   9d
isd-consumer-ceph-le-5f9b5d4676-4fsgg        1/1     Running     0            9d
isd-consumer-ceph-le-5f9b5d4676-9k9cs        1/1     Running     0            9d
isd-consumer-ceph-le-5f9b5d4676-bphqp        1/1     Running     0            9d
isd-consumer-ceph-le-5f9b5d4676-cc2pz        1/1     Running     0            9d
isd-consumer-ceph-le-5f9b5d4676-chlvk        1/1     Running     0            9d
isd-consumer-ceph-le-5f9b5d4676-fchp5        1/1     Running     0            9d
isd-consumer-ceph-le-5f9b5d4676-jlbrw        1/1     Running     0            9d
isd-consumer-ceph-le-5f9b5d4676-l78cc        1/1     Running     0            9d
isd-consumer-ceph-le-5f9b5d4676-lpcsn        1/1     Running     0            9d
isd-consumer-ceph-le-5f9b5d4676-n2wqt        1/1     Running     0            9d
isd-consumer-cos-le-846f5fd97f-54qm9         1/1     Running     0            9d
isd-consumer-cos-le-846f5fd97f-6hsq9         1/1     Running     0            9d
isd-consumer-cos-le-846f5fd97f-9p4p5         1/1     Running     0            9d
isd-consumer-cos-le-846f5fd97f-dhlgc         1/1     Running     0            9d
isd-consumer-cos-le-846f5fd97f-hr76h         1/1     Running     0            9d
isd-consumer-cos-le-846f5fd97f-mkvx8         1/1     Running     0            9d
isd-consumer-cos-le-846f5fd97f-tvscz         1/1     Running     0            9d
isd-consumer-cos-le-846f5fd97f-vrrd4         1/1     Running     0            9d
isd-consumer-cos-le-846f5fd97f-w59c2         1/1     Running     0            9d
isd-consumer-cos-le-846f5fd97f-xqncl         1/1     Running     0            9d
isd-consumer-cos-scan-79fb979585-4klcc       1/1     Running     0            9d
isd-consumer-cos-scan-79fb979585-8r6w7       1/1     Running     0            9d
isd-consumer-cos-scan-79fb979585-fqs5m       1/1     Running     0            9d
isd-consumer-cos-scan-79fb979585-fwb8p       1/1     Running     0            9d
isd-consumer-cos-scan-79fb979585-h78g5       1/1     Running     0            9d
isd-consumer-cos-scan-79fb979585-lvwl5       1/1     Running     0            9d
isd-consumer-cos-scan-79fb979585-nhznb       1/1     Running     0            9d
isd-consumer-cos-scan-79fb979585-q2l8b       1/1     Running     0            9d
isd-consumer-cos-scan-79fb979585-z6tfj       1/1     Running     0            9d
isd-consumer-cos-scan-79fb979585-zv2zw       1/1     Running     0            9d
isd-consumer-file-scan-5c7565bf7b-5mrrg      1/1     Running     0            9d
isd-consumer-file-scan-5c7565bf7b-8rphj      1/1     Running     0            9d
isd-consumer-file-scan-5c7565bf7b-b5dbv      1/1     Running     0            9d
isd-consumer-file-scan-5c7565bf7b-b5lv2      1/1     Running     0            9d
isd-consumer-file-scan-5c7565bf7b-d9gbm      1/1     Running     0            9d
isd-consumer-file-scan-5c7565bf7b-f5rxf      1/1     Running     0            9d
isd-consumer-file-scan-5c7565bf7b-m8nw6      1/1     Running     0            9d
isd-consumer-file-scan-5c7565bf7b-ntfbb      1/1     Running     0            9d
isd-consumer-file-scan-5c7565bf7b-ql55x      1/1     Running     0            9d
isd-consumer-file-scan-5c7565bf7b-qvggm      1/1     Running     0            9d
isd-consumer-protect-scan-67d5ffb65-6s75x    1/1     Running     0            9d
isd-consumer-protect-scan-67d5ffb65-845bx    1/1     Running     0            9d
isd-consumer-protect-scan-67d5ffb65-8kmnf    1/1     Running     0            9d
isd-consumer-protect-scan-67d5ffb65-gntbt    1/1     Running     0            9d
isd-consumer-protect-scan-67d5ffb65-mlnfb    1/1     Running     0            9d
isd-consumer-protect-scan-67d5ffb65-p9lpt    1/1     Running     0            9d
isd-consumer-protect-scan-67d5ffb65-rckm8    1/1     Running     0            9d
isd-consumer-protect-scan-67d5ffb65-vkmpd    1/1     Running     0            9d
isd-consumer-protect-scan-67d5ffb65-vmh8x    1/1     Running     0            9d
isd-consumer-protect-scan-67d5ffb65-zm4gf    1/1     Running     0            9d
isd-consumer-scale-le-5d56449994-6dw9h       1/1     Running     0            9d
isd-consumer-scale-le-5d56449994-9nhsz       1/1     Running     0            9d
isd-consumer-scale-le-5d56449994-dnwpw       1/1     Running     0            9d
isd-consumer-scale-le-5d56449994-dz2mf       1/1     Running     0            9d
isd-consumer-scale-le-5d56449994-h2ffj       1/1     Running     0            9d
isd-consumer-scale-le-5d56449994-hdrxg       1/1     Running     0            9d
isd-consumer-scale-le-5d56449994-nf779       1/1     Running     0            9d
isd-consumer-scale-le-5d56449994-pf6n4       1/1     Running     0            9d
isd-consumer-scale-le-5d56449994-q8gqf       1/1     Running     0            9d
isd-consumer-scale-le-5d56449994-xzmvh       1/1     Running     0            9d
isd-consumer-scale-scan-7bdc7957c6-49vkb     1/1     Running     0            9d
isd-consumer-scale-scan-7bdc7957c6-54pb8     1/1     Running     0            9d
isd-consumer-scale-scan-7bdc7957c6-5sr89     1/1     Running     0            9d
isd-consumer-scale-scan-7bdc7957c6-98lm9     1/1     Running     0            9d
isd-consumer-scale-scan-7bdc7957c6-d4zlj     1/1     Running     0            9d
isd-consumer-scale-scan-7bdc7957c6-fc82j     1/1     Running     0            9d
isd-consumer-scale-scan-7bdc7957c6-mnsn2     1/1     Running     0            9d
isd-consumer-scale-scan-7bdc7957c6-r2kc6     1/1     Running     0            9d
isd-consumer-scale-scan-7bdc7957c6-tglsz     1/1     Running     0            9d
isd-consumer-scale-scan-7bdc7957c6-zbhgv     1/1     Running     0            9d
isd-contentsearchagent-5d7bfbd887-r487x      1/1     Running     1 (9d ago)   9d
isd-db-schema-xm5cn                          0/1     Completed   0            9d
isd-db2whrest-6c6bbfcbc6-9v6v2               1/1     Running     1 (9d ago)   9d
isd-generate-license-6g94v                   0/1     Completed   0            9d
isd-importtags-64498dbdd8-5kqpb              1/1     Running     1 (9d ago)   9d
isd-keystone-7dc84b69f5-sw6nn                1/1     Running     0            9d
isd-license-check-27982200-c9gkm             0/1     Completed   0            2d21h
isd-license-check-27983640-ldxv2             0/1     Completed   0            45h
isd-license-check-27985080-rhzjl             0/1     Completed   0            21h
isd-policyengine-598f565867-zg5sn            1/1     Running     1 (9d ago)   9d
isd-producer-ceph-le-76b9885854-557b7        1/1     Running     0            9d
isd-producer-cos-le-85d446c9d8-zvzmg         1/1     Running     0            9d
isd-producer-cos-scan-d584f646d-2t669        1/1     Running     0            9d
isd-producer-file-scan-5586b48fd-zkt7q       1/1     Running     0            9d
isd-producer-protect-scan-7b66bb7c64-wz6qq   1/1     Running     0            9d
isd-producer-scale-le-8d7bc64b4-nvqbl        1/1     Running     0            9d
isd-producer-scale-scan-5df647956-qfl6p      1/1     Running     0            9d
isd-proxy-5f4d7dd8ff-44fwt                   1/1     Running     0            9d
isd-reports-c6kmq                            0/1     Completed   0            9d
isd-scaleafmdatamover-85cc44b566-644vx       1/1     Running     1 (9d ago)   9d
isd-scaleilmdatamover-6b86dd7b58-j28sn       1/1     Running     1 (9d ago)   9d
isd-sdmonitor-6fffc999b7-s2srd               1/1     Running     0            9d
isd-tikaserver-79548bdb4-ssft5               1/1     Running     0            9d
isd-ui-backend-f6c4b65d7-dwzrs               1/1     Running     0            9d
isd-ui-frontend-9659fc847-vcbmv              1/1     Running     0            9d

Run the following command to verify the console route
availability.oc -n ibm-data-cataloging get route consoleExpected output
NAME      HOST/PORT                                       PATH   SERVICES   PORT    TERMINATION   WILDCARD
console   console-ibm-data-cataloging.apps.ocp2.vmlocal          isd-svc    <all>   reencrypt     None






Verify the IBM Storage Fusion CR


IBM Storage Fusion installation status can also be
checked through IBM Storage Fusion
CR.



Important: The IBM Storage Fusion
namespace ibm-spectrum-fusion-ns is used in the following steps for your reference.
If IBM Storage Fusion is installed in a different
namespace, replace the namespace with your namespace.
Run the following command and export IBM Storage Fusion namespace as environmental
variable.export FUSION_NS="ibm-spectrum-fusion-ns"
Run the command to validate the IBM Storage Fusion
installation
status.oc describe SpectrumFusion/spectrumfusion -n $FUSION_NSWhere the
SpectrumFusion is the kind of the CR and spectrumfusion is name of
the CR.

Navigate to OpenShift Container Platform console, go to
Operators >  Installed
operators.
Select the IBM Storage Fusion namespace from the
Project  drop down and select the Storage Fusion tab.
It shows the CR kind and name of the CR.

This CR show status and version of all IBM Storage Fusion services as well as the IBM Storage Fusion Install
status.Spec:
   Global Data Platform: 
      Enable: true
   License: 
      Accept: trueStatus: 
    Global Data Platform Status: 
       Service Enabled:              true
       Health:                       Healthy
       Install Status:               Completed
       Install Status Message:       IBM Spectrum Scale storage installation is succeeded.
       Install Status Message Code:  BMYSS0003
       Is CRC Rendered:              false
       Is Deployable:                true
       Is Machine config Rendered:   false
       Is supported:                 true
       Is Upgrade Failed:            false
       Is Upgrade In Progress:       false
       Max Available Version:        5.2.0
       Progress Percentage:          100
       Upgrade Available:            false
       Version:                      5.2.0
  Events: <none> 








Parent topic: Deploying IBM Storage Fusion






