One of Fasten's long term goals is to support a cloud deployment model with zero-knowledge encryption for your medical records.

While considering the implications of this, it became apparent that I may have to move a majority of the Server side logic to the client-side (Angular SPA). 

This document is my scratchpad/work-in-progress notes as I work on sliming down the Golang Server to almost nothing, and migrate a majority of the logic to Angular. 

# Potential Issues with SPA model
- Some healthcare providers require client id & client secret
- Some healthcare providers speak protocols that are not web friendly - HL7 (how does auth work, what is this protocol)
- Some healthcare providers do not support CORS. 
- Encrypted patient data would need to be synced to a central location from the client side, if the user wants to see the data from multiple devices - zero knowledge encryption
- Progressive Web Apps (PWA) have an install flow that may be unfamiliar to most users. 
- Background refresh of data is difficult, only available while user is logged in. 
	- https://learn.microsoft.com/en-us/microsoft-edge/progressive-web-apps-chromium/how-to/background-syncs
- multi-user roles become complicated

All of these issues need to be solved to implement Zero-knowledge encryption in Fasten

# PouchDB/CouchDB
- https://pouchdb.com/guides/databases.html
- https://rxdb.info/
- https://web.dev/learn/pwa/offline-data/
- https://github.com/go-kivik/kivik

### Security CouchDB
- http://guide.couchdb.org/draft/security.html
- https://mircozeiss.com/couchdb-security-and-pouchdb-authentication
- 
### MultiUser CouchDB
- https://docs.couchdb.org/en/stable/config/couch-peruser.html
- https://docs.huihoo.com/apache/couchdb/2.1/install/docker.html
- https://gist.github.com/nolanlawson/9676093
- https://www.joshmorony.com/creating-a-multiple-user-app-with-pouchdb-couchdb/
- https://www.joshmorony.com/part-2-creating-a-multiple-user-app-with-ionic-2-pouchdb-couchdb/
- https://groups.google.com/g/pouchdb/c/1Nr5ZYC0mc0
- https://github.com/chorpler/pouchdb-authentication
- https://github.com/pouchdb-community/pouchdb-authentication/blob/master/docs/recipes.md#some-people-can-read-some-docs-some-people-can-write-those-same-docs
- https://docs.couchdb.org/en/main/api/server/authn.html
- https://www.bennadel.com/blog/3206-configuring-pouchdb-after-login-for-a-database-per-user-architecture-in-angular-2-4-1.htm
- https://gabrielpoca.com/2017-04-20-how-to-build-offline-web-applications-with-couchdb-and-pouchdb/
https://www.bennadel.com/blog/3212-syncing-local-pouchdb-data-with-remote-ibm-cloudant-database-in-angular-2-4-1.htm


### CouchDB searching & pagination
- https://pouchdb.com/guides/bulk-operations.html
- https://guide.couchdb.org/draft/documents.html
- https://pouchdb.com/guides/documents.html
- https://pouchdb.com/2014/04/14/pagination-strategies-with-pouchdb.html
- 

## Pouchdb Encrypted database
- https://github.com/calvinmetcalf/crypto-pouch/issues/84
- https://github.com/calvinmetcalf/crypto-pouch

# Filesystem Access API 
- https://web.dev/file-system-access/
- https://developer.mozilla.org/en-US/docs/Web/API/File_System_Access_API
- https://stackoverflow.com/questions/62243648/pwa-persistent-storage-best-practice


# PWA
- https://blog.angular-university.io/angular-service-worker/




## Webworker Testing
- http://ryanogles.by/testing-jasvascript-web-workers-with-jasmine/
- 

States


| State Name | Local Database | Remote Database | 