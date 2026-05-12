AWS Cloud Security Audit & Remediation
Project Overview:
This project demonstrates a professional end-to-end security audit of an Amazon Web Services 
(AWS) environment. The goal was to identify critical misconfigurations in cloud storage (S3) 
and Identity and Access Management (IAM), document the findings using automated tools, and 
implement industry-standard remediation.

Phase 1: Discovery & Vulnerability Identification:
1. S3 Storage Misconfiguration:
*	Vulnerability: An S3 bucket was configured with public read access.
*	Evidence: Sensitive data (passwords.txt) was accessible via a public URL without 
authentication.
*	Automated Finding: The AWS IAM Access Analyzer flagged the bucket testdata-audit-l 
as having "Public Read" access.

Evidence: Public Exposure & Finding:
Figure 1: Object overview for 'passwords.txt' showing the live public URL.
Figure 2: Active finding in Access Analyzer highlighting a bucket with public read access.

2. IAM Privilege Escalation:
*	Vulnerability: A test user (ankana-audit) was assigned the AdministratorAccess managed 
policy directly.
*	Risk: This violates the Principle of Least Privilege (PoLP), granting full control over 
the entire AWS account to a non-administrative user.
*	Identity Risk: The IAM Dashboard and user setup confirmed that over-privileged roles 
were created without proper scoping.

Evidence: Over-Privileged User Creation:
Figure 3: Directly attaching the 'AdministratorAccess' policy during user creation.
Figure 4: Final review of the 'ankana-audit' user possessing full administrative rights.

Phase 2: Remediation (The Fix):
1. Securing S3 Storage
*	Action: Enabled "Block all public access" at the bucket level.
*	Action: Deleted the permissive JSON bucket policy.
*	Result: The public URL now returns a 403 Forbidden error, and the Access Analyzer 
finding is resolved.

Evidence: Closing the Leak:
Figure 5: Activating 'Block all public access' settings to secure the bucket.
Figure 6: Browser confirmation showing 'AccessDenied' when attempting to reach the file 
publicly.

2. Implementing Least Privilege:
*	Action: Removed the AdministratorAccess policy from the user.
*	Action: Created and attached a Custom Inline Policy that restricts access only to the 
specific audit bucket.

Secure Policy Implemented:
JSON
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::962765735107:user/ankana-audit"
            },
            "Action": [
                "s3:ListBucket",
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::testdata-audit-project19-ankana",
                "arn:aws:s3:::testdata-audit-project19-ankana/*"
            ]
        }
    ]
}

Tools Used:
*	AWS IAM Access Analyzer: For automated resource scanning.
*	IAM Management Console: For auditing user security hygiene.
*	S3 Bucket Policies: For resource-based access control.
*	GitHub: For project documentation and audit reporting.

Audit Environment Construction:
Figure 7: Final repository layout for the 'AWS-cloudsecurity-Audit' project.

Conclusion:
By identifying these vulnerabilities and applying remediation, the attack surface of the AWS 
account was significantly reduced. This project highlights the importance of continuous 
monitoring using tools like Access Analyzer and the strict application of identity-based security 
controls.
