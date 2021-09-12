---
layout: page
title: AWS Developer Associate Certification
permalink: /AWS-DA-Certification/
parent: Miscellaneous
nav_order: 10
---

# This is AWS Developer Associate Certification

![AWS DA Certification](https://d1.awsstatic.com/training-and-certification/Certification%20Badges/AWS-Certified_Developer_Associate_512x512.6d5f0ad35de66966c96f8e408e4fd919c1a2d753.png)

## DynamoDB

1. **Introduction**

DynamoDB is a fast and flexible nonrelational database service for any scale.
Every item must have a **Primary Key** which will uniquely identify that row (two items may not contain the same Primary Key). At a minimum when you create a table you must choose an attribute to be the **Partition Key** (aka the **Hash Key**) and you can optionally specify another attribute to be the **Sort Key**.

**Recommendations for partition keys**

- **Use high-cardinality attributes**. These attributes have distinct values for each item, like e-mailid, employee_no, customerid, sessionid, orderid, and so on.

- **Use composite attributes**. Try to combine more than on attribute to form a unique key, if that meets your access pattern. For example, consider an orders table with customerid+productis+countrycode as the partition key and order_date as the sort key.

2. **DynamoDB Accelerator (DAX)**

DAX is a DynamoDB-compatible caching service that enables you to benefit from fast in-memory performance for demanding applications. DAX addresses three core scenarios:
    1 - As an in-memory cache, DAX reduces the response times of eventually consistent read workloads by an order of magnitude from single-digit milliseconds to microseconds.

    2 - DAX reduces operational and application complexity by providing a managed service that is API-compatible with DynamoDB. Therefore, it requires only minimal functional changes to use with an existing application.

    3 - For read-heavy or bursty workloads, DAX provides increased throughput and potential operational cost savings by reducing the need to overprovision read capacity units. This is especially beneficial for applications that require repeated reads for individual keys

3. **DynamoDB Time to Live (TTL)**

TTL for DynamoDB allows you to define when items in a table expire, so that they can be automatically deleted from the database.

[Expiring Items By Using DynamoDB Time to Live (TTL)](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/TTL.html)

4. **Read/Write Capacity**

- On-Demand

- Provisioned mode: If you choose provisioned mode, you specify the number of reads and writes per second that you requiere for your application. Provisioned mode is a good options if **you have predicable app. traffic**, **you run apps whose traffic is consictend or ramps gradually** or **you can forecast capacity requirements to control costs**.

    - One read capacity unit (RCU) represents one consistent read per second or two eventually consistent reads per second for any item up to 4 KB in size.
    Transactional reads requires two RCU to perform one read per second for items up to 4 KB.
    - One write capacity unit (WCU) represents one write per second for an item up to 1 KB size. 
    Transactional writes require 2 write capacity unites to perdorm one write per second for items up to 1kb.

For example, if your data is going to be read at a rate of 300 items every 30 seconds. Each item is 6 KB size and the reads can be eventual consistent reads. What would be the Read Capacity Unit (RCU) that needs to be set to the table?

I will have 300 reads ecery 30 seconds. 300/30 = 10 items read per second. Because the item is 6KB, I will need 2 eventual consistend reads per seconds which is equal to 1 RCU.

1 RCU = 2 eventual consistend reads 

Answer, I will need 10 RCU's.

Another example, if you are writing 10 items every second, where each item is 15.5 KB in size. What would be the requiered provisioned write thoruhgput for best performance?

One WCU represents one write per second for an item up to 1 KB size. Here, we are writing 10 items per second. However, each item is 15.5 KB in size. It means that we need 16 WCU per the Items 10 --> 16 x 10 = 160 WCU.

[Read/Write Capacity Mode](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadWriteCapacityMode.html)

## Lambda

1. **Introduction**

https://aws.amazon.com/blogs/compute/sharing-secrets-with-aws-lambda-using-aws-systems-manager-parameter-store/

## API Gateway

1. **Links to read**

https://aws.amazon.com/premiumsupport/knowledge-center/api-gateway-cors-errors/

https://aws.amazon.com/blogs/aws/new-usage-plans-for-amazon-api-gateway/

https://aws.amazon.com/premiumsupport/knowledge-center/support-case-browser-har-file/

https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-create-api-as-simple-proxy-for-lambda.html