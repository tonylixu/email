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