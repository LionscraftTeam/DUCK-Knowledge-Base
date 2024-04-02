# Incident Communication Protocols

Incidents can lead to a massive impact on Node Operators and their stakeholders. They can result in far more than only direct financial losses but also in irreversible reputational and collateral damages. In order to minimize incident impacts and ensure effective analysis and communications, the standardized communication protocols in this section give a reference for relevant procedures.&#x20;

The **Incident Communication Protocols** equip Node Operators with guidelines around predefined procedures that cover both internal and external procedures.&#x20;

## Internal Procedures

### 📋 Pre-Incident

1. Define relevant internal teams and stakeholders for specific incidents in the respective Incident Response Plan (see [risk-management-procedures.md](../risk-framework/risk-management-procedures.md "mention"))
2. Define dedicated channels of communication in the case of an incident

### 🚨 During Incident

1. Create an incident async communication channel (Slack, Telegram, or similar).
2. Initiate defined procedures in respective Incident Response Plan.
3. Investigate the specific incident if the root cause is not clear:

* Escalate to relevant team (based on the specific risk).
* Collect generic data about the incident from the detection/monitoring system or the infrastructure.
* Have “Involved teams” in Incident Response Plan depending on the triaged risk and invite the relevant stakeholders in the order defined.

4. Collect data and create documentation for:

* Executive summary and communication procedures
* Technical details and sync of team members as the incident progresses
* Optional: Incident response platform can be used to do that in a more efficient manner&#x20;

5. Create a communication matrix what should or should not be communicated and the communication of information to departments inside the organization.

### 🔎 Post-Incident

1. Create internal post-incident summaries.
2. Create summaries for executives and communications with next steps.
3. Apply new monitoring and detection to limit future risk exposures.
4. Perform extensive post-mortem analysis (see [post-mortem-analysis.md](templates-and-toolkits/post-mortem-analysis.md "mention")).

## External Procedures

### 📋 Pre-Incident

* Define relevant external stakeholders for specific incidents in the respective Incident Response Plan
* Define dedicated channels of communication in the case of an incident

### 🚨 During Incident

1. Involve relevant teams of legal, privacy, policy, and communication departments (if applicable).
2. Update executive and internal teams before any external communication.
3. Ensure to communicate only when things are certain and clear 100%.
4. Handle the sharing of information based on the respective incident response plan.

{% hint style="info" %}
**NOTE:** Communicating as an incident is ongoing can result in further damage, only communicating about the root cause when it is identified and potentially resolved on a case-by-case basis.
{% endhint %}

### 🔎 Post-Incident

1. Decide on information and level of detail of the post-mortem analysis (see [post-mortem-analysis.md](templates-and-toolkits/post-mortem-analysis.md "mention")) to be shared with the different stakeholders ([stakeholder-management.md](stakeholder-strategy/stakeholder-management.md "mention")) across the communication channels.
