---
layout: default
title: Troubleshooting
parent: CloudFront
nav_order: 2
---

Troubleshooting CloudFront
-- 

Using Apache Bench for Simple Load Testing

`$ ab -vk -n 1000 https://doc.tuertolin.com/Linux/`

```
Benchmarking doc.tuertolin.com (be patient)

Server Software:        AmazonS3
Server Hostname:        doc.tuertolin.com
Server Port:            443
SSL/TLS Protocol:       TLSv1.2,ECDHE-RSA-AES128-GCM-SHA256,2048,128
Server Temp Key:        ECDH P-256 256 bits
TLS Server Name:        doc.tuertolin.com

Document Path:          /Linux

Concurrency Level:      1
Time taken for tests:   13.142 seconds
Complete requests:      1000
Failed requests:        0
Non-2xx responses:      1000
Total transferred:      8799800 bytes
HTML transferred:       8027000 bytes
Requests per second:    76.09 [#/sec] (mean)
Time per request:       13.142 [ms] (mean)
Time per request:       13.142 [ms] (mean, across all concurrent requests)
Transfer rate:          653.89 [Kbytes/sec] received

```
