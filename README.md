# CST8917Assignment2 - Serverless Applications

## Assignment2 - Serverless Service ALternatives Report

---

## Introduction
This document will analyze the comparison of  Microsoft Azure serverless services studied in this course with their closest equivalents in Amazon Web Services (AWS) and Google Cloud Platform (GCP).  
For each service, we provide:

- **Overview** – brief description of each service
- **Core Features** – supported triggers, bindings, messaging/eventing capabilities
- **Integration Options** – how it works with other cloud services or CI/CD pipelines
- **Monitoring & Observability** – available tools/logging integrations
- **Pricing Model** – high-level cost considerations
- **Strengths & Weaknesses** – from a serverless architecture perspective

---

## 1. Azure Functions

Azure Functions is a serverless compute service for running event-driven code without managing infrastructure.

| Azure Service   | AWS Equivalent | GCP Equivalent   |
|-----------------|---------------|------------------|
| Azure Functions | AWS Lambda    | Cloud Functions  |

### Comparison Table
| Feature / Capability | Azure Functions | AWS Lambda | GCP Cloud Functions |
|----------------------|-----------------|------------|----------------------|
| **Triggers**         | HTTP, Timer, Blob, Queue, Event Grid, Event Hub, Service Bus, Cosmos DB | API Gateway, S3, DynamoDB Streams, SQS, EventBridge, Kinesis | HTTP, Pub/Sub, Cloud Storage, Firestore, Firebase events |
| **Bindings**         | Rich input/output bindings for many Azure services | No native bindings (integrations via SDK/events) | No native bindings (Pub/Sub + SDKs) |
| **Languages**        | C#, JavaScript, Python, Java, PowerShell, Go (preview) | Node.js, Python, Java, Go, .NET, Ruby, Custom Runtime | Node.js, Python, Go, Java, .NET, Ruby |
| **Scaling**          | Consumption, Premium, App Service plan | Auto-scale per request | Auto-scale per request |
| **Integration**      | Deep with Azure ecosystem, CI/CD via Azure DevOps & GitHub Actions | Deep with AWS ecosystem, CI/CD via CodePipeline & CodeBuild | Deep with GCP ecosystem, CI/CD via Cloud Build |
| **Monitoring**       | Azure Monitor, Application Insights | CloudWatch, X-Ray | Cloud Monitoring, Trace, Error Reporting |
| **Pricing**          | Per execution + execution time | Per execution + execution time | Per execution + execution time |

### Analysis
Azure Functions offers the richest binding model, minimizing glue code. AWS Lambda supports the broadest range of event sources but requires more setup for cross-service integration. GCP Cloud Functions is the simplest to use, especially with Firebase or AI/ML integrations.

---

## 2. Durable Functions

Durable Functions extends Azure Functions for long-running workflows, state management, and orchestration.

| Azure Service     | AWS Equivalent       | GCP Equivalent |
|-------------------|----------------------|----------------|
| Durable Functions | AWS Step Functions   | GCP Workflows  |

### Comparison Table
| Feature / Capability | Durable Functions | AWS Step Functions | GCP Workflows |
|----------------------|-------------------|--------------------|---------------|
| **Workflow Models**  | Function chaining, fan-out/fan-in, async HTTP APIs | Sequential, parallel, branching workflows | Sequential workflows, conditional branching |
| **State Management** | Built-in with Azure Storage | Built-in | Built-in |
| **Triggers**         | Any Azure Function trigger | Any Lambda trigger | HTTP / Pub/Sub triggers |
| **Integration**      | Native with Azure Functions | Native with AWS Lambda, ECS, Fargate, Batch | Native with Cloud Functions, Cloud Run |
| **Monitoring**       | Application Insights | CloudWatch | Cloud Logging |
| **Pricing**          | Based on executions and storage transactions | Based on state transitions | Based on execution steps |

### Analysis
Durable Functions feels more like “code with orchestration features,” while Step Functions and Workflows are more declarative. AWS Step Functions are ideal for highly complex workflows. GCP Workflows is simpler but less feature-rich than the other two.

---

## 3. Azure Logic Apps

Azure Logic Apps is a low-code integration and workflow automation platform.

| Azure Service  | AWS Equivalent       | GCP Equivalent |
|----------------|----------------------|----------------|
| Logic Apps     | AWS Step Functions (Express) / EventBridge Scheduler | GCP Workflows / Cloud Composer |

### Comparison Table
| Feature / Capability | Logic Apps | AWS Step Functions (Express) | GCP Workflows |
|----------------------|------------|------------------------------|---------------|
| **Triggers**         | 400+ connectors, HTTP, timers | API Gateway, EventBridge, SQS, SNS | HTTP, Pub/Sub |
| **Integrations**     | Office 365, Dynamics, SAP, Salesforce | AWS services, SaaS via API Gateway | GCP services, limited SaaS connectors |
| **Development**      | Visual designer in Azure Portal | JSON/YAML definition | YAML definition |
| **Monitoring**       | Azure Monitor | CloudWatch | Cloud Logging |
| **Pricing**          | Per action execution | Per state transition | Per step execution |

### Analysis
Logic Apps leads in ready-to-use SaaS connectors. AWS and GCP equivalents require more manual API integration but may offer better control for custom architectures.

---

## 4. Azure Service Bus (Queues & Topics)

Azure Service Bus is a fully managed enterprise messaging service supporting queues (point-to-point) and topics (pub/sub).

| Azure Service     | AWS Equivalent | GCP Equivalent |
|-------------------|----------------|----------------|
| Service Bus       | Amazon SQS & SNS | Pub/Sub        |

### Comparison Table
| Feature / Capability | Azure Service Bus | AWS SQS & SNS | GCP Pub/Sub |
|----------------------|-------------------|---------------|-------------|
| **Messaging Model**  | Queues (P2P), Topics (Pub/Sub) | SQS (P2P), SNS (Pub/Sub) | Pub/Sub only |
| **Ordering**         | FIFO queues | FIFO queues (SQS), ordering for SNS | Ordering keys |
| **Dead-letter**      | Supported | Supported | Supported |
| **Protocols**        | AMQP, HTTPS | HTTPS | HTTPS, gRPC |
| **Integration**      | Azure Functions, Logic Apps | Lambda, EventBridge | Cloud Functions, Dataflow |
| **Pricing**          | Per operation, message size | Per request, message size | Per message volume |

### Analysis
Azure Service Bus is feature-rich for enterprise integration (sessions, transactions). AWS splits this into two services. GCP Pub/Sub is highly scalable but simpler in feature set.

---

## 5. Azure Event Grid

Azure Event Grid is a fully managed event routing service for building event-driven architectures.

| Azure Service | AWS Equivalent | GCP Equivalent |
|---------------|----------------|----------------|
| Event Grid    | Amazon EventBridge | Eventarc       |

### Comparison Table
| Feature / Capability | Event Grid | EventBridge | Eventarc |
|----------------------|------------|-------------|----------|
| **Event Sources**    | Azure services, custom topics | AWS services, custom apps | GCP services, custom events |
| **Delivery Model**   | Push (HTTP) | Push (HTTP), target AWS services | Push (HTTP), Pub/Sub |
| **Filtering**        | Advanced attribute-based filtering | Pattern-based filtering | Attribute filtering |
| **Retries**          | Yes | Yes | Yes |
| **Integration**      | Functions, Logic Apps, Service Bus | Lambda, Step Functions | Cloud Functions, Workflows |
| **Pricing**          | Per event | Per event | Per event |

### Analysis
All three offer similar event routing capabilities, but Event Grid stands out for integration with Azure security/compliance events, EventBridge for cross-account AWS integrations, and Eventarc for GCP's simple link with Cloud Run.

---

## 6. Azure Event Hubs

Azure Event Hubs is a big data streaming platform and event ingestion service.

| Azure Service | AWS Equivalent     | GCP Equivalent |
|---------------|--------------------|----------------|
| Event Hubs    | Amazon Kinesis Data Streams | Pub/Sub        |

### Comparison Table
| Feature / Capability | Event Hubs | Kinesis Data Streams | Pub/Sub |
|----------------------|------------|----------------------|---------|
| **Use Case**         | Large-scale event ingestion | Real-time data streaming | Pub/Sub messaging and streaming |
| **Throughput**       | Millions of events/sec | Millions of events/sec | Millions of events/sec |
| **Retention**        | Up to 7 days (standard), 90 days (dedicated) | Up to 7 days | Up to 7 days |
| **Partitioning**     | Yes | Yes | Yes |
| **Integration**      | Stream Analytics, Functions, HDInsight | Lambda, Analytics, Firehose | Dataflow, Functions |
| **Pricing**          | Throughput units | Shards | Data volume & retention |

### Analysis
Event Hubs and Kinesis are nearly identical in capabilities and architecture. GCP Pub/Sub can handle both pub/sub messaging and streaming but lacks some advanced partitioning metrics.

---

## Conclusion
While Azure, AWS, and GCP all provide equivalent serverless components, their **strengths differ**:
- **Azure**: Best for rapid integration via bindings and prebuilt connectors.
- **AWS**: Most mature, broadest service ecosystem for event-driven systems.
- **GCP**: Simplest to adopt, strongest ties to data analytics and AI.

The choice often depends on **existing cloud commitments**, **integration needs**, and **developer skillsets**.
