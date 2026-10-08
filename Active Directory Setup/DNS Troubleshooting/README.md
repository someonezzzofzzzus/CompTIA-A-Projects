# DNS Troubleshooting

## Problem

The Windows client was unable to join the Active Directory domain.

## Symptoms

- `mynetwork.com` could not be resolved.
- The Domain Controller could not be located.
- The domain join operation failed.

![Domain Join Failure](Active Directory Setup/DNS Troubleshooting/issue-1.png)

## Investigation

The issue was investigated using the following steps:

1. Checked the client's IP configuration.
2. Tested connectivity to the Domain Controller.
3. Checked the client's DNS configuration.
4. Used `nslookup` to test DNS resolution.
5. Discovered that the client was using the home router as its DNS server instead of the Active Directory DNS server.

## Root Cause

The Windows client was configured to use the **router as its DNS server**.

![Incorrect DNS Configuration](screenshots/Issue-1.png)

Because the client was not using the Active Directory DNS server, it could not properly resolve the internal domain or locate the Domain Controller.

## Solution

The client's preferred DNS server was changed from the router to the **Domain Controller's IP address**.

![Correct DNS Configuration](screenshots/solution-1.png)

The client was then configured to use the internal DNS server for domain name resolution.

## Result

After correcting the DNS configuration, DNS resolution was successful and the client was able to locate the Domain Controller and successfully join the Active Directory domain.

![Successful Domain Join](screenshots/solution-2.png)

## Lesson Learned

This troubleshooting exercise demonstrated the importance of DNS in an Active Directory environment.

**Active Directory relies heavily on DNS to locate domain services, including Domain Controllers.**

A client may have working network connectivity and still be unable to join or communicate with an Active Directory domain if its DNS configuration is incorrect.

### Troubleshooting Flow

```text
Domain Join Failed
       ↓
Check Network Configuration
       ↓
Test DNS Resolution
       ↓
Discover Incorrect DNS Server
       ↓
Change DNS to Domain Controller
       ↓
Test DNS Again
       ↓
Domain Controller Located
       ↓
Domain Join Successful
```
