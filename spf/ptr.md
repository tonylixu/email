## ptr
* ptr - Use the source-ip's PTR RR and a reverse map query. The A/AAAA RR for the host is then obtained. If this IP matches the sender-ip AND the sender-domain is the same as the domain name of the host obtained from the PTR RR then the test passes.
* ptr:domain - The form ptr:domain replaces the sender-domain with domain in the final check for a valid domain name. The domain form may use macro-expansion features.

## Note
 The ptr sender mechanism is strongly discouraged by RFC 7208 which even goes so far as to suggest its immediate removal for performance reasons since it places a load on the IN-ADDR.ARPA (IPv4) or IP6.ARPA reverse-map domains which generally have less capacity than the gTLD and ccTLD domains.

 ## Example:
 ```bash
 ; fragment for example.com
$ORIGIN example.com.
....
@            IN TXT "v=spf1 ptr -all"
; the effect is to allow any host which is 
; reverse mapped in the domain to send mail

; fragment for example.net
$ORIGIN example.net.
....
@            IN TXT "v=spf1 ptr:example.com -all"
; the effect is to allow any host which is 
; reverse mapped in the domain example.com to send mail
; for example.net
....
 ```