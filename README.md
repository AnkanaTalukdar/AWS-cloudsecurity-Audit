**AWS Cloud Security Audit & Remediation**

**1. Project Overview:**
This projectperforms an end-toend security audit in AWS environment. It simulates the lifecycle of a professional security assessment, focusing on identifying misconfigurations, validating vulnerabilities through exploitation, and implementing industry-standard remediation strategies.

**2. Methodology: Pentesting Execution Standard (PTES)**
* Discovery: Automated reconnaissance using AWS IAM Access Analyzer.
* Vulnerability Validation: Proof of Concept (PoC) through unauthorized data access.
* Privilege Audit: Analyzing IAM roles for adherence to the Principle of Least Privilege (PoLP).
* Remediation: Implementation of cloud-native security guardrails and resource-level IAM policies.
* Validation: Final verification of hardened security posture.

**3. Phase-by-Phase Report**

**Phase 1: Reconnaissance & Discovery**

Objective: Identify public-facing assets and excessive identity permissions.

Tool: AWS IAM Access Analyzer.

Finding: Identified an S3 bucket (testdata-audit-project13) with public access permissions enabled.

**Phase 2: Vulnerability Exploitation (PoC)**

Objective: Validate that the misconfiguration is exploitable.

Action: Attempted unauthorized data exfiltration of passwords.txt via unauthenticated browser request.

Result: Successfully accessed sensitive data, confirming a critical confidentiality breach.

**Phase 3: Impact Assessment (Privilege Escalation)**

Objective: Audit identity permissions to assess the "blast radius."

Finding: The service user project13-audit was assigned AdministratorAccess, violating the Principle of Least Privilege.

**Phase 4: Remediation (Defense-in-Depth)**

Objective: Harden the environment to prevent future breaches.

S3 Hardening: Enabled "Block all public access" settings at the bucket level.

IAM Hardening: Implemented a scoped Inline Policy following the Principle of Least Privilege.

Policy Definition: Granted ListBucket and GetObject actions only for the specific project resource.

**Phase 5: Final Validation**

Objective: Confirm the vulnerability is successfully mitigated.

Action: Re-attempted unauthorized data access.

Result: System returned a 403 Access Denied error. Access Analyzer confirms zero active findings.

**4. Conclusion:**

This audit demonstrates the critical importance of continuous cloud monitoring and the application of the Principle of Least Privilege. By transitioning from a permissive configuration to a hardened state, the attack surface was successfully minimized, ensuring data integrity and confidentiality.
