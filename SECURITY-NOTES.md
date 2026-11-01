# Security Notes: Log4Shell (CVE-2021-44228)

## Summary

**Log4Shell** is a critical remote code execution (RCE) vulnerability in Apache Log4j 2, an widely used Java logging library. An unauthenticated remote attacker can exploit specially crafted log messages containing JNDI lookups (e.g., `${jndi:ldap://...}`) to execute arbitrary code loaded from attacker-controlled LDAP/RMI servers. The vulnerability is present in the JNDI features used in configuration, log messages, and parameters when message lookup substitution is enabled.

## CVE Identifier

- **CVE-2021-44228** — Remote code injection in Log4j (Log4Shell)

## Affected Versions

| Range | Details |
| --- | --- |
| **Affected** | Apache Log4j2 **2.0-beta9 through 2.14.1** (per CISA; NVD lists 2.0-beta9 through 2.15.0 excluding security releases 2.12.2, 2.12.3, and 2.3.1) |
| **Not affected** | log4j-net, log4cxx, and other Apache Logging Services projects (vulnerability is specific to log4j-core) |
| **Java 1 branch (EOL)** | Log4j 1.x is End Of Life and vulnerable to other RCE vectors; migrate to Log4j 2.x |

## Fixed Version

- **2.16.0** — disables JNDI by default and completely removes support for message lookups (fixes CVE-2021-44228 completely; 2.15.0 only disabled it partially — tracked as CVE-2021-45046)
- **2.17.1+** — CISA recommendation; fixes CVE-2021-44228, CVE-2021-45046, CVE-2021-45105, and CVE-2021-44832
- **Backports:** 2.3.1 (Java 6), 2.12.2 / 2.12.3 (Java 7), 2.12.4 (Java 7), 2.3.2 (Java 6)
- Keep `log4j-api` at the same version as `log4j-core` for compatibility.

## Severity

- **CVSS 3.x Base Score: 10.0 — CRITICAL**
- Vector: `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H`
- Attack vector: Network | Attack complexity: Low | Privileges required: None | User interaction: None | Scope: Changed | Confidentiality: High | Integrity: High | Availability: High

## Sources

- NVD CVE-2021-44228: https://nvd.nist.gov/vuln/detail/cve-2021-44228
- Apache Logging Services Security Guidance: https://logging.apache.org/security.html
- CISA Apache Log4j Vulnerability Guidance: https://www.cisa.gov/news-events/news/apache-log4j-vulnerability-guidance
- GitHub Advisory Database (GHSA-JFH8-C2JP-5V3Q): https://github.com/advisories/ghsa-jfh8-c2jp-5v3q
- Log4Shell remediation cheat sheet (Snyk): https://snyk.io/blog/log4shell-remediation-cheat-sheet/
- NCSC-NL Log4Shell detection/mitigation: https://github.com/NCSC-NL/log4shell

## Related Tracking

Remediation actions are tracked as sub-issues of issue #1 ("Log4Shell remediation checklist") in this repository.
