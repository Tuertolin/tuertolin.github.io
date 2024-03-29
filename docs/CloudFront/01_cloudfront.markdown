---
layout: default
title: cURL
parent: CloudFront
nav_order: 1
---

Troubleshooting CloudFront with cURL.
-- 

This is the baseci cURL commnad to see the headers from a request to a CloudFront distrubution:


`curl -vo /dev/null https://doc.tuertolin.com` 

### Output

```
* Rebuilt URL to: https://doc.tuertolin.com/
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0*   Trying 18.67.95.10...
* TCP_NODELAY set
* Connected to doc.tuertolin.com (18.67.95.10) port 443 (#0)
...
> GET / HTTP/2
> Host: doc.tuertolin.com
> User-Agent: curl/7.58.0
> Accept: */*
...
< HTTP/2 200
< content-type: text/html
< content-length: 7537
< date: Sat, 14 Aug 2021 11:14:17 GMT
< last-modified: Tue, 27 Jul 2021 11:44:28 GMT
< etag: "e543120cedbeb7dc906f1a3369495b25"
< server: AmazonS3
< strict-transport-security: max-age=63072000; includeSubdomains; preload
< content-security-policy: default-src 'none'; img-src 'self'; script-src 'self'; style-src 'self'; object-src 'none'
< x-content-type-options: nosniff
< x-frame-options: DENY
< x-xss-protection: 1; mode=block
< referrer-policy: same-origin
< vary: Accept-Encoding
< x-cache: Miss from cloudfront
< via: 1.1 1d3e75fe2262e8a6f4a318b2bf3e6570.cloudfront.net (CloudFront)
< x-amz-cf-pop: SYD62-P1
< x-amz-cf-id: Sck9X4me50SLimLrJuVcnAP_EC4uSxQpL6uYG7-UX0wizXSk9UDGBg==
<
```

As we can see in the above output, we have recieved the following headers from the CloudFront distribution associate it to doc.tuertolin.com:

```
< x-cache: Miss from cloudfront
< via: 1.1 1d3e75fe2262e8a6f4a318b2bf3e6570.cloudfront.net (CloudFront)
< x-amz-cf-pop: SYD62-P1
< x-amz-cf-id: Sck9X4me50SLimLrJuVcnAP_EC4uSxQpL6uYG7-UX0wizXSk9UDGBg==
```

Also, there are some extra security headers that were put in place through a Lambda@Edge function attached to the cloudfront distribution. 



