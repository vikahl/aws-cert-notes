# Route 53

The name refers to the DNS port: 53.

## Exam tips

- Elastic load balancers (ELB) does not have pre-defined IPv4 addresses, they are resolved using DNS name
- Understand the difference between alias records and CNAME
- Given the choice, always choose alias over CNAME
- Domain names can be bought directly from AWS

## DNS basics

- Second level domain name is the `.co` part in `.co.uk`
- User requests `example.com` -> TLD queries for NS record -> SOA which contains the records

## Common DNS types and records

- SOA records  
  Stores information about name servers, administrator, TTL, … for the zone
- NS records  
  Used by TLD servers to direct traffic to the content DNS server which contains the authoritative DNS records
- A (address) record, IPv4, translates `example.com ⇒ 93.184.216.34`
- AAAA record, IPv6, translates `example.com ⇒ 2001:db8:85a3::8a2e:370:7334`
- Canonical name (CNAME) resolves one domain name to another domain name `organization.example.com -> example.org`.  
  Cannot be used for zone apex records ("naked domain names") such as `example.com`
- Alias record, almost same as CNAME, but can be used for zone apex records ("naked domain names"). `example.com -> example.org`. Given the choice, always choose alias over CNAME.
- MX records
- PTR records
