1. Architecture Overview

This system follows a layered, edge-secured architecture:

User → Route 53 → CloudFront → Private S3

There is no public access to the storage layer.
All requests must pass through CloudFront.

2. Component Roles
Amazon S3 – Private Origin

Stores website objects ( images)

Public access fully blocked

Not reachable from the internet

Only CloudFront is allowed

Purpose: isolated, durable object storage.

Amazon CloudFront – Security & Delivery Layer

Single public entry point

HTTPS termination

CDN edge protection

Origin Access Control to S3

Purpose: hide origin, enforce TLS, reduce attack surface.

AWS Certificate Manager – Trust Layer

Public certificate issued

DNS validation used

Attached to CloudFront

Automatic renewal

Purpose: encrypted transport and verified domain ownership.

Amazon Route 53 – DNS Control Plane

Domain hosted zone

DNS validation records

Alias records to CloudFront

Purpose: trusted routing and domain ownership.

3. Security Model

No public S3 permissions

CDN-only access pattern

TLS enforced

DNS-validated ownership

Origin hidden from users

4. Security Validation

Direct S3 object URL → ❌ Access denied

CloudFront URL → ✅ Works

Custom domain HTTPS → ✅ Works

Certificate validated → ✅

DNS controlled → ✅

This confirms the origin is protected and exposed only through a secure edge layer.
