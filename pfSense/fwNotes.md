# DNS
Set DNS IPs to (CloudFlare)[1.1.1.1], (Goggle)[8.8.8.8], and (Quad9)[9.9.9.9]\
Set **DNS Resolution Behavior** to `Use remote DNS Servers, ignore local DNS`\

# Rule Generation
Click on `Firewall > Rules`\
Go to `LAN`
Click `Add` above/below\
Set your action `Pass | Block | Reject`\
Set your `Interface`
Choose your `Address Family` > `IPv4 | IPv6`
Select your `Protocol` > `TCP | UDP`
Add your `Source`
Add your `Destination` or `Destination Port`   
Choose whether to `Log` your packets or not
`Save`