# Risk Management Procedures

Processes and actions that should be defined to address risks and that cover the concrete procedures in case of related incidents. &#x20;

## 1. Risk Monitoring

Leverage monitoring dashboards or systems to identify the risk and gain relevant data.

### Beacon Chain Monitoring

* **Slashing Events:** Monitor the beacon chain for any slashing events.
* **Anti-Slashing Database:** Regularly poll the local node to ensure the anti-slashing database is enabled and functioning correctly.
* **Impact of Slashing:** Assess and monitor the broader impact of any slashing incidents on the network.
* **Relay List Monitoring:** Monitor the relay list for availability metrics and load balance capabilities between various relayers for downtime conditions.
* **Chain Reorganizations:** Track events and causes of chain reorganizations&#x20;
* **Non-finalized Events:** Monitor events preventing the consensus layer from confirming finality
* **Special Software Conditions:** Monitor major software upgrades requiring specific durations and   events that will conclude the upgrade

### Node and System Health

* **Node Health Metrics:** Monitor key metrics like CPU, memory, restarts, and uptime of nodes.
* **System Configuration:** Monitor system configuration settings in real-time and continuously.
* **Key Usages:** Track the usage of critical system keys.
* **App-specific:** App specific metrics  (e.g. metrics for Dirk & Vouch)

### Security and Compliance

* **Access Control and Logs:** Keep an eye on access controls to nodes and abnormal configuration changes.
* **Phishing and Endpoint Protection:** Monitor for phishing attacks and ensure the security of endpoint protection systems, both for employee devices and infrastructure nodes.
* **Bastion Nodes:** If applicable, monitor bastion or connection nodes.
* **Suspicious Internal Interactions:** Watch for any suspicious internal interactions with infrastructure, cloud security platforms, or network monitoring solutions.
* **Access Patterns and Configurations:** Check for unusual access patterns and the configurations of VPNs and 2FA systems.
* **Relay Compliance:** Monitor relay compliance aspects and availability metrics.

### Upgrade and Code Management

* **Upgrade Process:** Monitor the upgrade process, including client code source, notification channels, bug reports, and community disclosures.
* **Customized Code in Testnet:** Monitor any new custom code deployed in the testnet.

### Hardware and Network

* **Baremetal and Network Equipment Health:** Monitor the health of bare metals and networking equipment, including internet and peering connectivity.
* **Predictive Models:** Use predictive models for future malfunctions and equipment replacement needs.
* **Capacity and Resource Usage:** Track capacity usage, processing memory, and CPU.
* **Peering Connectivity:** Monitor both internal and external network peering connectivity.
* **Firewall Configuration and Metrics:** Keep an eye on firewall configuration changes or unexpected increases in drop metrics.

### Cloud and Infrastructure

* **Cloud Monitoring Solutions:** Utilize cloud monitoring solutions to keep track of uptime and internal issues.
* **Cloud Service Notifications:** Stay informed about cloud service announcements regarding expected downtime and maintenance.

{% hint style="info" %}
Take a look at [collection-of-tools-scripts-and-templates.md](../mitigation-and-controls-library/collection-of-tools-scripts-and-templates.md "mention") for tool examples to perform the monitoring of some of the metrics mentioned above.
{% endhint %}

## 2. Incident Response Plan

Define Incident Response Plans (ICR) for all specific [risks](risks/ "mention") and store them in a central location with access for all relevant employees. ICRs establish plans for managing security incidents and events, and offer guidance for employees or incident responders who believe they have discovered, or are responding to, a security incident. Ensure that relevant employees are aware of the location. Simulations of an Incident Response Plan should be conducted at least once a year.

{% hint style="info" %}
Incident Response Plan template can be found here:\
[https://docs.google.com/document/d/1ynZfeMh3vxZu7Juh-f34b50\_3WHgejiL/edit?usp=sharing\&ouid=117284374075970906179\&rtpof=true\&sd=true](https://docs.google.com/document/d/1ynZfeMh3vxZu7Juh-f34b50\_3WHgejiL/edit?usp=sharing\&ouid=117284374075970906179\&rtpof=true\&sd=true)
{% endhint %}

## 3. Disaster Recovery Plan

A Disaster Recovery Plan gives guidance on recovering one or more information systems at an alternate facility in response to a major hardware or software failure or destruction of facilities. Simulations of a Disaster Recovery Plan should be conducted at least once a year in a test environment.

{% hint style="info" %}
Disaster Recovery Plan templates can be found here:

* [National Institute of Standards & Technology Template](https://csrc.nist.gov/files/pubs/sp/800/34/r1/upd1/final/docs/sp800-34-rev1\_cp\_template\_high\_impact\_system.docx)
* [#automation](../mitigation-and-controls-library/collection-of-tools-scripts-and-templates.md#automation "mention")
{% endhint %}

## 4. Pre-Mortem

Perform Pre-Mortems for specific risks. The article linked below provides instructions on how to use Pre-Mortems to prevent incidents. Example topics for a Pre-Mortem could be&#x20;

* Unauthorized users could gain access to the servers
* In the case of a security compromise it is not clear what to do
* A specific scenario could result in downtime

[https://medium.com/@shreyashere/how-to-use-pre-mortems-to-prevent-problems-blunders-and-disasters-6ecc6df6e22a](https://medium.com/@shreyashere/how-to-use-pre-mortems-to-prevent-problems-blunders-and-disasters-6ecc6df6e22a)
