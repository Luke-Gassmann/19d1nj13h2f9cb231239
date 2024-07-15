https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=applications



Applications
Applications contain resources, such as microservices, databases, and other stateful data
distributed across projects. IBM Storage Fusion
provides ways to do application-centric backup, which provides data loss protection for your
applications. 
Note: If IBM Storage Scale is used for storage,
it must have a minimum of 5G PVC size to perform backup and restore operations.
Note: The Applications page shows only local cluster applications or remote DR
applications. Remote Backup & Restore
Spoke applications do not show up on the Hub cluster. To view Spoke applications, go to Backup & Restore > Backed up
applications > Protect apps view.
Application list
The Applications page lists all your OpenShift® applications with their backup
details, such as Name, Used, Capacity,  Backup status, Last
backup on, Success rate, and Policies. 

Table 1. Application list


 
 




Application list
The Applications page lists all your OpenShift applications with their backup
details, such as Name, Used, Capacity, Backup status, Last backup on, and Policies. Note: In the
Applications page, if you continue to see applications that got deleted from OpenShift, check whether associated backups are
available. If you no longer need to restore those backups, delete the Application CR instance of
that application from the CRD. 



Actions 


View details
Use the Search field to filter and find your record from the list. You
can use the settings icon to customize the headings. To view the application details, click the
Name link of the record or click View details in the
ellipsis menu. 


Assign backup policy
To assign backup policy, see Assign backup policy.


Backup now
To start the backup of an application right away, click Backup now in the
ellipsis menu of the application record.


Restore
Restore the application backup. For the steps to restore an application resource, see Restoring an application.








Assign backup policy
Select applications with no policy assigned: 
Select one or more application(s) and click Assign backup policy.
Alternatively, for an application, click  Assign backup policy from the
ellipsis menu. The Assign a backup policy slide out pane gets
displayed.

Select one or more backup policies. You can select Run backup now to
initiate a backup. If you do not see any policy that suits your requirement, create a new policy.
For the procedure to, create a new policy, see Managing backup policies for application workloads.
Click Assign .


Select multiple applications having a mix of policies:
Select one or more application(s) and click Assign backup policy.
Alternatively, for an application, click  Assign backup policy from the
ellipsis menu. The Assign a backup policy slide out pane gets
displayed.

In the Policy provider section, select which service you want to use as a
policy provider. 
Select one or more backup policies. You can select  Run backup now to
initiate a backup. If you do not see any policy that suits your requirement, create a new policy.
For the procedure to, create a new policy, see Managing backup policies for application workloads.
Click Assign .
In the Confirm assignment  confirmation page, go through the information
about the number of applications that cannot be assigned as they use policies that are provided by
another backup service.
Click OK. 






Managing the application details
The application details are classified into Overview, Storage, Backups, and Resources tabs. 






