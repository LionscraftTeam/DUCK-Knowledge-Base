---
description: This page summarizes different, node-operator specific mitigation strategies.
---

# Mitigation Strategies

## Node-Operator Technology Stack Mitigations

### Local anti-slashing database

To avoid double signing, validators maintain a history of messages they signed, and this is usually stored inside of a database. In some cases, this feature is enabled by an external web3signer. The maintenance and protection of this database is crucial, as inconsistencies in this database may cause a double-signing event. The following items need to be in place:

* Persistence of anti-slashing database: Ensure that a persistent, not a temporary storage is used for the anti-slashing database.
* Ensure that slashing databases are always connected: It is possible to run a validator and a database, but never connect those two. Verify via monitoring that they interact.
* Prevent deletion

{% hint style="info" %}
**Links to risks:**

* SLS1
* SLS2
* SLS3
{% endhint %}

### Doppelgänger protection

While there are multiple measures possible to be taken to avoid two validator running with the same signing keys, one can also employ technologies that detect and prevent two validators running at the same time. This can be done using monitoring and alert systems, robust StatefulSet handling in Kubernetes to ensure no two containers with the same keys run at the same time, or pre-defined tools such as [DoppelBuster](https://github.com/SimplyStaking/DoppelBuster).

{% hint style="info" %}
**Links to risks:**

* SLS2
{% endhint %}

### Use of a Web3Signer

The main benefit of the use of Web3 signers is to have a service that is focused on the signing task directly, and comes with protection mechanisms.

Similar to the anti-slashing database, whenever used, a web3signer needs to be

* Connected to a storage system (such as a database), and it needs to be ensured that it is always connected.
* Ensured that they are not accidentally terminated.
* Ensured that the failover is using the same web3signer

{% hint style="info" %}
**Links to risks:**

* SLS2 - SLS3
* SLS14 - SLS15
* KEC5 - KEC6
{% endhint %}

### Client diversity

Maintain a diverse set of clients for different protocols, in order to reduce blast radius in case one of the clients appears to have a protocol error or other bug. In some cases, migrate keys to different clients in case of a specific client error observed, such as startup issues after controlled update or bug in the latest version of the chosen client.

{% hint style="info" %}
**Links to risks:**

* SLS6
* SLS7
* DOW2
* DOW19
{% endhint %}

### Distributed Validator Technology (DVT)

In order to avoid the single-point of failure problem for a node-validator without risking a slashing incident, DVT has been developed.

{% hint style="info" %}
**Links to Risks:**

* SLS1
* SLS14
* SLS15
* KEC2 - KEC6
{% endhint %}

### Lido-specific: Handling of delinquent state&#x20;

In order to avoid loosing out on opportunity cost, Node operators need to develop and adhere to strict processes to properly exit validators, as they are otherwise put into a delinquent state. This results in monetary losses.

{% hint style="info" %}
**Links to risks:**

* SPS1
{% endhint %}

## Secret Management

### Controlled/audited secret access

Any secret needs to be accessed and authorized through a vault system. In this way, everything is audited, and anomaly detection can be activated for those vaults.

Also, multi-sig wallets should be used where appropriate.

Furthermore, access credentials for internal systems should also be stored inside those vaults, and key rotation managed from there.

{% hint style="info" %}
**Links to Risks:**

* SLS5
* KEC1 - KEC4
* KEC6
* KEC8
* KEC9 - KEC11
* GIR25
{% endhint %}

### Encryption of data at rest/in transit

Many different components interplay while a staking operation is going on. It is crucial, since sensitive information may be transmitted, to ensure that data is stored and transmitted in an encrypted fashion.

{% hint style="info" %}
**Links to risks:**

* SLS8
* KEC5 - KEC7
* KEC10 - KEC11
* GR10
{% endhint %}

### Store withdrawal keys in a cold location

Ideally, since these keys are not used often, it makes sense to store them in locations where data is not as often accessed. Ideally Air-Gapped.

{% hint style="info" %}
**Links to risks:**

* KEC5 - KEC7
{% endhint %}

### Employees and signing keys

Employees should not be able to delete signing keys and there should be a back-up for the signing keys. Modern vault systems can have policies where deletion is prevented by certain or all users. Signing keys should be only possible to be removed by the root-user or through some multi-signing mechanism.

{% hint style="info" %}
**Links to risks:**

* KEC10
{% endhint %}

### Access to unencrypted signing keys

The use case where an employee would need to access a signing key is low, and this should only be possible with a clear protocol when a support case is required. Vault systems can be set up that only verifier container roles can access these keys.

{% hint style="info" %}
**Links to risks:**

* KEC2
* KEC11
{% endhint %}

### Key rotation

Key rotation and a proper process around it is key to protect one's infrastructure from a potential breach of credentials. When in doubt, keys should be rotated. This includes, but is not limited to:

* The Postgres database used by Web3Signer
* The vault itself
* Any SSH keys
* Any API keys for your cloud infrastructure

{% hint style="info" %}
**Links to risks:**

* SLS8
* GIR6 - GIR7
{% endhint %}

## Access Management

### Access controls & access management

The principle to follow is "least privilege". This is usually achieved by using an enforcing role-based access control, and create fine-grained roles throughout all processes of an organization.

Each user should be assigned roles, and some are temporary. There should be a clear lifetime of a user, that is automatically enforced and can be extended when needed.

{% hint style="info" %}
**Links to risks:**

* SLS8 - SLS9
* DOW16
* GIR1
* GIR7
* GIR22
{% endhint %}

### Least Privilege

Even when employing RBAC, there are ways to log into containers as users and acquire larger privileges from there. Take `docker exec -uroot` as an example. These mechanisms can be disabled on the orchestration level (and should be).

{% hint style="info" %}
**Links to risks:**

* SLS8 - SLS9
* DOW16
* GIR1
* GIR22
* KEC8
* GIR25
{% endhint %}

### Strict employment termination process in place

Ensure that terminated employees do not have lingering credentials they can use to cause harm.

{% hint style="info" %}
**Links to risks:**

* SLS10
* DOW17
* GIR25
{% endhint %}

### No access from external network to the nodes

Following the principle of defense in depth and least privilege, it is important that nodes are generally not accessible from the web. Any web access should be proxied through a load-balancer that has a firewall attached to it. The reason is that there are many software pieces on a node, potentially, and the attack vector due to a potential CVE may be incresed.

{% hint style="info" %}
**Links to risks:**

* SLS12
{% endhint %}

### Strong authentication

Use password policies at every layer of the infrastructure (i.e. DUCK123 should never be an allowed password ;-)). When users are authenticating, MFA should be used.

{% hint style="info" %}
**Links to risks:**

* SLS13
{% endhint %}

### Prevent physical access to non-authorized persons

This is mainly for bare-metal installations. If you host your nodes on-premise, ensure that physical access to the servers is restricted through a key-mechanism. Ideally, any entry and exit should be logged.

{% hint style="info" %}
**Links to risks:**

* DOW4
* KEC6
* KEC8
{% endhint %}

## Development and Update Process

### Testing and review of all changes to infrastructure code&#x20;

Anything on the infrastructure should be captured in a code repository, and changes managed through a versioning system such as Git. No direct push to the main branch should be possible; everything should go through pull requests and review.

All code should go through static and dynamic analysis tools to minimize risk.

There should be custom tests created, and a strict testing policy before pushing to prod needs to be in place.

Ideally, metrics should be used to verify a high degree of testing culture. This includes, but is not limited to:

* Line coverage
* Endpoint coverage
* Accidental human error detection
* Architectural enforcement

{% hint style="info" %}
**Links to risks:**

* SLS4-SLS7
* SLS18
* DOW2
* DOW6
* DOW11-DOW14
* GIR11
* GIR13
* GIR18
* GIR21
* GIR23-GIR24
* DOW19
* DOW20
{% endhint %}

### No custom changes to the validator software

Validator software is open source, but in order to ensure that no protocol error occurs, the code should not be touched.

{% hint style="info" %}
**Links to risks:**

* SLS7
* DOW13
* DOW19
* DOW20
{% endhint %}

### Sanitize inputs

Unchecked inputs are a major cause for overflow attacks and brute force. Ideally, the load balancer in front of the node filters out all traffic that has too large headers and payloads. Additionally, if JSON payloads are being used, they should be checked to adhere to a certain schema.

{% hint style="info" %}
**Links to risks:**

* GIR8
{% endhint %}

### Use of separate tests and staging environments

This minimizes a potential blast radius. It is important to run any change (even an update of a validator software or Web3Signer) through a test environment first, and then roll it out in a staged fashion. If it causes some slashing event, it is then contained to the few nodes that it was rolled out to.

{% hint style="info" %}
**Links to risks:**

* GIR11
* DOW19
* DOW20
{% endhint %}

### Use containerized and orchestrated environments only.

Follow their best practice recommendations. Their mechanisms are more than battle-tested in different environments. Any make-shift approach to do mechanisms such as fail-over by hand should be deemed insecure.

{% hint style="info" %}
**Links to risks:**

* GIR23
{% endhint %}

### Automation where possible

Human error is a real threat, and every process should at least follow an automated script that may or not be invoked by a human. The other risk of non-manual steps is the reduction of the risk of exposure of secrets. Everything should be done through pipelines and job-mechanisms (GitHub Actions, Apache Airflow, Apache Nifi)

{% hint style="info" %}
**Links to risks:**

* GIR16
* GIR18 - GIR21
* SLS17
* DOW19
* DOW20
* GIR25
{% endhint %}

### Minimize CVEs in images

Analyzing images for potential CVEs is simple nowadays (use e.g. [Trivy](https://github.com/aquasecurity/trivy)). Further configurations inside these images can be checked using [CoGuard](https://www.coguard.io). Any image used in your infrastructure should be checked this way.

{% hint style="info" %}
**Links to risks:**

* GIR17
{% endhint %}

## Monitoring

### Logging/Alerting at all levels of the infrastructure

Every component of your node operation is producing logs. These should be captured, analyzed, and alert systems should be set up to warn if something is wrong. Examples include, but are not limited to:

* Web3Signer database has no CRUD operations going on (is it connected?)
* CPU/Memory spike suddenly in container
* Network traffic in and out of container
* Relays
* Slashing related logs on validator nodes

The alert systems should be automatically set up to take actions such as shutting nodes down (nuking).

{% hint style="info" %}
**Links to risks:**

* SLS8
* SLS16
* DOW6
* DOW15
{% endhint %}

## General Measures

* General cyber security (Firewall, Intrusion Detection System, ....)
* Check the uptime promise of cloud provider (minimum three 9s)
* Failover system (also in different locations)
* Keeping track of age and replacing appliances
* Conduct an internal special study of failover and load balancer strategies
* Securing the physical access
* Being informed about the relevant natural catastrophes
* Ensure stable Internet connection of the System (Cloud, Bare Metal, ....)
* Ensure stable Power connection of the System (Cloud, Bare Metal, ....)
* Ensure proper load-balancer and firewall at the front
* Only necessary software on the relevant servers
* Being able to switch the relayer or disconnect from the relay
* Back-Up/DR / BC Policies
* Validate cloud, data center or infrastructure provider regarding security
* Safety training
* Central & accessible documentation of critical knowledge
* Having a communication toolkit and process prepared
* Having a incident response policy / strategy
