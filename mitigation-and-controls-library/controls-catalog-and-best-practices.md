---
description: >-
  Security at the expense of usability comes at the expense of Security.  - Avi
  Douglen, OWASP Board of Directors
---

# Controls Catalog & Best Practices

This section contains controls by framework that were identified to be material to Node Operator risks

## Summary

<table><thead><tr><th width="443">Framework</th><th>Criterion</th></tr></thead><tbody><tr><td>OWASP</td><td><a href="https://owasp.org/Top10/A01_2021-Broken_Access_Control/">A01:2022: Broken Access Control</a></td></tr><tr><td>OWASP</td><td><a href="https://owasp.org/Top10/A10_2021-Server-Side_Request_Forgery_(SSRF)/">A10:2021: Server Side Request Forgery</a></td></tr><tr><td>SOC2 Trust Services Criteria</td><td>CC 5.2</td></tr><tr><td>SOC2 Trust Services Criteria</td><td>CC 6.1</td></tr><tr><td>SOC2 Trust Services Criteria</td><td>CC 6.3</td></tr><tr><td>SOC2 Trust Services Criteria</td><td>CC 6.7</td></tr><tr><td>SOC2 Trust Services Criteria</td><td>CC 7.1</td></tr><tr><td>SOC2 Trust Services Criteria</td><td>CC 7.2</td></tr><tr><td>SOC2 Trust Services Criteria</td><td>CC 7.3</td></tr><tr><td>SOC2 Trust Services Criteria</td><td>CC 7.5</td></tr><tr><td>SOC2 Trust Services Criteria</td><td>CC 8.1</td></tr><tr><td>SOC2 Trust Services Criteria</td><td>CC 8.2</td></tr><tr><td>SOC2 Trust Services Criteria</td><td>CC 8.3</td></tr><tr><td>SOC2 Trust Services Criteria</td><td>CC 9.1</td></tr><tr><td>SOC2 Trust Services Criteria</td><td>CC 9.2</td></tr><tr><td>SOC2 Trust Services Criteria</td><td>A 1.1</td></tr><tr><td>SOC2 Trust Services Criteria</td><td>PI 1.2</td></tr><tr><td>SOC2 Trust Services Criteria</td><td>PI 1.3</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 5.15</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 5.16</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 5.17</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 5.18</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 7</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 8.2</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 8.7</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 8.9</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 8.10</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 8.16</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 8.18</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 8.21</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 8.22</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 8.25</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 8.29</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 8.30</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 8.31</td></tr><tr><td>ISO 27001 Information security controls reference</td><td>Annex A 8.32</td></tr></tbody></table>

## OWASP

### Access Control mitigations

When it comes to access control, there are three pillars that need to be considered:

* Authentication: Ensure that no service accepts requests without some form of authentication.
* Authorization: Clearly define who can read/write/update/delete resources. Ideally, this is not done on a per-user basis, but on a per-role basis.
* Audit: Ensure that all access is logged so that you can alert on anomalies. Especially login failures should be logged.

Special considerations:

* Limit the IP sources for access.
* Disable meta-data serving through public endpoints (like what server is running in what version).
* Limit the outbound traffic of a node that runs a certain service.
* Apply rate limits to ensure that internal services cannot unintentionally DDos each other.
* Where possible apply the use of authentication tokens that have a limited lifetime.

**References:**

* [OWASP A01:2022: Broken Access Control](https://owasp.org/Top10/A01\_2021-Broken\_Access\_Control/)

#### Examples for best practices:

* [Webserver authentication configuration of Microsoft IIS servers.](https://learn.microsoft.com/en-us/iis/configuration/system.webserver/security/authentication/) Observe how different authentication methods are possible to be set there. `anonymousAuthentication` would allow anyone to access as `anonymous`, which is rarely the intention except for the starting page. `basicAuthentication` is better than nothing, but makes user management not scalable. `clientCertificateMappingAuthentication` and `digestAuthentication` are the better ways to also implement RBAC.

{% hint style="info" %}
**Links to risks:**

* GIR1
* GIR5
* GIR7
* GIR9
{% endhint %}

### Server-Side request forgery mitigations

An often overlooked aspect of attack vectors is server-side request forgery. In essence, an attacker sends (almost) random messages to the server and analyzes the response. Based on that, they are able to deduce behavioral patterns that can be used for a successful attack.

The most common goal of such attacks is to create some form of an overflow. Modern load-balancers and web-servers have built-in functionality that serve as a first line of defense against such mechanisms.

Functionality to look out for when creating your application is:

* Validate the user input against a given schema where possible.
* Limit the request size that the server accepts. This includes payload and header.
* Do not use redirections or symbolic links unless absolutely necessary.
* Use rate limits to make this attack infeasible.
* When writing user-input into a database, always use Object Relational Mappers to achieve maximal protection against SQL injection.

**References:**

* [OWASP A10:2021: Server Side Request Forgery](https://owasp.org/Top10/A10\_2021-Server-Side\_Request\_Forgery\_\(SSRF\)/)

**Examples for best practices:**

* ORM systems exist for almost all programming languages and frameworks. Some of the most common ones are [Hibernate](https://hibernate.org/orm/documentation/getting-started/), [TypeORM](https://typeorm.io) and [SQLAlchemy](https://www.sqlalchemy.org).
* In the Apache web-server, one can control the request size of different pieces of the request:
  * [LimitRequestBody](https://httpd.apache.org/docs/2.0/mod/core.html#limitrequestbody)
  * [LimitRequestFields](https://httpd.apache.org/docs/2.0/mod/core.html#limitrequestfields)
* In order to protect oneself from bad redirects, one can define proper [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) headers and a [ContentSecurityPolicy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP). Both are set in header fileds of your Web server or load balancer.

{% hint style="info" %}
**Links to risks**

* GIR8
{% endhint %}

## SOC 2

### Control activities to achieve operational goals

In a nutshell: technology needs to serve the business goal, not the other way around.

Main outline from the COSO principles:

1. **Technology Infrastructure Control** — Stakeholders develop control activities over the technology infrastructure, ensuring accuracy, availability and completeness of data.
2. **Security Access Control** — External threats are analyzed and access rights are properly defined.
3. **Third Party tool integration** — Integration, management, and updates of third party tools is closely monitored.

**References:**

* CC 5.2 of the Trust Services Criteria

**Examples for best practices:**

* Every third party software that is brought in needs to be known, and proper change management applied to it.
* Every third party software needs to be analyzed for the correct access rights with respect to users who can access it, but also the privileges it needs on the system it runs on. \
  Examples for this are:
  * Do not run main processes as root, since a compromised software can then execute privileged operations.
  * Do not allow uncontrolled inbound and outbound networking traffic to this specific service.

{% hint style="info" %}
**Links to risks:**

* GIR5
* DOW18
* DOW16
* SLA11 - SLA18
* SLA1 - SLA5
{% endhint %}

### Risk assessment of one's own Node operation

Node operation does not equal node operation. There are subjective goals for each organization, and the way they decided to operate. This control ensures that one is always having an eye on risk assessments.

Main outline from the COSO principles:

1. Considers Tolerances for Risk — Identify what is acceptable.
2. Complies With Externally Established Frameworks — Consider local and international laws and benchmarks when developing the node operation.

**References:**

* CC 3.1 of the Trust Services Criteria

**Examples for best practices:**

* Ensure that every service, where possible, is configuration hardened using common benchmarks such as [CIS](https://www.cisecurity.org).
* Analyze each component in your infrastructure environment in terms of security, availability, processing integrity, confidentiality and privacy.
* Outline directly which risks are a high priority, and which ones are more acceptable, and the scenarios where it applies. For example, downtime comes only with an opportunity cost for ETH stakers, but may cause a slashing event in Polkadot.

{% hint style="info" %}
**Links to risks:**

* GIR24
{% endhint %}

### Access Control

This is, by far, the most important mitigation. On- and off-boarding should be simple, and every piece of the infrastructure should be secured from unauthenticated and unauthorized access.

Main outline from the COSO principles:

1. Keep an inventory of information assets
2. Restrict Logical Access — Logical access to information assets, should be restricted through the use of access control software and rule sets.
3. Use authentication systems.
4. Network Segmentation — Restrict access to nodes to a minimum set of IPs.
5. Manages Points of Access — Access to nodes inside the segmented area need to be controlled with authentication and authorization methods.
6. Proper credentials management for infrastructure software — A clear definition of each credential life-time is established and enforced.
7. Protects Encryption Keys — Processes are in place to protect encryption keys for their lifetime.

**References:**

* CC 6.1 of Trust services Criteria

**Examples for best practices:**

* Creation and continuous analysis of Software Bill of Materials ([SBOM](https://www.cisa.gov/sbom)).
* Use of Clients, roles and groups when using [AWS IAM](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-iam-role.html).
* Have an internal virtual private network and only have well-defined endpoints be accessible from the web.
* Uses of vault systems to manage credentials and encryption keys. Like AWS KMS.

{% hint style="info" %}
**Links to risks:**

* DOW7
* KEC4
* GIR9
* GIR22
{% endhint %}

### Implement least privilege

This mitigation goes into the authorization piece of the different users and software pieces. The principle of least access should be considered, as much as possible. Putting measures in place that restrict access to certain groups as an afterthought can become fairly expensive.

Main outline from the COSO principles:

1. Creates or Modifies Access — Processes are in place to create or modify access.
2. Quick removal of access when needed
3. Use Role-based access control (RBAC)
4. Review of roles and permissions on a regular basis.

{% hint style="info" %}
**References:**

* CC 6.3 of the Trust services Criteria
{% endhint %}

**Examples for best practices:**

* Credentials rotation needs to be in place to ensure that there is no interruption in the service when it is done.
* Off-boarding of a terminated employee should not take more than an hour. Ideally, one would only disable them inside a single-sign-on service such as [Cognito](https://aws.amazon.com/cognito/) or [Keycloak](https://www.keycloak.org).
* Tools need to be in place to analyze the permissions of certain users/programs and determine if these are too wide.
* Use of roles on the API endpoint level to determine the correct authorization.



{% hint style="info" %}
**Links to risks:**

* KEC10
* GIR1
{% endhint %}

### Protection of Data in transit

Data remains rarely in one place. It is accessed, displayed, and analyzed. For each such operation, it needs to be ensured that there is no weakest link in the chain, and that any data in transit is protected as well.

Main outline from the COSO principles:

* Transmission of sensitive data needs to be restricted.
* Data in transit needs to be encrypted.

**References:**

* CC 6.7 of the trust services criteria

**Examples for best practices:**

* Ensuring that encrypted communication is enabled for each service. This includes, but is not limited to:
  * Databases
  * Web servers
  * Streaming services
  * Load balancers
  * Authentication systems
  * CI/CD pipeline tools
* Ensure that the latest version of TLS is being used, in combination with [secure algorithms](https://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#tls-parameters-4).

{% hint style="info" %}
**Links to Risks:**

* KEC1 - KEC3
* KEC4 - KEC9
{% endhint %}

### Capture configuration changes vulnerabilities

Main outline from the COSO principles:

* Uses defined Configuration Standards, monitor and enforce them.
* Detect configuration drift.
* Detect unwanted sofware installed on nodes.
* Conducts Vulnerability and Configuration security Scans.

**References:**

* CC 7.1 Trust services criteria

**Examples for best practices:**

* Many software pieces have defined configuration standards provided by [CIS benchmarks](https://www.cisecurity.org).
* Configuration standards can be enforced by automated software (e.g. [CoGuard](https://www.coguard.io))
* An example for monitoring software is the [ELK stack](https://www.elastic.co/elastic-stack/). A very common centralized dashboard is [Grafana](https://grafana.com).

{% hint style="info" %}
**Links to Risks:**

* GIR4
{% endhint %}

### Have Monitoring in place

Monitoring is so important, it is literally present in almost all compliance and security frameworks. It is crucial that not only high level business functions are monitored, but also correct functionality of all containers. In particular, proper log collection allows to dynamically verify that e.g. a slashing database ist actually being used, and used by the right signer.

Main outline from the COSO principles:

* Implements Detection Policies, Procedures, and Tools
* Design and improve on Detection Measures — Ideally capture unauthorized access, suspicios traffic, etc.
* Implement filters to not even let suspicious requests contact the back-end.
* Check frequently if detection tools are working correctly.

**References:**

* CC 7.2 of the SOC 2 trust services criteria.

**Examples for best practices:**

* Example of [alerting setup in Grafana.](https://grafana.com/docs/grafana/latest/alerting/set-up/)
* Cognito's [Userpool Addons for auditing authentications](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-cognito-userpool-userpooladdons.html).
* Filtering and anaysis of anomalies can be done in AWS using the[ WAF module](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-wafv2-webacl.html).

{% hint style="info" %}
**Links to Risks:**

* GIR13
{% endhint %}

### Analyze security events and learn from them

Main outline from the COSO principles:

* Have a proper incident response plan in place, and review it periodically.
* Communicates and Reviews Detected Security Events — Either take direct actions, or create tickets for future detection of events of a similar kind.
* Develops and Implements Procedures to Analyze Security Incidents.

**References:**

* CC 7.3 of the SOC 2 Trust services criteria.

**Examples for best practices:**

* Responses can and should also be automated. Ideally, high risk alerts cause the respective instances to be nuked.
* Always have post-mortems, ideally resulting in more unit- and integration tests of the organization.

{% hint style="info" %}
**Links to Risks:**

* DOW10
* GIR6
* GIR7
{% endhint %}

### Identify and respond to security incidents

Main outline from the COSO principles:

* Assigns Roles and Responsibilities in case of a security event.
* Contains Security Incidents — Ideally incidents can be contained within a short period of time.
* Communication protocols are in place to inform affected parties.
* Identified vulnerabilities need to be identified.
* Evaluate the identification and response on a regular basis.

**References:**

* CC 7.4 of the SOC 2 Trust services criteria

**Examples for best practices:**

* There are several incident response templates available. One example is [NIST SP 800-61](https://csrc.nist.gov/pubs/sp/800/61/r2/final).

{% hint style="info" %}
**Links to Risks:**

* RER1
* RER3
{% endhint %}

### Disaster recovery

This is by far the hardest to implement and to get right, but it is useful to not "train on an incident".

Main outline from the COSO principles:

* Quick restoration of affected enviroments.
* When possible, determine the root cause.
* Implement necessary changes to prevent similar disasters.
* Implements Incident-Recovery Plan Testing periodically.

**References:**

* CC 7.5 of the SOC 2 Trust Services Criteria

**Examples for best practices:**

* Use Minikube or docker-compose to create a local copy of a production environment to perform incident recovery plan testing.
* To restore affected environments and do all the automated events, one should run
* Use Chaos monkey to put your environment through the ultimate test.

{% hint style="info" %}
**Links to Risks**

* GIR19
{% endhint %}

### Proper change management

This is challenging for classically set up IT operations, but is straightforward if modern Infrastructure as Code principles are being used.

Main outline from the COSO principles:

* Manages Changes Throughout the System Life Cycle — To support system availability and processing integrity, any changes need to go through a well-defined process.
* Only perform authorized changes.
* Use a version control system for infrastructure.
* Maintain configuration of software in a code-base.
* Tests are in place for system changes.
* Have a ticketing system in place to document and review suggested changes.
* Have a controlled deployment.
* Have a way to directly identify historical changes to the infrastructure.
* A templated configuration of IT and control systems is created and maintained.
* Have breaking-glass change mechanisms in place for emergency situations.
* Protect confidential information to be leaked or accidentally accessed in the change management system.

**References:**

* CC 8.1 of the SOC 2 Trust Services Criteria

**Examples for best practices:**

* While this seems like a lot of points, most of them can be addressed by following the [GitOps lifecycle](https://about.gitlab.com/topics/gitops/#what-is-git-ops) to infrastructure.

{% hint style="info" %}
**Links to Risks**

* SLA6
* SLA7
* GIR3
* GIR18
* GIR20
* GIR21
{% endhint %}

### Develop Risk Mitigation Activities

Main outline from the COSO principles:

* Regularly develop and improve Mitigation of Risks of Business Disruption -- This should be automated where possible.

**References:**

* CC 9.1 of Trust Services Criteria

{% hint style="info" %}
**Links to Risks:**

* DOW6
{% endhint %}

### Vendors and business partners risk management

Main outline from the COSO principles:

* Establishes Requirements for Vendor and Business Partner Engagements.
* Assesses Vendor and Business Partner Risks - A process is in place to evaluate existing vendors.
* Ensure that previously identified issues with vendors are fixed and regressions may be identified.
* Implements Procedures for Terminating Vendor Relationships.

**References:**

* CC 9.2 of Trust Services Criteria

{% hint style="info" %}
**Links to risks:**

* SLA8
* SLA9
* GIR5
{% endhint %}

### Maintain the right operative capacity

Main outline from the COSO principles:

* Measures Current Usage in terms of computational resources.
* Have the ability to forecase capacity requirement changes.
* Have the ability to increse/decrease capacity when needed.

**References:**

* A 1.1 of the Trust Services Criteria

**Examples for best practices:**

* Current monitoring tools can also display a live feed of CPU and memory usage of each compute instance ([Zabbix reference](https://www.zabbix.com/documentation/6.4/en/manual/appendix/items/activepassive?hl=CPU%2Cload))

{% hint style="info" %}
**Links to risks:**

* DOW1
{% endhint %}

### Analyze system inputs for completeness and accuracy

Main outline from the COSO principles:

* Defines Characteristics of Processing Inputs, such as schemas.
* Evaluates Processing Inputs with defined requirements and compliance.
* Monitor the system inputs.

**References:**

* PI 1.2 of The Trust Services Criteria

**Examples for best practices:**

* Use [schema](https://json-schema.org) and [schema evolution techniques](https://en.wikipedia.org/wiki/Schema\_evolution) to keep your data-flow clean.
* Always define minimum and maximum input sizes and MIME types ([Microsoft IIS example](https://learn.microsoft.com/en-us/iis/configuration/system.webserver/staticcontent/mimemap)).

{% hint style="info" %}
**Links to Risks:**

* GIR8
{% endhint %}

### Analyze System outputs for completeness and accuracy

Main outline from the COSO principles:

* Inputs are processed completely, accurately, and timely.

**References:**

* PI 1.3 of the trust services criteria

**Examples for best practices:**

* Ensure that all inputs are being captured and either rejected or processed (schema enforcement).
* Data should be always referencable through a [unique ID](https://datatracker.ietf.org/doc/html/rfc4122).
* Data should be[ examined for](https://www.npmjs.com/package/ajv)[ correctness and completeness](https://github.com/validatorjs/validator.js).
* For each individual user, it should be determined if they are capable of accessing data or not. Using some technologies, such as [Apache Ranger](https://ranger.apache.org), this can be done on a row-by-row basis on a table.

{% hint style="info" %}
**Links to Risks:**

* GIR16
{% endhint %}

## ISO 27001

### Access Control

Main outline of the Information security controls reference:

* Rules to control physical and logical access to information needs to be in place.

**References:**

* ISO27001 Annex A 5.15

**Examples for best practices:**

* Role Based Access Control.
* Implement an authentication mechanism into every service.

{% hint style="info" %}
**Links to Risks:**

* SLA8
* SLA9
* GIR1
* GIR5
{% endhint %}

### Identity Management

Main outline of the Information security controls reference:

* The full life-cycle of a user or service identity needs to be managed.

**References:**

* ISO 27001 Annex A 5.16

**Examples for best practices:**

* Token lifetime.
* Off-boarding mechanisms.
* Potential use of 2FA

{% hint style="info" %}
**Links to Risks:**

* SLA8
* SLA9
{% endhint %}

### Authentication Information

Main outline of the Information security controls reference:

* Setting, revoking and updating access control and authentication needs to be a highly controlled managed process.

**References:**

* ISO27001 Annex A 5.17

**Examples for best practices:**

* Use of an [Single Sign on](https://en.wikipedia.org/wiki/Single\_sign-on) is preferred, and from there, all other secrets should be released to authorized users through e.g. [certificates](https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Certificate-based\_Authentication) and/or [vault mechanisms](https://developer.hashicorp.com/vault/docs/secrets/ssh/signed-ssh-certificates).

{% hint style="info" %}
**Links to Risks:**

* SLA8
* SLA9
{% endhint %}

### Access Rights

Main outline of the Information security controls reference:

* Access rights (authorization) needs to be reviewed regularly, and set accordingly with the organization's policies.

**References:**

* ISO 27001 Annex A 5.18

**Examples for best practices:**

* Role based access control should be used, and for each individual it needs to be automatically tested if their roles are set too wide, i.e. not minimal enough.

{% hint style="info" %}
**Links to Risks:**

* SLA8
* SLA9
{% endhint %}

### Physical Controls

Main outline of the Information security controls reference:

This is specific for the case where node operators are running their infrastructure on bare-metal and on their own premises.

* Protect physical areas and assets.
* Control entry to physical assets.
* All physical access to premises needs to be monitored.
* As much as possible, protect against environmental threats.
* Also secure off-site assets, if present.
* Supporting utilities, such as electricity and internet access, need to be protected.
* Maintain all equipment throughout a defined life-cycle.
* Enforce a strict rule of disposal and re-use of equipment.

**References:**

* ISO27001 Annex A 7

**Examples for best practices:**

* Camera systems at doors.
* Segregation of areas where people have access to.
* Thorough destruction of storage media.

{% hint style="info" %}
**Links to Risks:**

* DOW2
{% endhint %}

### Privileged access rights

Main outline of the Information security controls reference:

* Any allocation of privileged access needs to go through a proper review, audit and authorization process.

**References:**

* ISO27001 Annex A 8.2

**Examples for best practices:**

* Disable privilege escalation mechanisms ([like executing as root user inside a Docker container](https://docs.docker.com/engine/reference/commandline/container\_exec/))
* [Impersonation mechanisms need to be audited (if it is enabled).](https://github.com/keycloak/keycloak/blob/main/docs/documentation/server\_admin/topics/users/con-user-impersonation.adoc)

{% hint style="info" %}
**Links to Risks:**

* KEC10
{% endhint %}

### Protection against malware

Main outline of the Information security controls reference:

* Protection against malware needs to be implemented on all assets and users need to exercise proper caution.

**References:**

* ISO27001 Annex A 8.7

**Examples for best practices:**

* All depencencies should be checked for latest [CVE entries.](https://cve.mitre.org)

{% hint style="info" %}
**Links to risks:**

* GIR15
* GIR17
{% endhint %}

### Configuration Management

Main outline of the Information security controls reference:

* Any configurations of infrastructure components need to be documented, implemented, monitored and reviewed.

**References:**

* ISO27001 Annex A 8.9

**Examples:**

* This includes, but is not limited to:
  * Firewall configurations
  * Docker image setups
  * Container orchestration configurations
  * Database configurations
  * Webserver/Load balancer configurations
* Automated tools to track and scan for best practices are available (e.g. [CoGuard](https://www.coguard.io))

{% hint style="info" %}
**Links to risks:**

* GIR3
{% endhint %}

### Information deletion

Main outline of the Information security controls reference:

* Information which is no longer required needs to be safely deleted.

**References:**

* ISO 27001 Annex A 8.10

**Examples for best practices:**

* Definition and enforcement of retention periods.
* Use of thorough deletion mechanisms, such as [shred](https://man.archlinux.org/man/shred.1.en).

{% hint style="info" %}
**Links to Risks:**

* SLA10
* DOW17
{% endhint %}

### Monitoring Activities

Main outline of the Information security controls reference:

* All infrastructure components need to be monitored and proper alerting systems need to be in place.

**References:**

* ISO 27001 Annex A 8.16

**Examples for best practices:**

* See corresponding [SOC 2 control](https://app.gitbook.com/o/4wlsLrcXqEBGDqz0Hphy/s/xTRnDyIanlwU7cCKcAju/\~/changes/41/mitigation-and-controls-library/mitigation-strategies-and-best-practices/mitigation-strategies#to-meet-its-objectives-the-entity-uses-detection-and-monitoring-procedures-to-identify-1-changes-to).

{% hint style="info" %}
**Links to Risks:**

* GIR4
{% endhint %}

### Privileged utility programs

Main outline of the Information security controls reference:

* Any software in place that requires high privileges to run should be closely monitored, and as isolated as possible.

**References:**

* ISO 27001 Annex A 8.18

**Examples for best practices:**

* If there is an application that requires privileged access, any execution of it should be audited in a log.
* Access to this application should be granted only using a certificate-based authentication which as a timeout.

{% hint style="info" %}
**Links to Risks:**

* KEC10
* GIR6
* GIR7
{% endhint %}

### Network services

Main outline of the Information security controls reference:

* Any traffic needs to be monitored, analyzed and potentially alerted on.

**References:**

* ISO 27001 Annex A 8.21

**Examples for best practices:**

* Segmentation of networks using security groups and subnets.
* Encryption in transit should always be enabled.
* Use and enforcement of IP whitelists

{% hint style="info" %}
**Links to Risks:**

* DOW10
{% endhint %}

### Segregation of networks

Main outline of the Information security controls reference:

* Use private subnets where possible, and minimize the systems that belong to a given subnet.

**References:**

* ISO 27001 Annex A 8.22

**Examples for best practices:**

* [RFC 1918](https://www.rfc-editor.org/rfc/rfc1918)
* [Kubernetes Cluster Networking](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

{% hint style="info" %}
**Links to Risks:**

* DOW10
* GIR9
{% endhint %}

### Secure development life cycle

Main outline of the Information security controls reference:

* Use best practices to ensure that software development is happening in a secure and monitored way.

**References:**

* ISO 27001 Annex A 8.25

**Examples for best practices:**

* Use of CI/CD pipelines like GitHub Actions
* Use of Linters
* Use of enforced review processes
* Not allowing to directly push to the main branch

{% hint style="info" %}
**Links to Risks:**

* GIR8
{% endhint %}

### Testing

Main outline of the Information security controls reference:

* Use all possible tests (dynamic, static) in the CI/CD pipeline of your development lifecycle.

**References:**

* ISO 27001 Annex A 8.29

**Examples  for best practices:**

* Unit tests
* Dynamic tests
* Integration tests

{% hint style="info" %}
**Links to risks:**

* GIR20
* GIR21
{% endhint %}

### Outsourced development

Main outline of the Information security controls reference:

* Any outsourced development needs to be controlled, monitored and closely reviewed.

**References:**

* ISO 27001 Annex A 8.30

**Examples for best practices:**

* Proper ticketing system with clear expectations.
* Minimal access to do the job.

{% hint style="info" %}
**Links to risks:**

* GIR24
{% endhint %}

### Separation of development, test and production environments

Main outline of the Information security controls reference:

* Development, testing and production environments shall be separated and secured. Additionally, they should be virtually the same minus DNS, credentials and IP addresses.

**References:**

* ISO 27001 Annex A 8.31

**Examples for best practices:**

* Use [docker-compose](https://docs.docker.com/compose/) or [minikube](https://minikube.sigs.k8s.io/docs/) to define local-production-like environments.
* Use infrastructure as code to be able to spin up and tear down test environments.
* Have well-defined interfaces to pull part of the production data into a local database for testing.

{% hint style="info" %}
**Links to risks:**

* SLA6 - SLA7
* GIR11
* GIR18
{% endhint %}

### Change management

Main outline of the Information security controls reference:

* Use change management systems (e.g. GIT) for any information processing changes (infrastructure and software).

**References:**

* ISO 27001 Annex A 8.32

**Examples for best practices:**

* Using GIT also for infrastructure code and configurations.
* Use database migration systems such as [Liquibase](https://www.liquibase.org).

{% hint style="info" %}
**Links to risks:**

* DOW2
* DOW11
{% endhint %}
