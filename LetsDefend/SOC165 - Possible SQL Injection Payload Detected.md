# SOC165 - Possible SQL Injection Payload Detected

## Summary
A potential SQL Injection (SQLi) attack was detected targeting a web application. Multiple malicious payloads were identified in HTTP requests from a suspicious source IP.

## Details
- **Date/Time:** Feb 25, 2022 (11:30 AM – 11:34 AM)  
- **Source IP:** 167.99.169.17  
- **Destination IP:** 172.16.17.18  
- **Destination Port:** 443  
- **Protocol:** HTTPS  
- **Action:** Permitted  

## Analysis
- Multiple HTTP requests contained SQL injection payloads
- Requests were sent within a short time frame, indicating automated or semi-automated activity  
- All malicious requests resulted in HTTP 500 responses with identical response sizes (948 bytes)  
- A normal request returned HTTP 200 with a larger response size (3547 bytes), confirming expected behavior  

## Evidence
- Sample payloads:
-  /search/?q='
-  /search/?q=' OR '1
-  /search/?q=' OR 'x'='x
- /search/?q=1' ORDER BY 3--+
- /search/?q=" OR 1=1 -- -

## Conclusion
- This was a true positive SQL Injection attempt.  
- The attack was unsuccessful, as all responses returned consistent error codes (500) and identical response sizes, indicating no successful query execution.  
- No evidence of impact or post-exploitation activity was observed.

## Key Takeaways
- SQLi can be identified through payload patterns in requests  
- Response size and status codes help determine attack success  
- Consistent errors with no variation usually indicate failed exploitation  
