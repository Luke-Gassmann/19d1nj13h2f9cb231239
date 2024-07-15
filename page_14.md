https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=prerequisites-creating-image-pull-secret



Creating image pull secret
Create an image pull secret to enable the OpenShift® cluster to authenticate with the IBM
Entitled Registry. The image pull secret provides the credentials for pulling Docker images from the
IBM Entitled Registry.
Before you begin

As a prerequisite to run base64, you must install base64 or jq.Download the
jq JSON processor command line package. To download the jq JSON
processor package, see Download the jq JSON processor command line
package. You use jq to combine the JSON value of the default global pull
secret with the private registry pull secret that you want to add.

Ensure that you have access to https://cloud.ibm.com/docs/openshift?topic=openshift-access_cluster.


ProcedureRun the following command to log in to OpenShift system:  
oc login --token=<API token> --server=https://<server name>:6443


Create a base64 encoded string of the credentials used to access the image registry. 
Linux example:
echo -n "cp:GENERATED_ENTITLEMENT_KEY" | base64 -w0
Windows
example:echo -n "cp:GENERATED_ENTITLEMENT_KEY" | base64 -e

Note: Replace GENERATED_ENTITLEMENT_KEY with the entitlement key that you generated
in Obtaining entitlement key.



Create an authority.json to include the base64 encoded string of your
credentials (created in the previous step), user name (to access cp.icr.io
repository), and generated entitlement key for the IBM Cloud Container
Registry. Windows or Linux example:{
  "auth": "BASE64_ENCODED_ENTITLEMENT_KEY"
}Note: Replace BASE64_ENCODED_ENTITLEMENT_KEY with the value of base64
encoded entitlement key got from the previous step. 

The following step takes the authority.json and includes it as a new
authority in your .dockerconfigjson, stored as a
temp_config.json. 
oc get secret/pull-secret -n openshift-config -ojson | \
jq -r '.data[".dockerconfigjson"]' | \
base64 -d - | \
jq '.[]."cp.icr.io" += input' - authority.json > temp_config.json
Note: The referenced jq command is not installed on OpenShift Container Platform clusters by default. Run the following
command to install jq: yum install jqThe yum install jq
command is for Red Hat® Enterprise Linux systems. For other
operating system, use the appropriate commands to install jq.


Use the contents of the temp_config.json file and apply the updated
config to the OpenShift cluster. 
oc set data secret/pull-secret -n openshift-config --from-file=.dockerconfigjson=temp_config.json

To verify whether your pull-secret is updated with your new authority, run the following
command and confirm that your authority is present. 
oc get secret/pull-secret -n openshift-config -ojson | \
jq -r '.data[".dockerconfigjson"]' | \
base64 -d -
The updated config is now rolled out to all the nodes in the OpenShift
cluster.
When the global pull secret is updated, enter the following command to remove the
temporary files that were created. 
rm authority.json temp_config.json





Parent topic: Prerequisites






