---
title: "Week 7 Worklog"
date: 2026-06-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Learn Networking & CDN: Route 53, CloudFront.
* Learn how to secure applications with AWS WAF and Shield.
* Practice deploying CDN and security for websites.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 2 | Reviewed Lambda, Step Functions from Week 6. Learned about Route 53: hosted zones, record sets, routing policies. Understood DNS failover and health checks. Learned record types: A, AAAA, CNAME, MX, TXT | 01/06/2026 | 01/06/2026 | <https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html> |
| 3 | Created Hosted Zone in Route 53 to manage DNS for domain. Created A Record pointing to ALB endpoint to route traffic to load balancer. Created CNAME Record for www subdomain redirect to root domain. Configured Health Check to monitor endpoint availability. Created Failover record with primary target EC2 and secondary S3 for high availability. Updated nameservers at domain registrar to point to Route 53. Verified DNS propagation using dig or nslookup | 02/06/2026 | 02/06/2026 | <https://000010.awsstudygroup.com/> |
| 4 | Accessed CloudFront Console. Created new Distribution with origin as S3 bucket or ALB. Configured Default Cache Behavior with viewer protocol policy (HTTPS only). Added Price Class to select appropriate edge locations (All Locations or specific regions). Configured TTL (Minimum, Maximum, Default) to control cache duration. Enabled CloudFront Functions to manipulate requests and responses at edge. Tested distribution via CloudFront URL and verified caching works by header inspection | 03/06/2026 | 03/06/2026 | <https://000130.awsstudygroup.com/> |
| 5 | Requested SSL/TLS Certificate from ACM (AWS Certificate Manager). Validated domain using DNS validation method. Added CNAME record to Route 53 to complete validation automatically. Attached certificate to CloudFront Distribution. Enabled HTTPS for viewer requests. Redirected HTTP to HTTPS to enforce secure connection. Created Web ACL in AWS WAF to define security rules. Added rule to block SQL Injection attacks. Added rule to block XSS (Cross-Site Scripting) attacks. Added rule to block IP addresses from blocklist. Associated WAF ACL with CloudFront Distribution to protect website | 04/06/2026 | 04/06/2026 | <https://000026.awsstudygroup.com/> |
| 6 | Enabled AWS Shield Standard (free) for CloudFront to protect against DDoS. Understood Shield Standard protection features like volumetric attack mitigation. Created Web ACL with Rate-based rule to limit requests per IP (prevent abuse). Configured AWS Firewall Manager policy to centrally manage WAF rules. Added Rule Group for common attack patterns. Created S3 bucket with static website hosting enabled. Created CloudFront Distribution with OAI (Origin Access Identity) to restrict bucket access. Requested ACM certificate for custom domain. Configured Route 53 with A record pointing to CloudFront. Attached WAF Web ACL with CloudFront to filter malicious traffic. Tested HTTPS and verified SSL certificate works correctly | 05/06/2026 | 05/06/2026 | <https://000026.awsstudygroup.com/> |


### Week 7 Achievements:

* Configured Route 53 with DNS failover and health checks.
* Deployed CloudFront CDN with caching and edge functions.
* Set up SSL/TLS certificate with ACM for custom domain.
* Secured application with AWS WAF (SQL Injection, XSS protection).
* Enabled AWS Shield Standard to protect against DDoS attacks.
