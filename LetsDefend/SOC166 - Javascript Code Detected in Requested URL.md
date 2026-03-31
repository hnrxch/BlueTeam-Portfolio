# SOC166 - Javascript Code Detected in Requested URL

## Summary
A potential Cross-Site Scripting (XSS) attack was detected targeting a web application. 
Multiple malicious JavaScript payloads were identified in HTTP requests from a suspicious source IP, including several failed attempts prior to the alert.

## Details
- **Date/Time:** Feb 26, 2022, 06:56 PM  
- **Source IP:** 112.85.42.13  
- **Destination IP:** 172.16.17.17  
- **Destination Port:** 443  
- **Protocol:** HTTPS  
- **Action:** Allowed  

## Analysis
- The request contained JavaScript code in the URL:
  - '<script>javascript:alert(1)</script>'
- Multiple XSS payloads were observed before the alert, indicating probing and testing behavior  
- All responses returned HTTP 302 with response size 0  
- The redirection suggests the payload was not executed and the attack failed  
- The source IP is associated with malicious activity, with 45,324 reports on AbuseIPDB  
- According to VirusTotal, the IP is linked to an executable (`xjtzt6.exe`) identified as cryptomining malware  

## Evidence
- Sample payload:
- '/search/?q=prompt(8)'
- '/search/?q=<$script>javascript:$alert(1)<$/script>'
- '/search/?q=<$img%20src%20=q%20onerror=prompt(8)$>'
- '/search/?q=<$svg><$script%20?>$alert(1)'
- '/search/?q=<$script>$for((i)in(self))eval(i)(1)<$/script>'

## Conclusion
- This was a true positive XSS attempt  
- The attack was unsuccessful due to consistent redirection responses (302) with no execution evidence  
- No impact on the system was observed  

## Key Takeaways
- Repeated payload attempts indicate attacker probing behavior  
- HTTP 302 responses with empty bodies suggest failed execution  
- Threat intelligence (AbuseIPDB, VirusTotal) strengthens attribution of malicious intent  
