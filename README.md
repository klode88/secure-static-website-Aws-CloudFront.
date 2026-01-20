# secure-static-website-Aws-CloudFront.
This project demonstrates how to design and deploy a secure, production-style static website architecture on AWS using native cloud services.The website is stored privately in Amazon S3 and delivered globally through Amazon CloudFront using HTTPS and a custom domain managed with Route 53.
Security Principles Applied (Core of This Project)

❌ S3 bucket is NOT public
✅ All access goes ONLY through CloudFront
✅ HTTPS enforced using ACM certificates
✅ DNS controlled via Route 53
✅ Certificate ownership validated with DNS
✅ No servers, no open ports, no public infrastructure
✅ Origin protected behind a CDN
User → Route 53 (DNS) → CloudFront (HTTPS + CDN) → Private S3 Bucket

AWS Services Used & Why

*****Amazon S3 – Private Object Storage
Stores website files (HTML, images)
Highly durable andscalable
Bucket access blocked from public internet
Acts only as an origin for CloudFront
Why S3:Serverless-Cheap-Extremely reliable-Designed for static content

*****Amazon CloudFront – Secure Content Delivery Network
Global HTTPS access point
Serves website to users
Hides the S3 bucket from the public internet
Improves performance and security
Why CloudFront:
Prevents direct S3 exposure-TLS terminationDDoS-resistant edge network-Origin access control

*****AWS Certificate Manager (ACM) – HTTPS & Trust
Issued a public SSL certificate
Validated ownership of domain via DNS
Enforced encrypted traffic
Why ACM:
Free managed certificates
Automatic renewal
Native CloudFront integration
Eliminates manual TLS management

******Amazon Route 53 – DNS & Domain Control
Hosted zone for the domain
DNS records pointing domain to CloudFront
Domain ownership verification
Why Route 53:
Highly available DNS
Native AWS integrations
Required for automated certificate validation

*****Implementation Steps
Created S3 bucket and uploaded website files
Blocked all public access on the bucket
Created CloudFront distribution with S3 as private origin
Requested ACM certificate (us-east-1 for CloudFront)
Validated certificate using Route 53 DNS records
Attached certificate to CloudFront
Added custom domain names
Created Route 53 alias records to CloudFront
Tested HTTPS access and blocked S3 direct access
Verified public access only works via CloudFront

******Security Validation
Direct S3 object URL → ❌ AccessDenied
CloudFront URL → ✅ Works
Custom domain over HTTPS → ✅ Works
Certificate validated → ✅
DNS controlled → ✅
This confirms the bucket is protected and only reachable through the secure CDN layer.
