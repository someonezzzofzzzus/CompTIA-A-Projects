Ticket ID: 14557455

Date: 01.01.2021

Department/User: Accounting/Bob-Smith

Issue description: Network unavailable

Symptoms: 

    -   Searching engine returns page "No Internet"
    -   Enthernet connection icon on taskbar...

Assesment/Troubleshooting:

    -   Look into the Ethernet cable socket (RJ45), on the back side of the PC block, ensuring that it is connected to the PC

    -   Ping google.com to ensure DNS server connectivity
    -   Ping 8.8.8.8 to ensure access to the Intenet
        ["Ping connectivity"]   .../Ticket_Simulation/screenshots/INC-01/INC-01_ping.png    ["SCREENSHOT"]

    -    Check Internet connection through Windows command line using command 
        "ipconfig"                  
        ["IP Configuration"]    .../Ticket_Simulation/screenshots/INC-01/INC-01_ipconfig-screen.png   ["SCREENSHOT"]

Root cause:

    -   Ping command returned "...could not find the host google.com ..." implying that PC is not connected to the DNS server
    -   DHCP has not provided IP address for PC, it performed APIPA IP address asignmend with 169.254.x.x 

Resolution:

    -   Request a new IP address from DHCP server ["ipconfig /renew"]
        ["Requesting New IP Address"]   .../Ticket_Simulation/screenshots/INC-01/INC-01_ipconfig-renew.png    ["SCREENSHOT"]

Verification:

    -   Execute command ["ipconfig"] with ensuring that IPv4 address was assigned properly (192.168...) with private address 
    
    -   Ping again ["google.com"] ensuring DNS and Internet connectivity

Status: **Resolved


