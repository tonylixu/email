## mx mechanism
* mx - The basic form without any extensions uses the MX RR of the sender-domain to verify the mail source-ip. The MX record(s) return a host name from which the A record(s) can be obtained and compared with the source-ip.
* mx/cidr - applies the IP Prefix or slash range to the A RR address.
* mx:domain - With any of the domain extensions the MX record of the designated (substituted) domain is used for verification. The domain form may use macro-expansion features.

## Note
Warning Remember the MX RR defines the receiving MTA for the domain. If this is not the same host(s) as the sending (SMTP) MTA then tests based on an mx type will fail. We have also received a report that mx on its own is rejected by certain SPF libraries. We regard this as an error and are trying to contact the library developer to clarify the issue.

## Example
```bash
; fragment for example.com
$ORIGIN example.com.
....
@    IN  TXT "v=spf1 mx:example.net -all"
; verify sender using example.net MX and A RRs

; fragment for example.com
$ORIGIN example.com.
....
@    IN  TXT "v=spf1 mx/26 -all"
; verify sender using example.com MX and 
```

## Use mx with domain names, not mailserver names
Specifying mx:mailserver.example.com is generally incorrect, unless you truly want SPF validation to look up all the hosts that accept mail for the "mailserver.example.com" domain. (Usually, there will not be any such hosts, because "mailserver.example.com" is itself a host, not a domain.) This will not show up as a syntax error, however, it will simply not match anything.

The correct usage for validating against the MX records for "example.com" is mx:example.com, or if you want to specify a particular mail server's hostname or IP, a:mailserver.example.com or ip4:x.x.x.x. Finally, note that when your SPF rule is stored as a DNS record associated with "example.com", then "example.com" is the default domain for the rule, so mx on its own (with no explicit domain specified) is sufficient to check the sender IP against all the MX mail hosts listed for "example.com", in that context.

As of 2008 the SenderID wizard makes it easy to get this wrong. As a simple rule, if the commands `dig -tmx mailserver.example.com` or `nslookup -q=mx mailserver.example.com` yield nothing, then using mx:mailserver.example.com wastes the bandwidth of receivers checking SPF as well as the bandwidth of your own name servers answering pointless queries.