# Route 53

The name refers to the DNS port, 53.

## Exam tips

- Elastic load balancers (ELB) does not have pre-defined ipv4 addresses, they are resolved using DNS name
- Understand the difference between alias records and cname
- Given the choice, always choose alias over cname
- Domain names can be bought directly from AWS (might take up to 3 days)

## DNS basics

- Second level domain name is the `.co` part in `.co.uk`
- Start of authority record (SOA) stores information about name servers, administrator, ttl, … for the zone 
- Name server record (NS)
  - Used by TLD servers to direct traffic to the content DNS server which contains the authoritative DNS records
- User requests `example.com` -> TLD queries for NS record -> SOA which contains the records

## Common DNS types and records

- SOA records
- NS records
- A (address) record, translates `example.com -> 93.184.216.34`
- Canonical name (CNAME) resolves one domain name to another domain name `organization.example.com -> example.org`.
  Cannot be used for zone apex records ("naked domain names") such as `example.com`
- Alias record, almost same as CNAME, but can be used for zone apex records ("naked domain names"). `example.com -> example.org`
- MX records
- PTR records
