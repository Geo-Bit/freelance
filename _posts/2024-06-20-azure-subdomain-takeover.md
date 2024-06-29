---
layout: post
title: "Azure Subdomain Takeover & Dangling DNS"
date: 2024-06-20
tags: [Azure, DNS, Security]
---

# Azure Subdomain Takeover & Dangling DNS

As a security researcher and application security engineer, I frequently encounter the issue of dangling DNS or subdomain takeovers, particularly within Microsoft Azure environments. This occurs when web applications are deleted, but their associated CNAME records on custom domains are not removed. This leaves the domain vulnerable to malicious actors who can redirect traffic to their own infrastructure.

## Understanding the Problem

When you create a web application in Azure and assign it a custom domain using a CNAME record, you establish a link between your domain and Azure's resources. If these resources are later deleted without removing the CNAME record, the domain remains pointed to a now non-existent resource. This creates a "dangling" DNS entry.

### What Happens Next?

1. **Domain Availability Check**: Attackers can periodically check for available subdomains.
2. **Resource Re-creation**: They can then create a resource in Azure with the same name, effectively taking over the subdomain.
3. **Malicious Redirection**: The hijacked subdomain can be used to serve malicious content, phish for credentials, or spread malware.

## Real-world Example

Let's say you have a CNAME record pointing `app.example.com` to `myapp.azurewebsites.net`. If `myapp` is deleted but the CNAME record remains, an attacker can claim `myapp` in Azure, and `app.example.com` will now point to their resource.

### DNS Provider Configuration

For demonstration, we'll use a common DNS provider, such as GoDaddy, to illustrate how to check and remove these records.

```plaintext
example.com
├── www.example.com (CNAME -> myapp.azurewebsites.net)
├── app.example.com (CNAME -> myapp.azurewebsites.net)
└── blog.example.com (A -> 192.0.2.1)
```

## Mitigation and Remediation Strategies

### Regular Audits

Perform regular audits of your DNS records to ensure they are still valid. Tools and scripts can automate this process.

```bash
# Simple script to check DNS records
for domain in $(cat domains.txt); do
  nslookup $domain | grep "can't find" && echo "$domain is dangling"
done
```

## Automated Cleanup

Implement automated cleanup of DNS records when deleting Azure resources. Azure Resource Manager (ARM) templates and scripts can be configured to remove DNS entries.

```json
{
  "resources": [
    {
      "type": "Microsoft.Network/dnszones/CNAME",
      "apiVersion": "2018-05-01",
      "properties": {
        "TTL": 3600,
        "CNAMERecord": {
          "cname": "myapp.azurewebsites.net"
        }
      },
      "dependsOn": ["[resourceId('Microsoft.Web/sites', 'myapp')]"]
    }
  ]
}
```

## Use Azure Managed Services

Where possible, use Azure-managed services that handle DNS records for you. Azure Front Door, for example, can manage your custom domains and reduce the risk of dangling DNS.

## Conclusion

Dangling DNS records pose a significant security risk, especially in dynamic cloud environments like Azure. By understanding the problem and implementing the strategies outlined above, you can mitigate and remediate these risks effectively. Regular audits, automated cleanups, and utilizing managed services are key steps to securing your domains.

Stay vigilant and keep your infrastructure secure!
