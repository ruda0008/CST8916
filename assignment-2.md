# Cloud Service Providers Comparison Report
## AWS vs Azure vs GCP: Real-Time and Remote Data Applications


### Summary
 Amazon Web Services (AWS), Microsoft Azure, and Google Cloud Platform (GCP), three of the top cloud service providers, are thoroughly compared in this research with an emphasis on their capacities for remote data and real-time applications.  The investigation looks at WebSocket implementations, GraphQL support, RESTful API services, data streaming platforms, and stream analytics solutions.

With services like API Gateway, Amazon Kinesis, and other third-party connectors, AWS provides the most developed and extensive ecosystem, according to key results.  Azure's robust Azure API Management and Azure Stream Analytics services make it an excellent choice for enterprise integration scenarios, especially for companies that have already made an investment in the Microsoft ecosystem.  GCP sets itself apart with competitive pricing structures that support high-volume operations and enhanced data analytics capabilities with BigQuery and Pub/Sub.

For general-purpose real-time applications requiring maximum flexibility and third-party tool support, AWS emerges as the recommended choice. Azure is optimal for enterprise scenarios with existing Microsoft infrastructure investments. GCP is particularly well-suited for data-intensive applications requiring advanced analytics and machine learning integration. The choice ultimately depends on specific use case requirements, existing infrastructure, development team expertise, and long-term scalability needs.


## 2. Introduction 


Real-time communication and ultra-low latency distant data access are becoming more and more necessary in the architecture of contemporary applications, which are fueled by mobile computing, IoT devices, and dynamic user interfaces.  Cloud service providers have been forced by this requirement to create specialized services that go beyond conventional compute and storage.

 This report's **purpose** is to compare the service levels of Google Cloud Platform (GCP), Microsoft Azure, and Amazon Web Services (AWS) in  key areas that support real-time applications.  The **scope** is restricted to managed services that concentrate on backend data flow services (streaming and analytics) and client-facing API protocols (REST, GraphQL, WebSockets).

* **AWS:** The market leader, known for its extensive depth, global reach, and highly specialized services that cater to nearly every imaginable workload.
* **Azure:** A strong competitor, focused on large enterprise customers, seamless integration with Microsoft’s software ecosystem, and hybrid cloud solutions (via Azure Arc).
* **GCP:** Known for its prowess in data analytics, AI/ML, and providing serverless infrastructure based on Google’s internal technologies for massive scale and reliability.



## 3. Service Comparison



### a) RESTful API Services 

| Feature | AWS | Azure | GCP |
| :--- | :--- | :--- | :--- |
| **API Gateway Service** | Amazon API Gateway | Azure API Management (APIM) | GCP Cloud Endpoints / Apigee |
| **Pricing Model** | Usage-based (per call + data transfer out). Lower-cost HTTP APIs available. | Tiered based on provisioned units (Developer, Basic, Standard, Premium), plus Consumption for lower tiers. | Primarily consumption-based for Cloud Endpoints. Apigee offers high-end subscription tiers. |
 **Pricing (per million calls)** | REST: $3.50<br>HTTP: $1.00 | Consumption: $3.50/million <br>Developer: $49/month base<br>Basic: $144/month base | $3.00<br>(First 2M free/month) |
| **Management Tools** | CloudWatch, X-Ray, WAF | Monitor, App Insights, Policy | Cloud Monitoring, Logging, Trace |


### b) GraphQL Services 
| Feature | AWS | Azure | GCP |
| :--- | :--- | :--- | :--- |
| **Native GraphQL Support** | **AWS AppSync** (Fully managed, serverless GraphQL runtime). |  Limited via Functions/App Service | Limited via Cloud Run/Functions |
| **Third-Party Integration** | Can integrate Apollo SHasura, Prisma | **Apollo Server** is the standard approach, hosted on Azure Container Apps or AKS, and Hasura, Prisma. | **Apollo Server** is the standard approach, hosted on Cloud Run or GKE, and Hasura, StepZen |

### c) WebSocket Services 

| Feature | AWS | Azure | GCP |
| :--- | :--- | :--- | :--- |
| **Primary Service** | API Gateway (WebSocket APIs) or AWS AppSync. | **Azure Web PubSub** / Azure SignalR Service. |Firebase Realtime Database + Firestore |
| **Scalability** | Auto-managed scaling via API Gateway/AppSync; handles millions of concurrent connections. | Handles scaling and connection state up to 100,000+ connections, decoupling it from application logic. | Automatic (Firebase) |

### d) Data Streaming Services 

| Feature | AWS | Azure | GCP |
| :--- | :--- | :--- | :--- |
| **Streaming Platform** | **Amazon Kinesis Data Streams** | **Azure Event Hubs** | **GCP Cloud Pub/Sub** |
| **Data Model** | Sharded log-based stream (Requires shard management). | Partitioned event log (uses Throughput Units (TUs) for scaling). | Global topic/subscription model (Fully decoupled asynchronous messaging). |
| **Data Ingestion** | Kinesis Firehose (Managed delivery to S3/Redshift) or SDKs to shards. | SDKs, Kafka APIs (strong Kafka compatibility), Event Grid. | SDKs, REST/gRPC APIs, seamless integration with Cloud Functions/Run. |


### e) Stream Analytics 

| Feature | AWS | Azure | GCP |
| :--- | :--- | :--- | :--- |
| **Analytics Platform** | **AWS Kinesis Data Analytics** (Apache Flink) | **Azure Stream Analytics (ASA)** | **GCP Dataflow** (Apache Beam) |
| **Processing** | Streaming SQL, Java/Scala (Flink). | Streaming SQL (ASA Query Language). | Unified batch and stream processing (Apache Beam). |





## 4. Use Case Analysis
### Use Case 1: Real-Time Chat Application

**Scenario:**
A startup is building a mobile chat application for 5,000 users with the following requirements:
- Real-time messaging between users
- Online/offline status indicators
- Message history storage
- Push notifications
- Simple REST API for user profiles
- Budget-conscious solution

**Recommended CSP: GCP (Firebase)**

**Justification:**

1. **Simplicity:** Firebase provides an all-in-one solution with Firestore for real-time data sync, Firebase Authentication for user management, and Cloud Functions for backend logic. No need to manage separate services.

2. **Cost Analysis:**
   - **Firestore:** 
     - Storage: 5,000 users × 100 messages/user × 2KB = ~1 GB = $0.18/month
     - Reads: 5,000 users × 50 messages viewed/day × 30 days = 7.5M reads = $4.50/month
     - Writes: 5,000 users × 10 messages sent/day × 30 days = 1.5M writes = $2.70/month
   - **Cloud Functions:** ~$10/month for notification triggers
   - **Total: ~$17.38/month**

3. **Real-Time Sync:** Firestore automatically syncs data across all connected clients via WebSocket. No manual WebSocket management needed.

4. **Offline Support:** Built-in offline persistence means users can read messages without internet connection.

5. **Mobile SDKs:** Firebase has excellent iOS and Android SDKs that handle authentication, data sync, and push notifications out of the box.




---

### Use Case 2: E-Commerce Product Catalog API

**Scenario:**
An online retailer needs to expose their product catalog to mobile apps and third-party developers:
- 50,000 products in database
- REST API for product search, filtering, and details
- 1 million API calls per month
- Need rate limiting and API key management
- Must integrate with existing SQL database
- Require developer documentation portal

**Recommended CSP: Azure**

**Justification:**

1. **API Management Features:** Azure API Management includes a built-in developer portal with interactive documentation, making it easy for third-party developers to understand and use the API.

2. **Cost Analysis:**
   - **API Management (Consumption Tier):** 
     - API calls: 1M × $3.50/million = $3.50/month
     - Data transfer: ~10 GB × $0.50/GB = $5/month
   - **Azure SQL Database (Basic):** $5/month
   - **Total: ~$13.50/month**

3. **Policy-Based Control:** Azure's policy engine makes it simple to implement rate limiting, quota management, and API key validation without writing code.

4. **Database Integration:** Native integration with Azure SQL Database. The existing SQL database can be migrated easily, and API Management can connect directly.

5. **Developer Experience:** The automatic API documentation portal saves development time and provides a professional interface for API consumers.





**Why Azure Wins:**
- Built-in developer portal (AWS/GCP require custom solution)
- Better policy management for rate limiting
- Competitive pricing with superior features
- Easier migration from existing SQL databases


---

## Conclusion


While each cloud service provider has unique advantages, they all have strong capabilities for real-time applications and remote data access:

 In terms of enterprise-grade features, ecosystem breadth, and maturity, **AWS** leads.  For mission-critical applications that need significant third-party integrations, proven dependability, and thorough compliance certifications, it's the ideal option.  AWS is perfect for intricate real-time infrastructures because of its configurable Kinesis suite and managed GraphQL service (AppSync).

 For businesses that already use Microsoft products, **Azure** offers great value and performs exceptionally well in hybrid cloud environments.  Its SignalR Service makes WebSocket implementations easier, and its API Management service provides better policy-based control.  Azure's flexibility enables custom implementations integrated with enterprise Active Directory, despite the lack of native GraphQL support.

The most affordable options for data-intensive tasks with excellent analytics capabilities are provided by **GCP**.  Operational complexity is eliminated by Pub/Sub's automated scaling and BigQuery's performance.  Although GraphQL and WebSockets require additional self-managed components, GCP is appealing to startups and data-driven apps due to its developer-friendly tools and low pricing.

### Overall Recommendations
**Cloud platform should be chosen based on requirements such as follows:**

**AWS:**
- Building financial services, healthcare, or highly regulated applications
- Requiring the most mature ecosystem and broadest service catalog
- Need native GraphQL with real-time subscriptions
- Prioritizing proven reliability over cost optimization

**Azure:**
- Already invested in Microsoft enterprise technologies
- Requiring hybrid cloud capabilities
- Need strong developer portal and API documentation features
- Prioritizing enterprise integration and Active Directory

**GCP:**
- Building data analytics or machine learning-driven applications
- Cost optimization is a primary concern
- Team has strong data engineering capabilities
- Comfortable with container-based architectures and Apache Beam

**Multi-Cloud:** For large organizations, a hybrid approach leveraging each provider's strengths can optimize both cost and capabilities—for example, using AWS for customer-facing APIs, GCP for backend analytics, and Azure for enterprise integration.


## AI Usage Disclosure

 Claude AI (Anthropic) was  used to improve the structure and presentation of this research. Specifically, AI assisted in organizing the findings according to the assignment's required format  enhancing the professional tone and clarity of technical explanations, and formatting comparison data into comprehensive tables for easier analysis. AI also helped with the use case scenarios. 



## References


Graphql | decision guide to graphql implementation | amazon web services. (n.d.). https://aws.amazon.com/graphql/guide/  

AWS AppSync documentation. (n.d.-a). https://docs.aws.amazon.com/appsync/  

What to consider when modernizing apis with graphql on AWS | AWS Architecture Blog. (n.d.-c). https://aws.amazon.com/blogs/architecture/what-to-consider-when-modernizing-apis-with-graphql-on-aws/ 

Gaikwad, J. (2025). AWS Kinesis vs azure event hub vs google pub/sub for stream processing. Branch Boston. https://branchboston.com/aws-kinesis-vs-azure-event-hub-vs-google-pub-sub-for-stream-processing/ 

API management pricing. Microsoft Azure. (n.d.). https://azure.microsoft.com/en-ca/pricing/details/api-management/ 

Google. (n.d.). Firebase realtime database. Google. https://firebase.google.com/docs/database 

Google. (n.d.-a). BigQuery documentation  |  google cloud documentation. Google. https://docs.cloud.google.com/bigquery/docs 

Google. (n.d.-b). Compare AWS and Azure Services to Google Cloud  |  get started  |  google cloud documentation. Google. https://docs.cloud.google.com/docs/get-started/aws-azure-gcp-service-comparison 

Azure (n.d.). Azure event hubs documentation. Microsoft Learn. https://learn.microsoft.com/en-us/azure/event-hubs/ 

- https://cloud.google.com/products/calculator
- https://azure.microsoft.com/pricing/calculator/ 
- https://calculator.aws/ 
