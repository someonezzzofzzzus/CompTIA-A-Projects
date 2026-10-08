DNS TROUBLESHOOTING

Problem:
Windows client cannot join the Active Directory domain.

Symptoms:
- mynetwork.com cannot be resolved
- Domain Controller cannot be located
- Domain join fails ["Issue-2.png"]

Investigation:
1. Checked IP configuration
2. Tested connectivity to Domain Controller
3. Checked DNS configuration
4. Ran nslookup
5. Discovered client was using router DNS 

Root Cause:
The Windows client was configured to use the router as its DNS server.
["Issue-1.png"]

Solution:
Changed the client's preferred DNS server to the Domain Controller.
["solution-1.png"]

Result:
DNS resolution succeeded and the client was successfully joined to the domain.
["solution-2.png"]


Lesson:
Active Directory relies on DNS for locating domain services.