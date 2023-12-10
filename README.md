# Google Cloud Professional Data Engineer Certification
Udemy Link: https://www.udemy.com/course/google-cloud-gcp-professional-data-engineer-certification/

## Section 1: Introduction
Cost
- $0 - for GCP account.
- Free plan for the first 3 months. $300 for next 3 months.
- $200 for [certification](https://cloud.google.com/learn/certification/data-engineer). Length: 2 hours.

## Section 2: Data Engineering Concepts

### Data pipeline

There are 4 basic stages of data engineering pipeline:

![Data pipeline](images/section02/pipeline.png)

#### Ingest
Gather data from mutiple sources:
- From app: Event log, click stream data, e-commerce transaction,...
- Streaming ingest: PubSub.
- Batch ingest: Different transfer services, GCS - gutil,...

#### Store
Once the data is gathered, it's time to think about how to store that ingested data.
- Cost efficient & durable data storage.
- Different kinds of data need different kinds of storage.

![Data types and their services](images/section02/storage.png "Data types and their services")

Ref: https://cloud.google.com/products/databases?hl=en#store

#### Process and analyze
Once data is stored in an appropriate storage, it's time to process and analyze raw data into something meaningful via:
- BigQuery.
- ML: BigQuery ML, Spark ML with DataProc, Vertex AI.

#### Explore and visualize
Other than that, we can explore and visualize data via:
- Google Data Studio: Easy to use BI Engine (Dashboard & Visualization).
- DataLab: Interactive Jupyter Notebook that supports all data science libraries.
- ML Prebuilt API: Vision API, Speech API.

### Data type

There are 3 main kinds of data:

#### Structured data
- Tabular data.
- Represented by rows and columns.
- SQL can be used to interact with data.
- Fixed schema.
- Each row has the same number of columns.
- Relational databases are structured: MySQL, Oracle SQL, PostgreSQL, MSSQL,...
- In GCP: Cloud SQL, Cloud Spanner.

#### Semi-structured data
- Each record (row) has variable number of properties (column).
- No fixed schema.
- Flexible structure.
- NoSQL kind of data.
- JSON is the main main to represent semi-structured data.
- MongoDB, Cassandra, Redis, Neo4j.
- In GCP: BigTable, DataStore, MemoryStore.

#### Unstructured data
- No pre-define structure in data.
- Image, video,...
- In GCP: Google Cloud Storage.

### Batch Data vs Streaming Data

There are 2 main ways to process data:

#### Batching
- Data size is known.
- Processing data after certain periodic interval.
- Long time to process data.

#### Streaming
- Data size is unknown.
- Data is processed as it arrives.
- No much heavy processing - take millisecond or seccond to process data.

## Section 3: GCP Fundamentals

### Regions & zones
GCP manages their services across multiple regions (Singapore, US West, ...). Inside individual region, there are multiple zones. Region is nothing but a geographical area and zone is a data center. The concept behind the region and zonze solves some of the problems:

- Low latency
- Follow government rules
- High availability
- Disaster recovery

![Region & Zone](images/section03/region_zone.png "Region & Zone")

The naming of region and zone follow pattern: `<region>-<zone>`
E.g: `northamerica-norteast1-a` means `northamerica-norteast1` region and zone `a`.

Managed location by GCP: https://cloud.google.com/about/locations

## Section 4: GCP Basic Services

### IAM
- Identify & access management
- Who can do what on which resources
- Who: identity
- What: action: create, delete,update
- Which: resources
- Roles: collection of resources

#### Roles & Permission
- Roles are collections of permissions.
- Can assign a role to an identity, but cannot assign permission directly.
- Role can be classified into 3 categroies: primitive, pre-define, custom

![Roles Diagram](images/section04/iam_role_perm.png "Roles Diagram")

#### Service Account
- Account for none human: app, service.
- Service account keys can be used for authentication.
- Max 10 keys per service account.
- Max 100 service account per project.
- As other account types, service account can be assigned role into it.

### IAAS (Infrastructure As A Service)
- Google Compute Engine is the basic building block of any cloud.
- IAAS give full controle, more flexibility and more responsibility.
- Important params:
    - Zone
    - Service account
    - Machine family
    - Boot disk
    - Storage
    - Virtual Private Cloud

### PAAS (Platform As A Service)
- Google App Engine is PAAS solution.
- Fully managed service.
- Deploy web app at high scale.
- Serverless.
- Deploy HTTP based web application.
- Runtime supported: Go, Java, ...
- Two flavors:
    - Standard - basic runtime
    - Flexible - Docker container
- GAE features:
    - Auto scaling
    - Load balancing
    - Versioning
    - Traffic spliting
- GAE drawbacks:
    - Only one app of GAE per GCP project.
    - Once GAE app created, we cannot change its region.

### CAAS (Container As A Service)
- Kubernetes is the CAAS solution.
- Orchestration system for containerized application.
- Deploy an image to GKE :
    1. Create cluster
    2. Deploy workload (container image)
    3. Expose outside world

### Cloud Function
- Single purpose micro services
- Deploy code as function
- Event based triggerL
    - HTTP
    - Pub/sub
    - Object upload in Cloud Storage

## Section 5: Storage Products
Based on how the data is structured, there is an appropriate storage product for it.

![Storage Product 1](images/section05/storage_product_1.png)
![Storage Product 2](images/section05/storage_product_2.png)

## Section 6: Google Cloud Storage

### Instruction
- Object storage solution in GCP.
- Unstructured data storage:
    - Image
    - Video
    - Binary file, etc...
- Cloud storage can be used for long term archival storage.
- Can be access object over HTTP, Rest API,...
- No capacity planning required - scale to exabyte.
- Unlimited data can be stored.
- By default, data is encrypted.
- In transit, data is also encrypted.
- 0 <= Object size <= 5GB
- Object can be globally access.
- Single API to access accross multiple storage class.
- Data is geo-redundant (High Availability):
    - Multiregional
    - Dual-region storage

### Object Organization
- Bucket name is unique globally.
- Bucket name appears in URL -> careful while naming bucket.
- Bucket level lock with data retention policy.
- Object are immutable.
- Object can be versioned.

### Storage Location
1) Region
- Lowest latency within a single region.
- Replicated data across multiple zones in a single region.
2) Dual-region
- High availability and low latency across 2 regions (Paired region)
- Auto-failover
3) Multi-region
- Highest availability across continent area: US, AU, Asia,...
- Auto-failover

### Storage Class
Depends on data access frequency then choose the appropriate storage class. There are 3 storage classes:

1) Standard
- High frequency access (good for hot data)
- Storage cost: Highest
- Access cost: Lowest
- SLA:
    - 99.95% Multi/Dual
    - 99.9% Region

2) Nearline
- Low frequency access (once a month)
- Storage cost: High (lower than Standard class)
- Access cost: Fairly low (higher than Standard class)
- SLA:
    - 99.95% Multi/Dual
    - 99.9% Region

3) Coldline
- Very low frequency access (once a quarter)
- Storage cost: Fairly low (lower than Nearline class)
- Access cost: Fairly high (higher than Nearline class)
- SLA:
    - 99.95% Multi/Dual
    - 99.9% Region

4) Archive
- Offline data (once a year)
- Storage cost: Cheapest
- Access cost: Most expensive
- SLA: No SLA

### Object Lifecycle Management
- Based on condition, what action needs to perform on object.
- Conditions:
    - Object age
    - Object file type
    - After some specific date
- Action:
    - Transition to different storage class for high performance: from Standard to Nearline, from Coldline to Archive,...

### Secure Data With Encryption
There are 3 ways that we can do to ecrypt our data in GCS:
- Google managed encryption Keys
    - No configuration
    - Fully managed
- Customer managed encryption keys
    - Create keyring in Cloud KMS (Key Management Service)
    - Key will be managed by customer (Key rotation)
- Customer supplied encryption keys
    - We will generate key with command: `openssl rand -base64 32`
    - gsutil - encrypt with CSEK: `gsutil -o 'GSUtil:encryption_key='<openssl_key> cp <file> gs://<bucket>/<destination_path>`
    - We cannot open this file normally via browser, we must use `gsutil` with encryption key to access it: `gsutil -o 'GSUtil:encryption_key='<openssl_key> cat gs://<bucket>/<destination_path>`

### Object Versioning
- Help to prevent accidental deletion of object.
- Enable/Disable versioning at bucket level.
- Versioning are not enabled by default.
- Get access to older version with `<object_key>#<version_number>`.
- If we don't specify version numbner, always retrieve the latest version.
- If we don't need earlier version, delete it & reduce cost.
- To enable: `gsutil versioning set on gs://<bucket_name>`
- To see if the version is enabled or not: `gsutil versioning get gs://<bucket_name>`
- To list all files and see their version number: `gsutil ls -a gs://<bucket_name>`

### Access Control In GCS
- Who can do what on GCS at what level.
- There are 3 ways to grant permission into a bucket:
    - Apply at project level
        - Using IAM: storage predefined role or custom role.
    - Apply at bucket level
        - Uniform level access: apply for all objects inside bucket (no object level permission).
        - Fine grained permission: ACL (Access Control List) for each object separately.
    - Assign bucket level role
        - Select bucket & assign role to a user.

### Signed URL
- Give temporary access to user who does not have Google Account.
- URL expires after defined period of time.
- Max period for such URL is value is 7 days.
- Using command: `gsutil signurl -d 10m <SA_key_json_path> gs://<bucket_name>/<fipath>`

### Bucket Retention Policy
- Minimum duration for which bucket will be protected from:
    - Deletion
    - Modification

## Section 7: Data Transfer Service
There are 3 scenarios to use DTS:
- From on-premise to GCS.
- From GCS bucket to another GCS bucket.
- From another cloud platform to GCS bucket (S3 bucket to GCS bucket).

### On-premiseto GCS
There are 3 ways to do this:

1. `gsutil`:
2. Transfer Service for on-premise data:
    - Quickly and securely move data from private data centers into GCS.
    - Two steps process:
        1. Install an agent
        2. Create transfer job inside GCP
3. Transfer Appliance:
    - Physical device which securely transfer large amounts of data to GCP.
    - Need to request to Google.
    - When data that exceeds 20TB or would take more than a week to upload.

### Transfer Service
- This will quickly and securely transfer data into GCS.
- From various sources:
    - Amazon S3
    - Azure Blob Storage.
    - Move data between GCS buckets.
- Create Transfer job.
- Onetime run or recurring.

## Section 8: Google Block Storage & Filestore

### Block Storage
Block storage is similar to hard disk storage in PC/laptop. There are 2 kinds of block storages:
1. Direct attached storage - Local SSD
    - Physically attached to VM
    - Very high performance - 10x to 100x of persistence disk
    - Costlier than persistence disk
    - Cannot re-attached to other VM
    - Once VM destroy, locall SSD will be deleted.
    - Lower availability
    - Temporary/ephemeral storage
    - No snapshot
    - Let's see in action
2. Network attached storage
    - Persistence disk
    - Zonal, regional
    - Not attached directly to any VM
    - Can be re-attached with other VM
    - Very flexible - resize easily
    - Permanent storage
    - Snapshot supported
    - Cheaper than local SSD

### Filestore
Similar to NFS and we can manage the file sharing.
- Fully managed, high performance filestore
- Network attached storage (NAS) for Compute Engine and GKE instance
- Minimum 1TB, maximum 64TB
- Support for HDD and SSD
- Enterprise level - easy file sharing
- Costly compare to cloud storage
- Need to use `nfs-common` (`mount` command) to mannually attach to Filestore

### Which storage to use and when
- Cloud Storage
    - Unstructured data storage
    - Video stream, image
    - Binary data
    - Staging environment
    - Compliance
    - Backup
    - Data lake
- Filestore
    - Performance predictable
    - Lift-shift millions of files
- Persistent disk
    - Attach disk with VM & containers
    - Share read-only disk with multiple VM
    - Database storage
- Local disk
    - Attach disk with VM & containers
    - Temporary high performance attach disk

## Section 9: Database concepts
Learn some database related terminology from cloud perspective.

### OLTP (Online Transaction Processing)
- Simple query
- Large number of small trasactions
- Database modification
- Traditional RDMS: MySQL, PostgreSQL, Oracle, MSSQL
- GCP: Cloud SQL, Cloud Spanner

### OLAP (Online Analytical Processing)
- Data warehouse
- Data is collected from multiple sources
- Complex query
- Data analysis
- GCP: Google Big Query

### RTO vs RPO

![RTO & RPO](images/section09/rpo_rto.png)

- RTO: Recovery Time Objective
    - Maximum defined time for a system can be down
    - When a problem happens, engineering team must bring system back within RTO.
- RPO: Recovery Point Objective
    - Maximum time for an organization can tolorate data loss

### Durability
- How healthy & resilient your data is
- For example: Object Storage provider measure durability in terms of number of 9's (99.9999999%). That means that even with 1 billion objects, you would likely go a hundred years without losing a single one.

### Availability
- Data is replicated across multiple regions to gain higher availability.
- Availability is defined by SLA (Service Level Agreement).
- For example: SLA level of 99.99 % uptime/availability results in the following periods of allowed downtime/unavailability:
    - Daily: 8.6s
    - Weekly: 1m 0.48s
    - Monthly: 4m 21s
    - Quarterly: 13m 2.4s
    - Yearly: 52m 9.8s
- Ref: https://uptime.is/
