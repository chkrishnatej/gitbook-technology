# SQL vs NoSQL

Applications which are generally available are multi-tenant applications. Which means there are multiple layers.

![N-tier architecture](<../.gitbook/assets/image (3).png>)

Scaling of a service depends on how fast and cheap it's easier to scale the logical tier and data tier. The logical tier which generally resides behind a Load Balancer, can be horizontally scaled by adding more server to serve the requests.

But after a point of time, the scaling of service becomes a bottle neck at the Data tier. It is because the number of varieties of queries that needs to be served, large load of data writes  that the data tier needs to cope up with becomes a bottle neck for scaling a service.&#x20;

**SQL:** Schema updates are very slow when you get bigger. Adding a column to 10 million rows takes locks and doesn’t work.

**NoSQL:** There is no defined schema as such, so it is easier to scale out when you want to add a new column.

### From usage point of view basically when using DB in application code:

#### SQL

SQL databases are particularly very good for when we have well-defined entities. For example, when we take a **money transaction,** it is generally a well-defined entity. And the properties of when the transaction should/shouldn't happen are also well-defined.&#x20;

A transaction can be made,&#x20;

* when there is a valid receiver account
* there account balance >= amount that needs to be sent

#### NoSQL

NoSQL databases are particularly good when the schema is loosely defined. For example, we are trying to build a CRM system. When we want to capture the customers interaction, it cannot be a one size fits. There could be a case where we need to introduce a new field quickly without having downtime. When there is a lot of data, and downtime is a no-go, that's when NoSQL databases shine.

Let's say a lot of customers requested a feature where they want to add new email-ids for interaction so that they can be informed of the updates. In a NoSQL database, this is easier as the data validation won't be done on the DB level before writing to it.

When the dimensionality of data changes rapidly or the app shipments needs to be quick, NoSQL is a better choice to go with.

### From read/write performance point of view

#### SQL

SQL has a lot of data and schema validation before a row is inserted/updated. This is to ensure that all the data which is inserted is always sane. Although this adds overhead, for critical applications, having this overhead is well worth it.&#x20;

For example, take a case of banking transaction, the constraint and type checks are beneficial so that the customers do not lose money.&#x20;

#### News App

When we are developing a read-heavy system, for example, a news website, there could be 100's of editors who continuously update or adds new articles. Still, there could be millions of users who read the articles. And the queries are much more well-defined. Like&#x20;

* Searching for an article with the title
* Searching for articles of author
* Searching for articles of a particular category

SQL excels at this kind of things when the entities are well-defined and need to be retrieved.

#### NoSQL

NoSQL is dynamic in nature.&#x20;

#### Building log aggregator web app

A log aggregator is a write-heavy service, and there is no specified schema around it. Based on the application needs, a new field can be introduced and not be used. In such kind of cases, there is no need to do a lot of schema and constraint checks when a log needs to be written. NoSQL gives this flexibility. And due to the no overhead of checking constraints and normalising the data, the writes are generally faster.&#x20;

### How queries and joins affect the performance of an application&#x20;

#### Building Kubernetes management web app

We are building a web app to help users manage their Kubernetes deployment. Kubernetes, as we know, considers all resources like deployments, ingress, storage, and secrets are **deeply nested datasets.** Let's assume the nested dataset is in **JSON** format

&#x20;**** This application can be built using both SQL and NoSQL databases. Let's try to compare how it would look in both cases:

#### SQL

As we talk, we know many popular SQL database offerings support nested JSON objects. Using that, let's try to build the application.

Consider every deployment (which includes deployment, service, storage, and secrets) can be tracked with a unique identifier. That is stored in relational DB. Let's consider we maintain one table for each entity of Kubernetes.

* Workloads
  * Deployment/ReplicaSet
  * Job/Cron Job
  * Daemonset
  * Statefulset
* Storage
  * PVC
  * NAS
  * ...
* Networking
  * Load Balancer
  * ClusterIp
  * NodePort
  * Ingress

These are some of the main components of Kubernetes and the sub-divisions. Let's consider there are around ten tables.&#x20;

#### WRITES

For every deployment, we need to make sure all the related resource table needs to be updated with the required data for the customers to keep track of the deployments. If we consider there is a type defined for every field(including nested fields), just the sheer amount of constraint checking to insert the data might make the application slower.&#x20;

#### READS

Suppose the user want's to query these resources using deployment id(which was unique). Since all these data resides in different tables, we need to use <mark style="color:orange;">**JOINS**</mark> to aggregate the data to bring it to user. This along with the deeply nested dataset each and every table stores, if we wanted to query it and return the result, is such as costly operation and performance of the application also takes a hit.&#x20;

In these scenarios, users can ingest JSON data without conversion to SQL fields, **but take a performance hit when querying the data because these columns support minimal indexing at best.**

#### **NoSQL**

In NoSQL, let's say we store all the resources related to deployment in document like JSON.&#x20;

When the user needs to query in that deployment or few number of deployments, it is easier to apply filter as the data access pattern, allows for giving the information efficiently using NoSQL database.&#x20;
