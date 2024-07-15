https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=registry-mirroring-red-hat-operator-images-enterprise



Mirroring Red Hat operator images to
enterprise registry 
Mirror the Red Hat® operator images to
your enterprise registry. 
Before you begin

Make sure that you go through the Before you begin section and About the
task section of Mirroring your images to the enterprise registry. For more information
about the installation of Red Hat operator
images, see Using Operator Lifecycle Manager on restricted networks .
Make sure that you install the oc-mirror OpenShift CLI plug-in. For more
information about oc-mirror OpenShift CLI plug-in installation, see Installing the oc-mirror OpenShift CLI plugin.
The registry must have at least one directory path specified. For
example:
https://<enterprise registry host>:<enterprise registry port>/<mandatory root path>


ProcedureLog in to quay.io and run the following command to login to the Docker registry with your
Red Hat enterprise credentials: 
podman login registry.redhat.io -u <Red Hat enterprise registry username> -p <Red Hat enterprise registry password>
Set the following environment variables:
export LOCAL_ISF_REGISTRY="<Your enterprise registry host>:<port>"
export LOCAL_ISF_REPOSITORY="<Your image path>"
export TARGET_PATH="$LOCAL_ISF_REGISTRY/$LOCAL_ISF_REPOSITORY"
echo "$TARGET_PATH"Note:

If you face any issues during mirroring Red Hat operator 4.15 images, then use either Ubuntu 22 or higher or RHEL 9 or higher server versions to
mirror. For more information, see the Red Hat
issue https://access.redhat.com/solutions/7062641.
Port is a non-mandatory value when you set the LOCAL_ISF_REGISTRY variable. You
can ignore this if your enterprise registry is accessible and has a secure connection.


Sample value for without
port:export LOCAL_ISF_REGISTRY="registryhost.com"
See the
following sample values:

export LOCAL_ISF_REGISTRY="registryhost.com:443"
export LOCAL_ISF_REPOSITORY="fusion-mirror"

LOCAL_ISF_REGISTRY is your entitlement registry. 
LOCAL_ISF_REPOSITORY is the image path in which you want to mirror the images.
You can choose your own repository paths. For example, sds-2.8.0/isf or sds-2.8.0.

Run the command to login to the Docker registry with your enterprise registry
credentials. 
podman login $LOCAL_ISF_REGISTRY -u <your enterprise registry username> -p <your enterprise registry password>

Create an image set configuration file for Red Hat packages that are required for IBM Storage Fusion installation. For
example:cat << EOF > imageset-config-redhatoperator.yaml
kind: ImageSetConfiguration
apiVersion: mirror.openshift.io/v1alpha2
mirror:
  operators:
    - catalog: registry.redhat.io/redhat/redhat-operator-index:$OCP_VERSION
      packages:
        - name: "amq-streams"
        - name: "redhat-oadp-operator"
EOF
Note:

The redhat-oadp-operator and amq-streams packages are
required to install the Red Hat OADP operator and
AMQ Streams operator. It is a prerequisite to deploy the IBM Backup & Restore service. If you plan to use the IBM Backup & Restore service, retain it in the commands, or else
you can skip it.
The amq-streams package is required to install the Data Cataloging service. If you plan to use the IBM Data Cataloging service, retain it in the commands, or else
you can skip it.



Run the following oc command to mirror the images from the specified
image set configuration to a specified registry. 
oc mirror --config imageset-config-redhatoperator.yaml docker://$TARGET_PATH --dest-skip-tls --ignore-history 
This can take 5-10 minutes to complete. 
Example output:Rendering catalog image "<TARGET_PATH>/redhat/redhat-operator-index:v4.15" with file-based catalog
Writing image mapping to oc-mirror-workspace/results-1693810862/mapping.txt
Writing CatalogSource manifests to oc-mirror-workspace/results-1693810862
Writing ICSP manifests to oc-mirror-workspace/results-1693810862


After you mirror the content to your registry, go to the generated
oc-mirror-workspace/ directory. Go to the results-1xxxx directory, and verify that the
YAML files are present for the ImageContentSourcePolicy and
CatalogSource resources.
Apply the generated ImageContentSourcePolicy to the cluster. 
cd ./oc-mirror-workspace/results-<generated_id>
oc apply -f imageContentSourcePolicy.yaml
You can run this step only once when the cluster is up for a freshly installed rack.

Apply the generated CatalogSource to the cluster. 
oc apply -f catalogSource-cs-redhat-operator-index.yaml








