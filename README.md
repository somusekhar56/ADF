# ADF
# 1. Key Features and Services
# 1.1 Global Data Centers
Azure operates a global network of data centers distributed across multiple regions worldwide.

# Key Points
Regions are geographically isolated

Each region contains one or more data centers

Supports data residency and compliance requirements
# Benefits
Low latency access

High availability

Disaster recovery

Global scalability
# Examples:

Central India

East US

West Europe
# 1.2 Azure Subscription and Resource Groups
# What is an Azure Subscription?
An Azure Subscription is a billing and access boundary in Azure.

# A subscription:

Tracks usage and billing

Controls access via RBAC

Contains multiple resource groups

# 1.2.1 Creating Azure Subscription
# Ways to create a subscription:

Azure Portal

Azure Free Account

Enterprise Agreement (EA)

Pay-As-You-Go
# Basic steps:

Sign in to Azure Portal

Go to Subscriptions

Click Add

Choose subscription type

Complete payment setup
# 1.2.2 Managing Resources in Resource Groups
Resource Groups

Logical containers for Azure resources

Resources share lifecycle
# Example:

Resource Group: prod-rg
 ├── Virtual Machine
 ├── Storage Account
 ├── Virtual Network
# Management Operations:

# Create / Delete
Move resources between RGs

Apply tags for cost management

Set RBAC permissions
# 1.3 Azure Workspace and UI
Azure provides multiple interfaces to manage resources.

# 1.3.1 Navigating the Azure Portal
Azure Portal is a web-based GUI for managing Azure resources.

# Key sections:

Home

Dashboard

All services

Resource groups

Subscriptions
# Capabilities:

Create resources

Monitor performance

Configure security
# 1.3.2 Overview of Dashboard and Resource Management
Dashboard

Customizable view

Pin frequently used resources

Monitor metrics & alerts

Resource Management

Create / update / delete resources

Monitor usage

Apply policies
# 1.3.3 Azure CLI and PowerShell
Azure supports command-line management for automation and scripting.

Tool	Platform

Azure CLI	Cross-platform

PowerShell	Windows & Cross-platform
# 1.3.4 Command-Line Interface Options for Azure
Azure CLI

Uses az commands

Works on Windows, Linux, macOS
# Example:

az login

az group create --name myRG --location centralindia
# 1.3.5 Scripting with PowerShell
Azure PowerShell uses cmdlets.

# Example:

Connect-AzAccount

New-AzResourceGroup -Name myRG -Location "Central India"
# Why Use PowerShell?
Automation

Repeatable deployments

Infrastructure as Code support

Why These Azure Features Matter

Simplified cloud management

Centralized billing and access control

Multiple management interfaces

Enterprise-ready governance


# 1.4 Azure Storage Account (Types)
An Azure Storage Account provides a unique namespace to store data objects in Azure.

A single storage account can host multiple storage services.

# 1.4.1 Blob Storage
Azure Blob Storage is used to store unstructured data.

# What it stores
Text files

Images

Videos

Backups

Big data files

Use Cases

Data lakes

Media content

Log storage

Blob Types

Block Blob – Most common (CSV, JSON, Parquet)

Append Blob – Logs

Page Blob – VHD disks
# 1.4.2 File Storage
Azure File Storage provides file shares in the cloud.

# Features
SMB & NFS support

Mountable like a network drive

# Use Cases
Lift-and-shift applications

Shared file systems

Application configuration storage
# 1.4.3 Table Storage
Azure Table Storage is a NoSQL key-value store.

Characteristics

Schema-less

Highly scalable

Low latency
# Use Cases
Metadata storage

User profiles

IoT data
# 1.4.4 Queue Storage
Azure Queue Storage is a message queue service.

# Features
Stores large numbers of messages

Asynchronous communication
# Use Cases
Decoupling applications

Background processing

Event-driven workflows
# 1.5 Azure Data Factory (ADF)
Azure Data Factory is a cloud-based ETL/ELT service used for data integration.

# Introduction to ADF
ADF allows you to:

Ingest data from multiple sources

Transform data

Load data into target systems
# It supports:

Batch processing

Incremental loads

Hybrid data integration (on-prem + cloud)
# Key Components of ADF
# 🔹 Pipelines
A pipeline is a logical container for activities.

# Example pipeline:

Copy Activity → Data Flow → Sink
# 🔹 Datasets
Datasets represent the data structure used by activities.

# Examples:

Azure Blob Dataset

Azure SQL Dataset

ADLS Gen2 Dataset
# 🔹 Linked Services
Linked Services define connection information.

# Examples:

Azure Blob Storage linked service

Azure SQL linked service

Azure Databricks linked service

# 1.6. Azure Key Vault
Used to securely store sensitive information like passwords, API keys, and certificates.

# Real Scenario:
ADF pipelines use Key Vault to retrieve SQL credentials securely without exposing them.

# 🔗 4. Integration with Azure Services
# 4.1 Datasets & Linked Services
Datasets reference data, while Linked Services define connections.

# 4.2 Integration Runtime (IR)
| Type                | Purpose                                                         |
| ------------------- | --------------------------------------------------------------- |
| **Azure IR**        | Used for cloud-to-cloud data movement                           |
| **Self-Hosted IR**  | Used for on-premises to cloud data movement                     |
| **Managed VNet IR** | Used for secure data movement in restricted or private networks |

# 4.3 Triggers & Monitoring
ADF supports Scheduling, Event-based triggers, and monitoring through the Azure portal with alerts.
# Real Scenario:
A file arriving in Blob Storage automatically triggers a pipeline using event triggers.

#  Activities in Azure Data Factory (ADF)
Activities in ADF define what action should be performed. There are three major types:

Data Movement Activities

Execution Control Activities

Control Flow Activities
# 1.1 Data Movement Activities
Used to move data between supported sources and destinations using Copy Activity.

# 1.1.1 Azure Blob Storage Source/Sink:
Scenario	   Example
Source	     Read CSV files from Blob Storage and copy to SQL Database
Sink	       Store transformed files from SQL/Databricks back to Blob for storage layer
# Example use case:

Source: raw/customer_data.csv in Blob → Sink: Azure SQL dbo.Customers

# 1.1.2 Azure SQL Database Source/Sink:
Used when SQL Database is either the source or destination.

# Real Example:

Copy incremental sales data from SQL and store into ADLS Gen2 for reporting.

# 1.2 Execution Control Activities
These help control the workflow logic and orchestration.
# 1.2.1 Execute Pipeline Activity:
Used to run a pipeline from another pipeline.
Example:
Master Pipeline → Executes pipeline to copy raw → Executes pipeline for validation → Executes data transformation.
# 1.2.2 If Condition Activity:
Executes logic based on true/false output.
Real Scenario:
If today's file exists → proceed with load, else send failure notification.
# 1.2.3 ForEach Activity:
Loops through a collection of items.
# Example:
Iterate through multiple folders/files: jan, feb, mar and load data.
# 1.2.4 Web Activity:
Calls REST API endpoint.
# Use Case:
Trigger Databricks job or external API before/after pipeline run.
# 1.3 Control Flow Activities
These activities control pipeline structure and behaviour.
# 1.3.1 Wait Activity:
Pauses execution for a given time.
# Example: Wait 5 mins before retrying external API.
# 1.3.2 Until Activity:
Loops until a logical condition becomes true.
# Example: Continue checking file arrival every 10 mins until file exists.
# 1.3.3 Get Metadata Activity:
Fetch metadata like file size, existence, folder count.
# Real Case: Check if today's file exists in storage.
# 1.3.4 Lookup Activity:
Fetch single row from a data store.

Example: Lookup valid file date or expected record count.
# 1.3.5 Stored Procedure Activity:
Runs stored procedure in SQL.
# Use Case:
After data load, execute stored procedure for cleansing or merge operation.
# 1.4 Pipelines and Triggers
Pipelines are containers of activities.

Triggers schedule and execute pipelines.

| **Trigger Type**    | **Use Case**                                                                                         |
| ------------------- | ---------------------------------------------------------------------------------------------------- |
| **Schedule**        | Run pipelines on a fixed schedule, e.g., every day at 1 AM                                           |
| **Tumbling Window** | Process data in fixed time slices, e.g., hourly or daily batch logs                                  |
| **Event Trigger**   | Start pipeline automatically when a specific event occurs, e.g., a new file arrives in Azure Storage |



