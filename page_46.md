https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=data-cataloging



Data Cataloging
Companies need the ability to use unstructured data to meet their business
priorities.
Data Cataloging is a container native modern metadata management software that provides data insight for
exabyte-scale heterogeneous file, object, backup, and archive storage on premises and in the cloud.
The software easily connects to these data sources to rapidly ingest, consolidate, and index
metadata for billions of files and objects.
Data Cataloging provides a rich metadata layer that
enables storage administrators, data stewards, and data scientists to efficiently manage, classify,
and gain insights from massive amounts of data. It improves storage economics, helps mitigate risk,
and accelerates large-scale analytics to create competitive advantage and speed critical
research.
Many companies face significant challenges to manage their 
data. Some difficult challenges that companies face include:

Pinpointing and activating relevant data for large-scale analytics.
Lacking the fine-grained visibility needed to map data to business priorities.
Removing redundant, trivial, and obsolete data.
Identifying and classifying sensitive data.

Note: The IBM Spectrum®
Discover service
name is used interchangeably with  Data Cataloging.    
Benefits of Data Cataloging
Data Cataloging can help you manage your unstructured
data by reducing the data storage costs, uncovering hidden data value, and reducing the risk of
massive data stores. See Table 1.


Table 1. Benefits of Data Cataloging

Optimize - Improve storage usage
Analyze - Uncover hidden data value
Govern - Mitigate risk and improve data quality
Data Management




Decreases storage capital expenditure (CaPex) by facilitating data movement to colder,
cheaper storage.
Accelerates data identification for large-scale analytics.
Perform data inspection and classification.
Automate tags for custom insight.


Increases storage efficiency by eliminating trivial or redundant data.
Operationalize tasks to reduce the burden of data preparation.
Helps ensure that data is compliant with governance policies by
labeling sensitive data.
Create reports for analysis.


Reduces storage operating expenditure (OpEx) by improving storage administrator
productivity.
Orchestrates the ML/DL and Platform Symphony®
MapReduce process.
Helps reduce risk that is hidden in heterogeneous
data sources.
GUI search for real-time results Search content for fast discovery.








Data Cataloging architecture
Data Cataloging is an extensible platform that provides exabyte scale data ingest, data visualization, data activation, and business-oriented data mapping.
Planning

Configuring Data Cataloging
This section provides information on how to deploy and configure Data Cataloging capabilities.
Managing user access
The Data cataloging environment provides access to users and groups. The role that is assigned to a user or group determines the functions that are available. Users and groups can also be associated with collections that use policies that determine the metadata that is available to view.
Managing metadata policies
Policies might be used to automatically tag a set of documents on a periodic basis. In addition, policies might be used to send sets of documents to be deep-inspected by a registered application.
Using content search policies
You can define regular expressions to search for and create policies that use the regular expressions.
Tiering data by using ScaleILM application
Use the IBM Spectrum Discover ScaleILM application to move data to different tiers (pools) that are configured on the IBM Storage Scale connection. 
Copying data by using ScaleAFM application
The ScaleAFM application supports copy function between IBM Storage Scale connection and IBM Cloud® Object Storage connection.
Exporting metadata to IBM Watson Knowledge Catalog
IBM Spectrum Discover Watson™ Knowledge Catalog  (WKC) connector supports export of the metadata to either an IBM Cloud instance or to an On-Premise Instance of the Watson Knowledge Catalog .
Importing externally curated tags for COS/S3 using import tags application
The import tags application is used to import a set of externally curated tags for Cloud Object Storage and S3 services.
Performing retention analytics on IBM Storage Protect archive data
Use IBM Spectrum Discover to perform retention analytics on archive data managed by IBM Storage Protect. 
Managing tags
A tag is a custom metadata field that is used to supplement storage system metadata with organization-specific information. For instance, an organization might segment their storage by project or by chargeback department. Those facets do not show up in the system metadata. Additionally, the storage systems themselves do not provide management and reporting capabilities based on those organizational concepts. Use custom tags to store additional information and manage, report, or search for data by using that organizationally important information.
Discover data
By discovering your data, you can apply policies that assign tags to your data. You can apply tags to the results of a single search, or you can use policies to automatically apply tags on a periodic basis.
Managing applications
An application is a program that interfaces with IBM Spectrum Discover and can access the source storage. There are many use cases for application, including data content inspection for enriching metadata, data movement or migration, data scrubbing or sanitation, and more. Data is identified by IBM Spectrum Discover by policy filter and passed to the application as pointers through a messaging queue. Then, the application performs whatever work is appropriate on the source data and returns a completion status back to IBM Spectrum Discover, which might or might not include enriched metadata for the records. If it does include enriched metadata, IBM Spectrum Discover catalogs that metadata and makes it immediately searchable.
Using the IBM Spectrum Discover application catalog
Use the IBM Spectrum Discover application catalog to search, download, or deploy applications (which are provided by IBM®, customers, or third parties) to use in IBM Spectrum Discover.
Reports
Reports can be generated upon applying tags to a set of data.
High availability for a Db2 Warehouse MPP deployment
For an MPP deployment, Db2® Warehouse provides high availability, offering you the ability to have your data warehouse carry on with its activities if failures occur.
Monitoring data sources
You can use the Home page to monitor the data sources that are connected to your IBM Spectrum Discover environment. Use the Data Source Connections page view details about data source connections.
Monitoring the Data Cataloging service environment
You can monitor the health and status of the Data Cataloging service environment and obtain audit log information.
Updating the network configuration
This topic describes how to update the network configuration.
Using a third-party data movement application to manage data
 Introduction to data movement with IBM Spectrum Discover. 
Enabling feature for skipping the snapshot directories
Enabling skipping feature allows you to skip the metadata ingestion to the snapshot directories.
Data protection

REST API for Data Cataloging

Graceful shutdown
Provides detailed instructions to put Data Cataloging in idle state on an OpenShift® environment. 
Health check monitoring
Provides series of checkpoints to check Data Cataloging health status.
Multiple connection managers
Multiple connection managers are a new capability that is designed to enhance scanning performance and enable parallel ingestion. It proves especially valuable in scenarios where data sources are geographically dispersed and need to be scanned as remote sources.
Collecting logs and metrics
Steps to collect logs and metrics for the Data Cataloging.
Creating a Data Cataloging application for metadata-based policies
Provides information about how to create  Data Cataloging application for metadata-based policies.
Data Cataloging Harvester CLI
Data Cataloging Harvester is a new capability that is designed to import external data to the Data Cataloging service catalog database. It imports the data even if it is not coming from a Db2 database that uses the same schema.
FKEY migration script
The FKEY migration script is a fix to avoid potential rare collisions in the FKEY file identifier when ingesting billions of records.
Configurable Db2 log trimmer
Db2 log trimmer tool provides a mechanism to trim the informative logs that are generated by scanning a data source. It uses the Harvester CLI to ingest data into the Data Cataloging.






