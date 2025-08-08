# OSINT Reconnaissance Report — walmart.com

**Author:** Carlo Cedillo de la Fuente Alvarez
**Date:** 2025-08-08  
**Target:** walmart.com  
**Purpose:** Educational OSINT demonstration for portfolio. All data gathered from public online sources; no exploitation performed. This report is for **educational** and **ethical** purposes only.

---

## Executive Summary
This report summarizes publicly-available domain, DNS, hosting, and third-party service information collected for `walmart.com`. The reconnaissance demonstrates common OSINT techniques used to map an organization's external footprint and identify potential exposure. No active intrusion or exploitation was performed — only publicly accessible resources and web lookups were used.

---

## Methodology & Tools
Tools and websites used (browser-based, no installation required):
- SecurityTrails (subdomains / DNS)
- WHOIS / DomainTools (domain registration details)
- Netcraft / BuiltWith (hosting & technology stack)
- Hunter.io (email format)
- HaveIBeenPwned (breach visibility)
- Censys / Netcraft / SecurityTrails (service and hosting info)
- Manual inspection of DNS A / MX / TXT records via nslookup.io

---

## Findings

### 1) Domain / Hosting
- **Domain:** `walmart.com`
- **Hosting provider (inferred):** Akamai Technologies, Inc.
- **Observed IPv4 (example):** `184.51.141.181` (note: large enterprise sites use CDNs and multiple IP ranges)
- **Mail Exchange (MX) record(s):** `mxa-000c7201.gslb.pphosted.com` (indicates use of a hosted mail provider)

### 2) DNS / Subdomains (collected)
> *List below uses representative subdomain types and DNS records observed via SecurityTrails / DNS lookups. Replace or expand with your full list if you collected more items.*

- `www.walmart.com` — main web front-end (CDN)
- `api.walmart.com` — API endpoints (observed or likely)
- `mail.*` / `mx` records — hosted mail infrastructure
- Additional listed subdomains and DNS TXT entries associated with third-party integrations

### 3) Third-party / Service Identifiers (observed)
The following service/vendor indicators were found in DNS or configuration metadata. Values shown below are redacted for safety; they indicate presence of integrations:

- **Canva verification token:** `[REDACTED]`  
- **Duo verification token:** `[REDACTED]`  
- **Fastly (CDN) marker:** `fdd46849203012022-468492-2022-03-01` (CDN signature/identifier observed)  
- **GlobalSign TLS/Cert identifiers:** `[REDACTED]` (multiple)  
- **Google site verification / tokens:** `[REDACTED]` (multiple)  
- **Miro verification:** `[REDACTED]`  
- **OpenAI marker:** `[REDACTED]`  
- **Slack verification marker:** `[REDACTED]`  
- **Wiz / Wrike integration markers:** `[REDACTED]`

**Interpretation:** These indicators suggest Walmart uses a variety of third-party SaaS integrations (design/collab tools, identity/auth providers, CDNs, and possibly security tools). From a defensive perspective, this expands the attack surface (third-party credentials, exposed tokens in DNS, supply-chain considerations).

---

## Risk Assessment (high-level)
1. **Exposure via third-party integrations:** Publicly-listed verification tokens in DNS/TXT (if real verification tokens) can lead to risk if they are used to validate ownership or link to admin functionality. **Risk:** Medium–High (depends on token usage).
2. **Large CDN footprint (Akamai/Fastly):** CDNs reduce direct server exposure but introduce caching/configuration complexity. Misconfigured CDN behavior can lead to cache poisoning or accidental exposure of sensitive endpoints. **Risk:** Low–Medium.
3. **Mail infrastructure via hosted providers:** Hosted mail providers reduce operational burden but can be targeted for phishing and business-email-compromise (BEC) campaigns. **Risk:** Medium.
4. **Multiple vendor touchpoints:** Each third-party service represents additional account security dependencies and potential supply-chain vectors. **Risk:** Medium.

---

## Recommendations (practical, concise)
> These are general OSINT-style recommendations suitable for an enterprise. They are not exploit instructions — they are defensive and governance-oriented.

1. **Audit DNS TXT Records & Remove Unnecessary Verification Strings**  
   - Remove any old or unnecessary verification tokens from DNS TXT records. If tokens are required, rotate them and document usage.  
2. **Inventory Third-party Integrations**  
   - Maintain an up-to-date inventory of SaaS providers (Canva, Miro, Wrike, Duo, Wiz, Slack, etc.) and the accounts tied to them. Enforce least privilege and 2FA/MFA on admin accounts.  
3. **Protect Mail Infrastructure**  
   - Ensure SPF / DKIM / DMARC are correctly configured to reduce phishing/BEC risk. Monitor MX records and mail logs for anomalies.  
4. **CDN Configuration Review**  
   - Review caching rules, origin server access controls, and WAF rules. Ensure no sensitive endpoints are being cached inadvertently.  
5. **Secure Verification Tokens**  
   - Treat all verification tokens as secrets. Remove any that are not strictly necessary, rotate tokens periodically, and store them in a secrets manager if used internally.  
6. **Continuous Monitoring**  
   - Use external monitoring (Censys, SecurityTrails, certificate transparency logs) to alert on new subdomains, cert changes, or anomalous DNS updates.

---

## Conclusion
This OSINT exercise demonstrates how an attacker or defender can map an enterprise’s external surface using only publicly available tools. The key defensive takeaways are inventorying third-party integrations, securing DNS/TXT records, enforcing strict access controls on SaaS platforms, and ensuring robust email protections.

---

## Appendices

### Appendix A — Tools / Sources
- SecurityTrails — DNS & subdomain enumeration  
- Whois / DomainTools — domain registration records  
- BuiltWith / Netcraft — tech stack & hosting reconnaissance  
- Hunter.io — email format heuristics  
- HaveIBeenPwned — breach visibility  
- Censys / Certificate Transparency logs — certificate & service discovery



---

*End of report*
