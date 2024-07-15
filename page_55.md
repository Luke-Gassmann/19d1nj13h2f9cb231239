https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=storage-fusion-considerations-gdpr-readiness



IBM Storage Fusion considerations for GDPR
readiness

Notice
This document is intended to help you in your preparations for GDPR readiness. It provides
information about features of IBM Storage Fusion that you
can configure, and aspects of the product’s use, that you must consider to help your organization
with GDPR readiness. This information is not an exhaustive list, due to the many ways that clients
can choose and configure features, and the large variety of ways that the product can be used in
itself and with third-party applications and systems.
Clients are responsible for ensuring their own compliance with
various laws and regulations, including the European Union General Data Protection Regulation.
Clients are solely responsible for obtaining advice of competent legal counsel as to the
identification and interpretation of any relevant laws and regulations that might affect the
clients' business and any actions the clients might need to take to comply with such laws and
regulations.
The products, services, and other capabilities that are
described here are not suitable for all client situations and might have restricted availability.
IBM does not provide legal, accounting, or auditing advice or represent or warrant that its services
or products ensure that clients are in compliance with any law or regulation.

Table of Contents

GDPR
Product configuration -
considerations for GDPR readiness
Data life cycle
Data collection
Data storage
Data access
Data processing
Data deletion
Data monitoring
Responding to data subject
rights


GDPR
General Data Protection Regulation (GDPR) is adopted by the European Union ("EU") and applies
from 25 May 2018.
Why is GDPR important?GDPR establishes a stronger data protection regulatory
framework for processing of personal data of individuals. GDPR brings:
New and enhanced rights for individuals
Widened definition of personal data
New obligations for processors
Potential for significant financial penalties for non-compliance
Compulsory data breach notification



Read more about GDPR

EU GDPR Information
Portal
ibm.com/GDPR website




Product configuration – considerations for GDPR readiness
The following sections provide considerations for configuring IBM Storage Fusion to help your organization with GDPR
readiness.

Data life cycle
User accountsThe IBM Storage Fusion
system administrator or security administrator creates a user by providing a user ID, email address,
full name, and password to grant the user access to the system. This personal data is stored in the
database on the client's hardware and can be fully managed by the system administrator or security
administrator and edited by the user.
Information on managing users is documented in IBM
Documentation (IBM Docs) for IBM Storage Fusion.

System logsPersonal data, including IP addresses, session IDs, user IDs,
web-page URLs, and cookie names, might exist within operating system and application logs. The data
within these logs is captured automatically as part of the offering and is beyond the control of the
client. The logs are retained on disk when sufficient space is available. As more space is needed,
older log files are removed. The log files might not be modified or deleted by the client.
The
purpose of the system log files is for use during troubleshooting situations. As needed, the log
files might be collected and downloaded from the offering for transfer to IBM Support. The log files
are not included in the system backups and are therefore constrained to the node unless involved
while logs are collected for troubleshooting activity. 
Information on system logs is
documented in IBM Documentation for IBM Storage Fusion.

Personal data used for online contact with IBMIBM Storage Fusion clients can submit online
comments/feedback/requests to contact IBM about IBM Storage Fusion subjects in various ways, primarily:
Public comments area on pages in the IBM Storage Fusion community.
Public comments area on pages of IBM Storage Fusion
documentation in IBM Documentation.
Public comments in the IBM Storage Fusion space of
dWAnswers
Feedback forms in the IBM Storage Fusion
community


Typically, only the client name and email address are used, to enable personal replies
for the subject of the contact, and the use of personal data conforms to the IBM Online Privacy
Statement.


Data collection
For more information, see Data life
cycle.

Data storage
Personal data is contained within backups of the offerings. Such personal data includes the
personal data that is associated with user accounts that are stored within the database. The IBM
Documentation provides information pertaining to creating the backups within the IBM Storage Fusion offering.
The backup feature enables the client to transfer the backup archives to an external location.
However, management of any external backup archives is beyond the scope of the offering. The client
must implement a set of established 'best practices' for managing and securing such backup files.
Information on managing backups is documented in IBM Documentation for IBM Storage Fusion.

Data access
General security measures (for example, disk encryption, physical and remote access) either
directly implemented by the offering or suggested actions for the client's preparedness to deploy
the offering are documented in IBM Documentation.
For user account data, read or write access can be given to specific users.

Data processing
General security measures are directly implemented by the offering.

Data deletion
Personal data associated with user accounts (as described in Data life cycle) can be fully managed
by the system administrator or security administrator, including deletion. Users are not authorized
to delete the personal data associated with the accounts. Information on managing users is
documented in IBM Documentation for IBM Storage Fusion.
Personal data, including IP addresses, session IDs, and user IDs, might exist within operating
system and application logs. The log files might not be modified or deleted by the client. The logs
are retained on disk when sufficient space is available. As more space is needed, older log files
are removed. The log files might not be modified or deleted by the client. Information on system
logs is documented in IBM Documentation for IBM Storage Fusion.

Data monitoring
IBM Storage Fusion does not monitor operating system
or application logs, which are collected by the system and remain on the node as space permits. When
needed for troubleshooting, logs might be downloaded from the console. Typically, such files remain
local to the offering and cannot be managed or altered by users or administrators. Administrators
might be able to review some log files (for troubleshooting purposes and without context of any
personal data that is contained within) from the offering console. For more complex troubleshooting
situations, such logs might be collected and downloaded from the offering for transmission to IBM
Support.

Responding to data subject rights
IBM Storage Fusion meets the following data subject
rights: right to access, modify, forgotten, and portability.







