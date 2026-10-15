BUX is a Netherlands-based digital investment platform and subsidiary of ABN AMRO, offering retail customers accessible investment services, including trading in stocks, ETFs, fractional shares, and automated investment plans. As part of its product expansion, BUX is introducing a new Savings Proposition in collaboration with ABN AMRO, enabling customers to open and manage savings accounts alongside their existing investment services. The proposition is designed to support both savings and investment needs within the BUX ecosystem. 

BUX | Do more with your money
+1



The Savings Proposition leverages Mambu, a third-party cloud banking platform, to support savings-related banking functionality. The BUX Web Application and associated backend services are hosted on Google Cloud Platform (GCP), utilizing containerized workloads and Kubernetes infrastructure.
This Security Evaluation & Advice (SEA) assessment is specifically conducted for the Friends & Family (F&F) release, which will initially be made available to a limited group of users ahead of a broader customer rollout.


Overall Expert Opinion
From an Application Security perspective, the BUX Savings Proposition benefits from its integration with Mambu, an established third-party banking platform with SOC 2 Type II assurance. This provides a level of assurance regarding Mambu's independently assessed controls; however, it does not extend automatically to the security of BUX's application, cloud infrastructure, or integration architecture.
The assessment identified significant gaps in BUX's secure development and deployment practices. Automated secret scanning, SAST, SCA, and container image vulnerability scanning are currently absent from the CI/CD pipeline. Furthermore, no vulnerability severity thresholds or security release gates have been established, increasing the likelihood of vulnerable code, dependencies, or container images reaching production.
At the infrastructure level, the absence of hardened base images, Kubernetes role hardening, runtime container security monitoring, and pod-to-pod network restrictions introduces additional risks of unauthorized access, lateral movement, and workload compromise. Security visibility is further limited by the absence of centralized security event collection and SIEM integration across infrastructure and application components.
While Google Cloud Armor provides web application firewall protection and a network-level VPN tunnel is reportedly established for connectivity, the security configurations governing Kubernetes API integration, network connectivity, and secrets management remain insufficiently understood and require further validation.
Considering the limited exposure associated with the Friends & Family release, a risk-based conditional acceptance may be considered, provided that the identified weaknesses are formally documented, appropriate compensating controls are validated, and remediation commitments are established before broader customer rollout.
2. Conclusion
The BUX Savings Proposition presents a number of security weaknesses, primarily associated with the absence of automated security controls in the CI/CD pipeline, insufficient Kubernetes workload hardening, and limited security monitoring capabilities.
Although the F&F release is restricted to a small group of users, this limitation reduces exposure rather than eliminating the underlying security risks. The existing Cloud Armor protection, VPN connectivity, and Mambu's third-party assurance provide positive security considerations but do not fully compensate for the identified gaps.
From an Application Security perspective, the F&F release may be considered conditionally acceptable, subject to documented risk acceptance, validation of critical security controls, and agreed remediation timelines. The identified gaps should be addressed before extending the Savings Proposition to a broader customer base.



3. List of Security Issues
#	Security Issue	Proposed Severity
1	Absence of automated secret scanning in CI/CD	High
2	Absence of Software Composition Analysis (SCA)	High
3	Absence of Static Application Security Testing (SAST)	High
4	Absence of container image vulnerability scanning	High
5	Missing CVE severity thresholds and security release gates	High
6	Container base images not hardened	Medium
7	BUX–Mambu Kubernetes/API integration security not validated	Pending
8	VPN tunnel security configuration not validated	Pending
9	Kubernetes RBAC and cluster hardening not implemented	High
10	Kubernetes secrets management controls not validated	Pending
11	Absence of centralized security logging and SIEM integration	High
12	Absence of runtime container security monitoring	Medium
13	Missing pod-to-pod network restrictions and segmentation	High



   4. Existing Security Controls
- Third-Party Assurance: Mambu has been identified as having SOC 2 Type II assurance; the applicable report, period, and scope should be verified.
- Web Application Protection: Google Cloud Armor is deployed as the WAF solution. Akamai is not used.
- Network Connectivity: A VPN tunnel is reportedly established, although its configuration and security boundaries require validation.
- Release Exposure: The initial F&F release is restricted to a limited number of users, reducing the initial customer exposure.

Management recommendation: Proceed only through formal conditional risk acceptance for the limited F&F release, with security ownership, compensating controls, and remediation deadlines documented. Broader production rollout should be subject to reassessment of the outstanding security gaps.
